# Summary

This documents provides guidelines on setting up CI scripts to report code coverage as well as using the AxoCover Visual Studio plugin for calculating coverage when developing locally.

# Contents

- [Background](#background)
- [Calculating Code Coverage](#calculating-code-coverage)
  * [Using OpenCover](#using-opencover)
    + [Including Debugging Symbols](#including-debugging-symbols)
    + [Excluding Code](#excluding-code)
    + [Ensuring Correct Output](#ensuring-correct-output)
  * [Using ReportGenerator](#using-reportgenerator)
- [Configuring CI Scripts](#configuring-ci-scripts)
  * [Before Starting](#before-starting)
    + [Note on Caching](#note-on-caching)
    + [Initial CI Script](#initial-ci-script)
    + [Include Debugging Symbols](#include-debugging-symbols)
  * [Single Test Project](#single-test-project)
    + [Reporting OpenCover Output](#reporting-opencover-output)
    + [Reporting ReportGenerator Output](#reporting-reportgenerator-output)
  * [Multiple Test Projects](#multiple-test-projects)
    + [Calculating Code Coverage](#calculating-code-coverage-1)
    + [Reporting Code Coverage](#reporting-code-coverage)
- [Calculating Coverage Locally](#calculating-coverage-locally)
  * [Running Commands Manually](#running-commands-manually)
  * [Using AxoCover](#using-axocover)
    + [Update `.gitignore`](#update-gitignore)
    + [Update AxoCover Settings](#update-axocover-settings)
    + [Run Coverage Analysis](#run-coverage-analysis)
- [External Links](#external-links)

# Background

We have adoped test-driven development as a step toward improving code quality, but a set of passing tests only gives a partial indication of code quality.  Code coverage metrics help give us an idea of the completeness of our tests; that is, they tell us how much of our code is being tested.  After all, a suite of 200 tests is not impressive when those tests only cover 5% of the code.

The two tools we use for calculating code coverage are [OpenCover](https://github.com/OpenCover/opencover) and [ReportGenerator](https://github.com/danielpalme/ReportGenerator).  OpenCover is responsible for calculating the code coverage, but it has a couple of limitations.  First, OpenCover can only calculate code coverage on a single test container (DLL), so using it by itself requires that all tests be contained in a single test project.  Second, OpenCover's reporting capability is nearly non-existent.  It will generate a full set of XML output, but the human-readable console output leaves something to be desired:

```
Committing...
Visited Classes 7 of 14 (50)
Visited Methods 18 of 36 (50)
Visited Points 68 of 136 (50)
Visited Branches 40 of 80 (50)

==== Alternative Results (includes all methods including those without corresponding source) ====
Alternative Visited Classes 10 of 22 (45.45)
Alternative Visited Methods 25 of 70 (35.71)
```

ReportGenerator augments OpenCover's functionality by reading its output and generating more granular reports.  ReportGenerator is capable of producting full line-by-line reports, but a textual summary report is sufficient for CI purposes, since it gives both an overall summary and a per-assembly, per-class summary:

```
Summary
  Generated on: 7/28/2017 - 1:45:23 PM
  Parser: OpenCoverParser
  Assemblies: 3
  Classes: 80
  Files: 58
  Line coverage: 28.1%
  Covered lines: 1151
  Uncovered lines: 2944
  Coverable lines: 4095
  Total lines: 9732

ITSMConnect                                                                  26.4%
  ITSMConnect.AutofacModules.LoggingModule                                  100.0%
  ITSMConnect.Controllers.AccountController                                   0.0%
  ITSMConnect.Controllers.AdminController                                         
  [Output Truncated]

ITSMConnect.Model                                                            35.7%
  Model.ApiKey                                                                    
  Model.CablePair                                                                 
  Model.EntityBase`1                                                         35.7%
  [Output Truncated]                                          

ITSMConnect.Persistence                                                      66.8%
  ITSMConnect.Persistence.Dao.ApiKeyDao                                           
  ITSMConnect.Persistence.Dao.Implementation.Repository`2                    68.1%
  ITSMConnect.Persistence.Dao.Mapping.ApiKeyMap                             100.0%
  [Output Truncated]
```

In addition, ReportGenerator is capable of providing an aggregate summary from multiple OpenCover output files.

# Calculating Code Coverage

Both OpenCover and ReportGenerator are executed via the command line.  There are two basic cases that require slightly different commands, depending on how the solution's testing projects are set up.  The first case occurs when all tests are included in a single project and the second when the tests are split into multiple projects.  The size and scope of the project will determine whether the tests are combined or separate.

OpenCover essentially acts as a wrapper for a unit testing tool, so coverage is calculated while the tests are run.  In some cases, the console output from OpenCover can be used to report code coverage to GitLab.  In other cases, ReportGenerator must be used to aggregate multiple OpenCover output files.

## Using OpenCover

OpenCover works by passing appropriate arguments to define what should be analyzed and what should be excluded.  Here is an example of an OpenCover command-line call:

```
OpenCover.Console.exe -target:"mstest.exe" -targetargs:"/testcontainer:Tests\bin\Test\RestApi.Tests.dll" -filter:"+[RestApi*]* -[RestApi.Tests]*"  -register:path32 -returntargetcode -skipautoprops -excludebyattribute:*.ExcludeFromCodeCoverageAttribute -hideskipped:All -mergebyhash
```

First, we start by calling `OpenCover.Console.exe`, will actually calculate code coverage.  Since OpenCover is a wrapper for a unit testing tool, we must specify which executable will be used to perform unit testing (MSTest in our case).  This is specified by the <code>&#8209;target:"mstest.exe"</code> argument.  Additionally, MSTest requires as an argument the test container (DLL), which is specified by the <code>&#8209;targetargs:"/testcontainer:Tests\bin\Test\RestApi.Tests.dll"</code> argument.  Given those two arguments, OpenCover will execute MSTest for us and generate a set of results (by default, OpenCover outputs to `results.xml`).

### Including Debugging Symbols

Note that OpenCover requires debugging symbols for the project being analyzed, and that debugging symbols can be included when the project is built.  Visual Studio generally creates a build profile called `Debug`, which will generate debugging symbols, however if you prefer to use a different build profile, you can pass an argument to MSBuild to tell the compiler to include debugging symbols.  OpenCover only requires the PDB files:

```
msbuild.exe RestApi.sln /p:Configuration=MyBuildConfig;DebugSymbols=true;DebugType=pdbonly
```

### Excluding Code

OpenCover provides multiple options for excluding classes and methods, but the primary way is to use filters defined in the `filter` argument.  These can be either include (+) or exclude (-) filters and can use wildcards (\*) to work on one or more assemblies and namespaces.  In the example command above, there are two filters, `+[RestApi*]*` and `-[RestApi.Tests]*`.  A filter must be formatted so that it begins with + or - to indicate include or exclude, respectively.  Next, the assembly name is given in square brackets (with or without wildcards).  Finally, the namespace to filter is given.  For example, `+[RestApi*]*` is parsed by OpenCover as follows:

| Filter Part | Purpose |
| ----- | ----- |
| `+` | Include assemblies and namespaces. |
| `[RestApi*]` | Use all assemblies that begin with `RestApi`. |
| `*` | Use all namespaces in the specified assemblies. |

OpenCover also provides some arguments that can be used to exclude code.  In the above example, the <code>&#8209;skipautoprops</code> argument will not consider any auto-implemented property such as 

```c#
public string MyString { get; set; }
```

Additionally, any methods given the `ExcludeFromCodeCoverage` attribute will also not be considered because of the <code>&#8209;excludebyattribute:*.ExcludeFromCodeCoverageAttribute</code> argument, which says to ignore them.

A good rule of thumb is to use filters when the exclusion needs to apply to multiple classes (e.g. all classes in a namespace or all classes with names matching a given pattern) and to use the `ExcludeFromCodeCoverage` attribute to selectively exclude single classes or methods.

To exclude a class using `ExcludeFromCodeCoverage`:

```c#
[ExcludeFromCodeCoverage]
public class MyClass
{
  // Code here.
}
```

To exclude a method using `ExcludeFromCodeCoverage`:

```c#
public class MyClass
{
  [ExcludeFromCodeCoverage]
  public void MyMethod
  {
    // Code here.
  }
}
```

### Ensuring Correct Output

The remaining arguments in our example command are meant to ensure that OpenCover runs correctly:

- <code>&#8209;register:path32</code>:  Registers the code coverage profiler.
- <code>&#8209;returntargetcode</code>:  MSTest works such that it returns an error return code whenever one or more tests fail.  However, since OpenCover acts as a wrapper for MSTest, the return code will be based upon whether OpenCover was able to successfully call MSTest and generate an output file.  This means that OpenCover will generally return a success code even if there are failing tests, which prevents the CI pipeline from failing during the testing/coverage stage.  By including the <code>&#8209;returntargetcode</code> argument, we tell OpenCover to ignore its own successes and return the code produced by MSTest, so that our CI pipeline is correctly informed of test successes and failures.
- <code>&#8209;hideskipped:All</code>:  By default, OpenCover will report on all methods in all classes, even if they are excluded.  The <code>&#8209;hideskipped:All</code> argument tells OpenCover to exclude skipped methods from the output XML, which makes the output files slightly easier to read.
- <code>&#8209;mergebyhash</code>:  MSTest will often load the same assembly from different locations which causes OpenCover to report as separate assemblies.  The <code>&#8209;mergebyhash</code> argument tells OpenCover to report all assemblies with the same file hash as a single assembly.  This helps ensure that the console output is correct.

More information on OpenCover arguments is available at the [OpenCover usage page](https://github.com/opencover/opencover/wiki/Usage).  

## Using ReportGenerator

Once OpenCover generates its output file or files, ReportGenerator can be used to produce readable reports.  Here is an example of a ReportGenerator command line call:

```
ReportGenerator.exe "-reports:results.xml" "-reporttypes:TextSummary" "-targetdir:.\"
```

In this example, the ReportGenerator executable is called and given the name of the output file from OpenCover (unless otherwise specified, OpenCover saves its output in `results.xml`) as well as the type of report to create and the directory in which to create it.  Here, we are creating a simple text summary which will be echoed to the console and used by the CI pipeline to report code coverage.  ReportGenerator can also create fully-detailed HTML or LaTeX reports, however you should generate those in a subdirectory rather than in the solution directory as ReportGenerator will create one page for each class being covered plus related images.  Note also that ReportGenerator's arguments must be wrapped in double quotes.  

More information on ReportGenerator usage is available at the [ReportGenerator usage page](https://github.com/danielpalme/ReportGenerator#usage).

# Configuring CI Scripts

The [GitLab server](https://code.cmich.edu) has both OpenCover and ReportGenerator installed and ready to use.  You only need to configure the project's CI script (`.gitlab-ci.yml`) to analyze and report code coverage.  This document illustrates how to configure the CI script both when the solution contains a single test project and when the solution contains multiple test projects.

## Before Starting

This document makes some assumptions that are give in the following subsections.  In addition, your project build command may need to be updated for code coverage to work.

### Note on Caching

This document assumes that your CI script uses caching (i.e. defines a `cache`).  At the time of writing, not all project CI scripts use caching, but instead some repeat steps from previous stages.  If your project's CI script does not use caching, you will see some command duplication in your script that does not appear in the following examples. Solutions with multiple test projects must be updated to use caching so that the results of the testing/coverage stage are available to the coverage reporting stage.

### Initial CI Script

This document assumes that all CI scripts have a standard form and that a script from any given project fairly closely resembles the script from any other project.  Specifically, the document assumes that all scripts have standard stages (`restore`, `build`, `test`, and `deploy`), and that all scripts will use the same commands for executing those stages (NuGet.exe, MSBuild.exe, MSTest.exe, etc.).  Therefore, the full scripts will not be illustrated.  Instead, we will present the relevant portion of the script as it looks initially, and then illustrate the script after the necessary changes have been made.

### Include Debugging Symbols

Before you can calculate code coverage, you must first update the build stage so that it includes debugging symbols.  In the `build` stage's script, look for the line that calls `msbuild`.  Change the build command to include debugging symbols (PDB only) as illustrated in the [Including Debugging Symbols](#including-debugging-symbols) subsection above.  The `Debug` build profile created by Visual Studio will already be configured to include debugging symbols.

## Single Test Project

When a solution contains a single test project, you only need to update the stage that runs all tests.  Suppose we have a CI script with the following stage defined:

```yaml
test_all:
  stage: test
  script:
    - echo 'Running tests...'
    - mstest /testcontainer:Tests\bin\Test\Enterprise.Tests.dll
  only:
    - master
    - testing
    - production
```

In this case, all tests are run whenever there is a change to the `master`, `testing`, or `production` branches.  Not all projects will be configured this way, so you will have to review the CI script for your project to determine the best place to make the change;  you may even decide to add a new stage.  However, in our example, the jobs in the script will remain the same, but the `test_all` job will be updated:
- The job must be updated to use OpenCover to run the tests
- A coverage setting must be added to the job so that GitLab will report the results

Updating the job to use OpenCover is pretty straightforward.

```
mstest /testcontainer:Tests\bin\Test\Enterprise.Tests.dll
```

will be replaced with 

```
OpenCover.Console.exe -target:"mstest.exe" -targetargs:"/testcontainer:Tests\bin\Test\Enterprise.Tests.dll" -filter:"+[Enterprise*]* -[Enterprise.Tests]*" -excludebyattribute:*.ExcludeFromCodeCoverageAttribute -register:path32 -returntargetcode -skipautoprops -hideskipped:All -mergebyhash
```

to ensure that code coverage is calculated.  You will need to check the properties for the projects in your solution to determine the appropriate assembly and namespace names.

### Reporting OpenCover Output

OpenCover will report line coverage on its own, so ReportGenerator is not strictly necessary in this case.  To report the line coverage based on OpenCover's output, you will need to add a `coverage` setting to the job.  This setting is a regular expression pattern that the CI runner can use to determine the coverage.  As illustrated in the [Background](#background) section above, OpenCover will report line coverage as "visited points" with this pattern: `(Visited Points).*\((.*)\)`.  Thus the new job configuration is:

```yaml
test_all:
  stage: test
  coverage: '/(Visited Points).*\((.*)\)/'
  script:
    - echo 'Running tests...'
    - OpenCover.Console.exe -target:"mstest.exe" -targetargs:"/testcontainer:Tests\bin\Test\Enterprise.Tests.dll" -filter:"+[Enterprise*]* -[Enterprise.Tests]*" -excludebyattribute:*.ExcludeFromCodeCoverageAttribute -register:path32 -returntargetcode -skipautoprops -hideskipped:All -mergebyhash
  only:
    - master
    - testing
    - production
```

### Reporting ReportGenerator Output

You may find that you prefer to use ReportGenerator since it also breaks down coverage by assembly and class.  In that case, you will need to configure the job to read OpenCover's output and generate the coverage report.  As with configuring OpenCover, the only changes are to the `test_all` job.  However, there are two additional steps that must be added:  create the ReportGenerator report and print the report to the console.  First, add the step for creating the report:

```yaml
- echo 'Analyzing code coverage...'
- ReportGenerator.exe "-reports:results.xml" "-reporttypes:TextSummary" "-targetdir:.\"
```

This step uses the default output file from OpenCover (`results.xml`) and generates a summary text file (`Summary.txt`).  However, simply calling ReportGenerator produces no console output, so the CI runner cannot read the coverage metric.  Therefore, once the report has been generated, we can use the `TYPE` command to print the report to the console:

```yaml 
- type Summary.txt
```

Additionally, the output from ReportGenerator is different than that of OpenCover and requires a different matching pattern:  `Line coverage:\s+.*\%`.  Therefore, when using ReportGenerator, the new job configuration is:

```yaml
test_all:
  stage: test
  coverage: '/Line coverage:\s+.*\%/'
  script:
    - echo 'Running tests...'
    - OpenCover.Console.exe -target:"mstest.exe" -targetargs:"/testcontainer:Tests\bin\Test\Enterprise.Tests.dll" -filter:"+[Enterprise*]* -[Enterprise.Tests]*" -excludebyattribute:*.ExcludeFromCodeCoverageAttribute -register:path32 -returntargetcode -skipautoprops -hideskipped:All -mergebyhash
    - echo 'Analyzing code coverage...'
    - ReportGenerator.exe "-reports:results.xml" "-reporttypes:TextSummary" "-targetdir:.\"
    - type Summary.txt
  only:
    - master
    - testing
    - production
```

## Multiple Test Projects

Calculating code coverage in a solution with multiple test projects is slightly different than in a solution with a single test project.  First, you cannot use the console output generated by OpenCover because OpenCover must analyze test containers individually (due to a limitation of MSTest).  Therefore, you must use ReportGenerator to report code coverage.  

Second, due to a limitation in how GitLab caching works, all tests must be conducted in the same job.  Since all jobs in a stage are run in parallel, each will attempt to create the cache, but the CI runner will only persist the cache from the last job to successfully complete, which means that inaccurate code coverage will be reported (i.e. ReportGenerator will only be given one OpenCover output file).  You may use artifacts as a workaround, but the topic is outside the scope of this document.  The following examples will assume that your CI script configures a cache.

Please refer to the [GitLab documentation](https://docs.gitlab.com/ce/user/project/pipelines/job_artifacts.html) for more information about artifacts.

### Calculating Code Coverage

Suppose we have a CI script with the following cache and testing jobs defined:

```yaml
cache:
  key: "%CI_COMMIT_SHA%"
  paths:
    - packages/
    - Persistence/
    - Persistence.Tests/
    - Models/
    - Models/Tests/
    - Web/
    - Web/Tests/

test_persistence:
  stage: test
  script:
  - echo 'Running persistence tests...'
  - mstest.exe /testcontainer:.\Persistence.Tests\bin\Test\MyApp.Persistence.Tests.dll

test_web:
  stage: test
  script:
  - echo 'Running Web app tests...'
  - mstest.exe /testcontainer:.\Web.Tests\bin\Test\MyApp.Web.Tests.dll

test_models:
  stage: test
  script:
  - echo 'Running model tests...'
  - mstest.exe /testcontainer:.\Models.Tests\bin\Test\MyApp.Models.Tests.dll
```

As with a single test project, the calls to MSTest must be marshalled through OpenCover.  However, since there are three test projects, each project will require a separate OpenCover call and each call will generate a separate output file.  In addition, we want to ensure that that the output from one does not get overwritten by the output from another, so we'll need to update the OpenCover calls to specify the output files and directories.  Since we are already caching the project directories, it makes sense to tell OpenCover to store its `results.xml` file in the directory corresponding to the project being covered.  That allows us to generate three distinct output files and make them available for the subsequent reporting stage.

Now, our CI script looks like this:

```yaml
cache:
  key: "%CI_COMMIT_SHA%"
  paths:
    - packages/
    - Persistence/
    - Persistence.Tests/
    - Models/
    - Models/Tests/
    - Web/
    - Web/Tests/

test_all_coverage:
  stage: test
  script:
  - echo 'Running all tests with coverage...'
  - OpenCover.Console.exe -target:"mstest.exe" -targetargs:"/testcontainer:.\Persistence.Tests\bin\Test\MyApp.Persistence.Tests.dll" -filter:"+[MyApp.Persistence*]* -[MyApp.Persistence.Tests]*" -excludebyattribute:*.ExcludeFromCodeCoverageAttribute -register:path32 -returntargetcode -skipautoprops -hideskipped:All -mergebyhash -output:Persistence\results.xml
  - OpenCover.Console.exe -target:"mstest.exe" -targetargs:"/testcontainer:.\Web.Tests\bin\Test\MyApp.Web.Tests.dll" -filter:"+[MyApp.Web*]* -[MyApp.Web.Tests]*" -excludebyattribute:*.ExcludeFromCodeCoverageAttribute -register:path32 -returntargetcode -skipautoprops -hideskipped:All -mergebyhash -output:Web\results.xml
  - OpenCover.Console.exe -target:"mstest.exe" -targetargs:"/testcontainer:.\Models.Tests\bin\Test\MyApp.Models.Tests.dll" -filter:"+[MyApp.Models*]* -[MyApp.Models.Tests]*" -excludebyattribute:*.ExcludeFromCodeCoverageAttribute -register:path32 -returntargetcode -skipautoprops -hideskipped:All -mergebyhash -output:Models\results.xml  
```

One thing to note is that the solution has a root assembly namespace of `MyApp`, which is prepended to the test container names.  This is confirmed by the fact that the filters include `MyApp` in the assembly names.  Note also, however, that the directory structure does not reflect the root assembly name.  Situations such as this may occur in other projects, so it is important to verify assembly and namespace names when writing the CI script.

### Reporting Code Coverage

Now that code coverage has been calculated, we need to aggregate the results and print the metric to the console so that the CI runner can report the coverage.  First, we'll add a `report` stage after the test stage:

```yaml
stages:
  - restore
  - build
  - test
  - report
  - deploy
```

Next, we'll configure the job:

```yaml
report_coverage:
  stage: report
  coverage: '/Line coverage:\s+.*\%/'
  script:
    - echo 'Analyzing code coverage...'
    - ReportGenerator.exe "-reports:Persistence\results.xml;Web\results.xml;Models\results.xml" "-reporttypes:TextSummary" "-targetdir:.\"
    - echo 'Analysis complete.'
    - type Summary.txt
```

The reporting cannot be done during the `test` stage because the jobs in any given stage run in parallel.  Therefore, the reporting job would attempt to report on output files that likely don't exist yet.  However, stages are run sequentially, so we can safely run the `report` stage after the `test` stage and the output files will be available for ReportGenerator to analyze.

# Calculating Coverage Locally

There are a couple of options for calculating code coverage while developing on your local machine.  The first is to run the necessary commands individually and in order to produce a report, whether it be a text summary or full HTML report.  The second is to use a Visual Studio extension to automate the coverage analysis and reporting.

## Running Commands Manually

You may find that you want to run the commands manually from the command prompt, particularly to test that CI script commands run correctly.  If so, there are a couple of tools that you may find useful.  First is the [Open Command Line](https://marketplace.visualstudio.com/items?itemName=MadsKristensen.OpenCommandLine) extension for Visual Studio, which allows you to right-click your solution in the Solution Explorer and open a developer command prompt in the approprate directory.  The advantage of the developer command prompt is that it allows you to call MSBuild and MSTest without having to provide the full path to the executables.

Another useful tool is PowerShell ISE.  This allows you to use PowerShell to perform the build, coverage analysis, and coverage reporting steps all in a single script.  However, PowerShell does not include the Visual Studio developer commands by default. so you must set the appropriate environment variables if you would like to use PowerShell ISE.  See the [How-To on setting up developer commands in PowerShell](how-to-get-developer-commands-in-powershell) for more information.

## Using AxoCover

When developing, AxoCover can be used on your local machine to calculate code coverage.  AxoCover is a [Visual Studio extension](https://marketplace.visualstudio.com/items?itemName=axodox1.AxoCover) that uses OpenCover to calculate code coverage.  AxoCover can also generate ReportGenerator HTML coverage reports.

*Note: AxoCover calculates its own coverage metrics that may differ slightly from those calculated by ReportGenerator.  You will see this discrepancy if you compare AxoCover's results to the export generated by ReportGenerator.  Generally, the difference is not great enough to be a concern.*

### Update `.gitignore`

If you choose to install the AxoCover extension, you will need to update your `.gitignore` file so that AxoCover-generated output isn't committed to the repository.  Add the following lines to your `.gitignore` file:

```
# Exclude AxoCover output
.axoCover/runs/**
.axoCover/reports/**
```

This will allow the AxoCover settings file (`.axoCover/settings.json`) to be preserved in the repository without tracking the output files.

### Update AxoCover Settings

The AxoCover settings should closely mirror the OpenCover attributes from your CI script to ensure that AxoCover's reported coverage is as close as possible to ReportGenerator's reported coverage.  To verify the settings, open the AxoCover window (click the `Tools` menu then click `AxoCover`) and click `Settings`.  The first half of the settings are convenience settings that do not affect code coverage reporting.  However, the second half (starting with the `Coverage` section) are the settings that may need to be changed.  

The following table illustrates which AxoCover settings corresond to [OpenCover arguments](https://github.com/opencover/opencover/wiki/Usage#console-application-usage) and gives guidelines as to how each setting should be set:

| AxoCover Setting | OpenCover Argument | Remark |
| ----- | :-----: | ----- |
| Calculate coverage of each test separately | <code>&#45;coverbytest</code> | AxoCover value should be the same as OpenCover argument value.  This argument usually should not be used. |
| Exclude attributes | <code>&#8209;excludebyattribute</code> | AxoCover value should be the same as OpenCover argument value (typically `*.ExcludeFromCodeCoverageAttribute`).  Add attributes as needed. |
| Exclude files | <code>&#45;excludebyfile</code> | AxoCover value should be the same as OpenCover argument value.  This argument is usually not needed. |
| Exclude directories | <code>&#45;excludebydirs</code> | AxoCover value should be the same as OpenCover argument value.  This argument is usually not needed. |
| Filters | <code>&#45;filter</code> | AxoCover value should be the same as OpenCover argument value.  Value will change per project and depends on assembly names.  Uncheck both "Include solution output only" and "Exclude test assemblies". |
| Merge by hash | <code>&#45;mergebyhash</code> | AxoCover checkbox should be checked when OpenCover argument is provided.  This option is usually checked. |
| Skip auto properties | <code>&#45;skipautoprops</code> | AxoCover checkbox should be checked when OpenCover argument is provided.  This option is usually checked. |

### Run Coverage Analysis

Once the AxoCover settings are properly applied for the solution, you may run the code coverage to get a report.  Open the AxoCover window and click `Tests`.  If no tests are listed, build the solution to allow AxoCover to discover the tests.  You may either click `Run` to simply run the tests or `Cover` to run the tests with coverage.  Once the tests finish running, click `Report` to view the result.  If you would like to view a line-by-line analysis, click `Export` to have AxoCover generate a set of ReportGenerator HTML reports, which will open in your default browser.

*Note: if you make a change to your code, you will need to rebuild your solution before running AxoCover again.  AxoCover uses the last build to determine coverage.*

### Coverage Artifacts

AxoCover tends to build up artifacts (files) as a result of running MSTest, OpenCover, and ReportGenerator.  You see how much storage space AxoCover is using by click the settings button in the AxoCover window and then scrolling to the Output directories section:

![AxoCoverOutput](/uploads/9999f9d23f662e3e02024f9cb4080636/AxoCoverOutput.png)

To view the artifacts themselves (such as to view a ReportGenerator report from a previous run), click the blue arrow button corresponding to the type of artifacts you want to view (reports or runs).  To remove the artifacts, click the broom button corresponding to the type of artifacts you want to remove.

# External Links
1.  [OpenCover](https://github.com/OpenCover/opencover)
1.  [ReportGenerator](http://danielpalme.github.io/ReportGenerator/)
1.  [AxoCover](https://marketplace.visualstudio.com/items?itemName=axodox1.AxoCover)
1.  [Open Command Line](https://marketplace.visualstudio.com/items?itemName=MadsKristensen.OpenCommandLine)
1.  [GitLab CI Documentation](https://docs.gitlab.com/ce/ci/README.html)

## Tags
[[TDD]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=TDDTag)
