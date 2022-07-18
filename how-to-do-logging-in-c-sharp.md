# Summary
This page provides a walkthough for setting up logging in C# projects using Apache log4net.  The walkthrough gives instructions for basic setup and for enterprise setup using either Autofac or Microsoft Unity IoC.  The page also includes an anti-pattern for quick, simple logging.

# Starting Steps
Before configuring the logging, you must first add a reference to the log4net library, which is available as a NuGet package.  In your project, install the log4net NuGet package published by The Apache Software Foundation.

## Configuration File
Once the library reference is added, configure the rolling log file appender in the Web.config or App.config file.  Add the following configuration to the `<configuration>` section of the configuration file:

```xml
<!-- put `<configSections>` chunk as first thing in `<configuration>` section -->
  <configSections>
    <section name="log4net" type="log4net.Config.Log4NetConfigurationSectionHandler, 
      log4net" />
  </configSections>
  <log4net debug="false">
    <appender name="RollingLogFileAppender" type="log4net.Appender.RollingFileAppender">
      <file value="MyApplication.log" />
      <appendToFile value="true" />
      <rollingStyle value="Size" />
      <maxSizeRollBackups value="10" />
      <maximumFileSize value="10MB" />
      <staticLogFileName value="true" />
      <layout type="log4net.Layout.PatternLayout">
        <conversionPattern value="%-5level %date %-30.30logger{1} %message%newline" />
      </layout>
    </appender>
    <root>
      <level value="DEBUG" />
      <appender-ref ref="RollingLogFileAppender" />
    </root>
  </log4net>
```

You may wish to change the following elements to customize how your application performs its logging:

| Element | Purpose | 
| ---------- | ---------- |
| `<file [...] />` | Specifies the file name where the log entries will be stored. |
| `<maxSizeRollBackups [...] />` | Sets the number of backup log files to retain. |
| `<maximumFileSize [...] />` | Sets the maximum file size for the main log file and each backup |
| `<conversionPattern [...] />` | Specifies how each log entry will appear.  More information on pattern specifiers is available on the documentation page (see references below). |
| `<level [...] />` | Specifies the message levels that will allow appending to the log file.  Messages with levels lower than the specified value will be ignored. |

**A note on log levels:**  log4net log levels are, in increasing priority, `ALL`, `DEBUG`, `INFO`, `WARN`, `ERROR`, `FATAL`, and `OFF`.  When the root logger is given a log level, any logging messages with a lower-priority level are ignored.  This becomes useful when we want to capture more messages in testing and debugging than in production.  Web.config transforms can be used to specify different logging levels for different environments.

## Loading the configuration
Once the configuration is specified in the Web.config or App.config file, you must instruct log4net to load the configuration.  Add the following line to your `Global.asax.cs` file's `Application_Start()` method:

```c#
log4net.Config.XmlConfigurator.Configure();
```

For a more enterprisey solution, create a `LoggingConfig.cs` file in your project's `App_Start` folder and define the following class:

```c#
/// <summary>
/// Handles configuration startup tasks for the logging service.
/// </summary>
public static class LoggingConfig
{
    /// <summary>
    /// Prompts the logging service to load its configuration.
    /// </summary>
    public static void Configure()
    {
        log4net.Config.XmlConfigurator.Configure();
    }
}
```

Then, in your `Global.asax` file, call the `Configure` method:

```c#
LoggingConfig.Configure();
```

# Basic Logging with log4net
To use log4net in your application, you need to use the `LogManager` object to create a new logger instance.  This requires passing in the type for the class that will be creating log messages as log4net can use reflection to determine the method that is performing the logging.  Populating a class-level `ILog` variable is the easiest way to accomplish the setup in each class:

```c#
public class MyClass
{
  private ILog Logger;

  public MyClass()
  {
     Logger = LogManager.GetLogger(typeof(MyClass));
  }
}
```

Once the logger is created, you can call the appropriate method (`Debug()`, `Info()`, `Warn()`, etc.) to generate a log message with a corresponding logging level.  For example,

```c#
Logger.Warn("This is my very first warning message!");
```

will generate this entry in the log file as long as the configuration allows for `WARN` messages:

```
WARN  2017-04-25 14:55:19,336 MyClass       This is my very first warning message!
```

# Enterprise Logging with log4net
When using dependency injection by way of an IoC container, there is a little extra overhead involved in the configuration since log4net requires the data type for the object that is generating the log entry (i.e., the calling type).  The steps involved vary, depending on the IoC container being used.

## Configuring Autofac
Autofac requires a custom module to handle the type discovery for the calling class.  First, create a `LoggingModule.cs` file and define the logging module class:

```c#
    /// <summary>
    /// Resolves the log4net ILog dependency.
    /// </summary>
    public class LoggingModule : Autofac.Module
    {
        /// <summary>
        /// Checks the instance for an ILog property and injects a new logger into the 
        /// property if found.
        /// </summary>
        /// <param name="instance">The instance to check.</param>
        private static void InjectLoggerProperties(object instance)
        {
            var instanceType = instance.GetType();
            var properties = instanceType
                .GetProperties(BindingFlags.Public | BindingFlags.Instance)
                .Where(p => p.PropertyType == typeof(ILog) && p.CanWrite &&
                p.GetIndexParameters().Length == 0);

            foreach (var propToSet in properties)
            {
                propToSet.SetValue(instance, LogManager.GetLogger(instanceType), null);
            }
        }

        /// <summary>
        /// Handles the component's Prepare event.
        /// </summary>
        /// <param name="sender">The object instance calling the method.</param>
        /// <param name="e">Arguments associated with the event.</param>
        private static void OnComponentPreparing(object sender, PreparingEventArgs e)
        {
            e.Parameters = e.Parameters.Union(
                new[]
                {
                    new ResolvedParameter(
                        (p, i) => p.ParameterType == typeof(ILog),
                        (p, i) => LogManager.GetLogger(p.Member.DeclaringType)
                    ),
                });
        }

        /// <inheritdoc />
        protected override void AttachToComponentRegistration(IComponentRegistry 
            componentRegistry, IComponentRegistration registration)
        {
            registration.Preparing += OnComponentPreparing;
            registration.Activated += (sender, e) => InjectLoggerProperties(e.Instance);
        }
    }
```

Next, update your Autofac configuration to include the new `LoggingModule`.

```c#
public static class AutofacConfig
{
    /// <summary>
    /// Handles dependency injection and manages lifetimes for resolved components.
    /// </summary>
    public static IContainer Container { get; set; }

    /// <summary>
    /// Builds the IoC container.
    /// </summary>
    public static void RegisterAutofac()
    {
        // Create a new container builder object.
        var builder = new ContainerBuilder();
        
        // Register the log4net logging module.
        builder.RegisterModule(new LoggingModule());
        
        // Set the IoC container.
        Container = builder.Build();
    }
```

The logging module will extend Autofac to automatically resolve the `ILog` dependencies with logger instances containing the correct calling type.  You need only to add an `ILog` property to your dependent class.

```c#
public class MyLoggableClass
{
    public ILog Logger { get; set; }

    public MyLoggableClass()
    {
        // Do stuff here.
    }

    // Add more methods here.
}
```

## Configuring Microsoft Unity
Microsoft Unity requires a set of extensions, strategies, and policies in order to inject log4net logger instances.  First, create the following classes and interface:

`BuildTracking`:
```c#
/// <summary>
/// Unity container extension that tracks dependency builds.
/// </summary>
public class BuildTracking : UnityContainerExtension
{
    /// <summary>
    /// Adds the extended functionality to the container.
    /// </summary>
    protected override void Initialize()
    {
        Context.Strategies.AddNew<BuildTrackingStrategy>(UnityBuildStage.TypeMapping);
    }

    /// <summary>
    /// Gets the build tracking policy for the builder context.
    /// </summary>
    /// <param name="context">The context from which to retrieve the policy.</param>
    /// <returns>The requested policy.</returns>
    public static IBuildTrackingPolicy GetPolicy(IBuilderContext context)
    {
        return context.Policies.Get<IBuildTrackingPolicy>(context.BuildKey, true);
    }

    /// <summary>
    /// Sets the build tracking policy for the builder context.
    /// </summary>
    /// <param name="context">The context in which to set the policy.</param>
    /// <returns>The policy that was set.</returns>
    public static IBuildTrackingPolicy SetPolicy(IBuilderContext context)
    {
        IBuildTrackingPolicy policy = new BuildTrackingPolicy();
        context.Policies.SetDefault(policy);
        return policy;
    }
}
```

`BuildTrackingPolicy`:
```c#
/// <summary>
/// Represents a build tracking policy.
/// </summary>
public class BuildTrackingPolicy : IBuildTrackingPolicy
{
    /// <summary>
    /// Creates a new instance of the class.
    /// </summary>
    public BuildTrackingPolicy()
    {
        BuildKeys = new Stack<object>();
    }

    /// <inheritdoc />
    public Stack<object> BuildKeys { get; }
}
```

`BuildTrackingStrategy`:
```c#
/// <summary>
/// Represents a strategy for tracking builds.
/// </summary>
public class BuildTrackingStrategy : BuilderStrategy
{
    /// <inheritdoc />
    public override void PreBuildUp(IBuilderContext context)
    {
        var policy = BuildTracking.GetPolicy(context) ?? BuildTracking.SetPolicy(context);
        policy.BuildKeys.Push(context.BuildKey);
    }

    /// <inheritdoc />
    public override void PostBuildUp(IBuilderContext context)
    {
        var policy = BuildTracking.GetPolicy(context);

        if (policy != null && policy.BuildKeys.Count > 0)
        {
            policy.BuildKeys.Pop();
        }
    }
}
```

`IBuildTrackingPolicy`:
```c#
/// <summary>
/// Provides an interface to a build tracking policy.
/// </summary>
public interface IBuildTrackingPolicy : IBuilderPolicy
{
    /// <summary>
    /// Gets the set of keys used to build the object.
    /// </summary>
    Stack<object> BuildKeys { get; }
}
```

`LogBuildPlanPolicy`:
```c#
/// <summary>
/// Provides functionality for resolving a logging service dependency.
/// </summary>
public class LogBuildPlanPolicy : IBuildPlanPolicy
{
    /// <summary>
    /// Creates a new instance of the logging service builder.
    /// </summary>
    /// <param name="logType">The type for object that will use the logging service.</param>
    public LogBuildPlanPolicy(Type logType)
    {
        LogType = logType;
    }

    /// <summary>
    /// Gets the dependent class type.
    /// </summary>
    public Type LogType { get; }

    /// <summary>
    /// Builds the logging service instance in the secified context.
    /// </summary>
    /// <param name="context">The context for which to create the logging instance.</param>
    public void BuildUp(IBuilderContext context)
    {
        if (context.Existing == null)
        {
            var log = LogManager.GetLogger(LogType);
            context.Existing = log;
        }
    }
}
```

`LogCreation`:
```c#
/// <summary>
/// Extends unity to automatically create a logger instance for the appropriate type.
/// </summary>
public class LogCreation : UnityContainerExtension
{
    /// <inheritdoc />
    protected override void Initialize()
    {
        Context.Strategies.AddNew<LogCreationStrategy>(UnityBuildStage.PreCreation);
    }
}
```

`LogCreationStrategy`:
```c#
/// <summary>
/// Represents a strategy for creating a logging service instance.
/// </summary>
public class LogCreationStrategy : BuilderStrategy
{
    /// <summary>
    /// Gets a value indicating if the build policy is set.
    /// </summary>
    public bool IsPolicySet { get; private set; }

    /// <inheritdoc />
    public override void PreBuildUp(IBuilderContext context)
    {
        Type typeToBuild = context.BuildKey.Type;

        if (!typeof(ILog).Equals(typeToBuild)) return;
        if (context.Policies.Get<IBuildPlanPolicy>(context.BuildKey) != null) return;

        var typeForLog = GetLogType(context);
        var policy = new LogBuildPlanPolicy(typeForLog);

        context.Policies.Set<IBuildPlanPolicy>(policy, context.BuildKey);
        IsPolicySet = true;
    }

    /// <inheritdoc />
    public override void PostBuildUp(IBuilderContext context)
    {
        if (!IsPolicySet) return;

        context.Policies.Clear<IBuildPlanPolicy>(context.BuildKey);
        IsPolicySet = false;
    }
    /// <summary>
    /// Gets the type for the class that will use the logging service instance.
    /// </summary>
    /// <param name="context">The current builder context.</param>
    /// <returns>The type of the dependent class.</returns>
    private static Type GetLogType(IBuilderContext context)
    {
        var logType = typeof(ILog);
        var buildTrackingPolicy = BuildTracking.GetPolicy(context);

        if (buildTrackingPolicy != null && buildTrackingPolicy.BuildKeys.Count >= 2)
        {
            logType = ((NamedTypeBuildKey) buildTrackingPolicy.BuildKeys.ElementAt(1)).Type;
        }
        else
        {
            var stackTrace = new StackTrace();

            for (var i = 2; i < stackTrace.FrameCount; i++)
            {
                var frame = stackTrace.GetFrame(i);
                logType = frame.GetMethod().DeclaringType;

                if (logType != null && !logType.FullName.StartsWith("Microsoft.Practices")) break;
            }
        }
        
        return logType;
    }
}
```

Once the necessary classes and interface are created, update the Unity configuration class to include the extension objects:

```c#
var container = new UnityContainer();

container
    .AddNewExtension<BuildTracking>()
    .AddNewExtension<LogCreation>();

// Remaining configuration code
```

The Unity extensions will automatically resolve the `ILog` dependencies with logger instances containing the correct calling type.  You need only to add an `ILog` property to your dependent class and flag it with a `[Dependency]` attribute.

```c#
public class MyLoggableClass
{
    [Dependency]
    public ILog Logger { get; set; }

    public MyLoggableClass()
    {
        // Do stuff here.
    }

    // Add more methods here.
}
```

# Quick and Dirty Logging in C# #
Here is an example of writing out C# objects of interest to files to `/App_Data` folder. This works for "View in Browser" option in Visual Studio as well as full on debugging locally or on a Remote Windows Server.

```c#
if (ConfigurationManager.AppSettings["ApplicationMode"] != "Production")
{
  var path =
    HostingEnvironment.MapPath("~/App_Data/UpdateCourseInfo/" +
                               course.DepartmentCode + course.CourseId +
                               DateTime.Now.ToString("yyyyMMddHHmmssfff") + ".json");
  System.IO.Directory.CreateDirectory(System.IO.Path.GetDirectoryName(path));
  var content = Newtonsoft.Json.JsonConvert.SerializeObject(course,       Newtonsoft.Json.Formatting.Indented);
  System.IO.File.WriteAllText(path, content);
}
```

# References
[1]  *Apache log4net Manual - Introduction*, Apache Software Foundation, Wakefield, MA [Online].  Available: [https://logging.apache.org/log4net/release/manual/introduction.html](https://logging.apache.org/log4net/release/manual/introduction.html)

[2]  *log4net Integration Module*, Autofac [Online].  Available: [http://docs.autofac.org/en/latest/examples/log4net.html](http://docs.autofac.org/en/latest/examples/log4net.html)

[3]  "Just some ideas", *patterns &amp; practices - Unity*, CodePlex [Online].  Available:  [http://unity.codeplex.com/discussions/203744](http://unity.codeplex.com/discussions/203744)

## Tags
[[C#]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=CSharpTag)
[[Logging]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=LoggingTag)
[[Autofac]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=AutofacTag)
