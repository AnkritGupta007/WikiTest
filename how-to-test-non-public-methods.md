# How to Test Non-Public Methods

## Summary

This page discusses the conflict between test-driven development and information hiding, briefly explains some of the solutions to overcome that conflict, and then provides a guide on implementing one of those solutions.  Please note that the techniques outlined in this page should be applied mainly to existing applications.  New applications should be developed to have an architecture that promotes full test coverage whenever possible.

## Background

Non-public methods highlight a dichotomy between test-driven development and abstraction through information hiding/encapsulation in object-oriented programming.  Testing a method requires that it be accessible to the testing assembly, but non-public methods by definition are accessible only to the assemblies in which they are defined.  In addition, non-public methods are generally made non-public because they represent the internal workings of a class that should not be exposed.  

This problem is especially prevalent in legacy applications that were not developed with testing in mind.  Although new applications should be developed using a test-driven development process, we often want add testing around legacy applications to ensure that changes do not break existing functionality.  Thus arises the question of how to test non-public methods.

## Internal Methods for Testability

There are a couple of solutions for testing non-public methods, but they have their drawbacks:

 - Make the methods public, and potentially expose internal class details that should be hidden.
 - Use reflection to test the methods and accept the overhead (increased complexity/reduced maintainability) that goes along with it.

Internal methods provide an alternate solution that represents a good trade-off between public methods and reflection.  Instead of publicizing non-public methods, we can declare the methods as internal and then expose internal methods to the testing assembly.  This adds a little bit of overhead in that it requires extra configuration, but the setup happens only once per testing project.  After configuration, the developer need only to create the tests; the non-public methods will be visible as though they were public.  In addition, we can control who has access to those internal methods, since referencing assemblies do not have access by default.

## Configuration

The initial configuration requires that the referencing assembly (i.e. the testing project) be signed.  Signing involves creating a strong-name key file, updating the configuration, and then rebuilding the project.  Once signed, the testing assembly's public key can then be included in the project being tested so that it will expose its internal methods to the testing assembly.

## Walkthrough

By way of example, `MyProject` and `MyProject.Tests.Unit`, will be used, where 

- `MyProject` is a C# project containing the classes and methods to be tested
- `MyProject.Tests.Unit` is a C# unit testing project
- Both projects are contained in a single solution defined by the `MyProject.sln` file
- The projects are arranged in the standard folder hierarchy created by Visual Studio (the solution files in the solution root directory and each project in its own directory)

### Sign the testing assembly

To sign the testing assembly, you must first have a strong-name key file:
1.  Open the Developer Command Prompt for your version of Visual Studio (e.g. Start > Visual Studio 2015 > Developer Command Prompt for VS2015).
2.  Navigate to your solution's root directory.
3.  Type `sn -k [SolutionName].snk` where `[SolutionName]` is the name of your solution (see example below), and hit Enter.

```
C:\Users\User\Documents\VS Solutions\MyProject> sn -k MyProject.snk 

Microsoft (R) .NET Framework Strong Name Utility  Version 4.0.30319.0
Copyright (c) Microsoft Corporation.  All rights reserved.

Key pair written to MyProject.snk

C:\Users\User\Documents\VS Solutions\MyProject>
```

After creating the strong-name key file, sign the assembly:
1.  In Visual Studio, open the properties for the testing assembly and navigate to the Signing tab.
2.  Check the "Sign the assembly" checkbox.
3.  Under "Choose a strong name key file", select the file you just created.
4.  Save the project and build it, making note of the active build configuration, e.g., Debug.

### Get the testing assembly public key

In order to expose the internal methods in the assembly being tested, you must know the public keys of the assemblies that access them.  Return to the Developer Command Prompt for Visual Studio:

1.  Navigate to the build output directory for the active build configuration (e.g. `bin\Debug`).  
2.  Type `sn -Tp [ProjectName].dll` where `[ProjectName]` is the name of the referencing assembly (see example below), and hit Enter.

    ```
    C:\Users\User\Documents\VS Solutions\MyProject\MyProject.Tests.Unit\bin\Debug> sn -Tp MyProject.Tests.Unit.dll 

    Microsoft (R) .NET Framework Strong Name Utility  Version 4.0.30319.0
    Copyright (c) Microsoft Corporation.  All rights reserved.

    Public key (hash algorithm: sha1):
    0024000004800000940000000602000000240000525341310004000001000100edd25698263515
    09103c1c87e5d92d87e236326a4ff6be26a4bd5e2cf7af751d1e6072e20fed25e8d10d6e292cfd
    212581ccb3243fa3b460048e3c299408c0d08de9500887beef8159de945f6958db4c1e251454e3
    e3eb25be0512b74a9cfc7b159c2f88bc93672456192a59372e86497a096654ffd7b428d92d652f
    936622b5

    Public key token is 8ca50422a4944148

    C:\Users\User\Documents\VS Solutions\MyProject\MyProject.Tests.Unit\bin\Debug>
    ```
3.  Copy the public key (*not* the public key token) to use in the project being tested. Highlight the text and hit Enter to copy it.

### Expose internals to the testing assembly

Now that you have signed the referencing assembly and you have its public key, you must configure the project to allow the testing assembly to access its internals.  

1.  In the Solution Explorer, on `MyProject` expand Properties.
2.  Double-click `AssemblyInfo.cs` to open it.
3.  Add an `[assembly: InternalsVisibleTo([ReferencingProject], PublicKey=[Key])]` attribute to the file (see example below) where `[Referencing Project]` is the testing project and `[Key]` is the public key from the previous section.

```c#
// Allow unit testing project to access internal methods.
[assembly: InternalsVisibleTo("MyProject.Tests.Unit,PublicKey=" +
  "0024000004800000940000000602000000240000525341310004000001000100edd25698263515" +
  "09103c1c87e5d92d87e236326a4ff6be26a4bd5e2cf7af751d1e6072e20fed25e8d10d6e292cfd" +
  "212581ccb3243fa3b460048e3c299408c0d08de9500887beef8159de945f6958db4c1e251454e3" +
  "e3eb25be0512b74a9cfc7b159c2f88bc93672456192a59372e86497a096654ffd7b428d92d652f" +
  "936622b5")]
```

The solution is now configured for non-public method testing.  Any method with the `internal` access modifier will appear be visible to the testing project.

## References

[1]  Y. Cui, ".Net Tips – using InternalsVisibleTo attribute to help testing non-public methods", *theburningmonk.com*, 01 May 2010, [http://theburningmonk.com/2010/05/net-tips-using-internalsvisibleto-attribute-to-help-testing-non-public-methods/](http://theburningmonk.com/2010/05/net-tips-using-internalsvisibleto-attribute-to-help-testing-non-public-methods/).

[2]  Microsoft Corporation, "Create a Strong-Name Key File", *Microsoft Developer Network*, 2014, [https://msdn.microsoft.com/en-us/library/dd788548.aspx](https://msdn.microsoft.com/en-us/library/dd788548.aspx).

[3]  "How to declare a friend assembly?", *Stack Overflow*, 14 Jul 2009, [http://stackoverflow.com/questions/1123683/how-to-declare-a-friend-assembly](http://stackoverflow.com/questions/1123683/how-to-declare-a-friend-assembly).

## Tags
[[TDD]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=TDDTag)
[[UnitTesting]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=UnitTestingTag)