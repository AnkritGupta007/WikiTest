# How to Add a New Database Table using Fluent NHibernate
_Note: This process outlines a code-first approach.  A database first approach may be somewhat different.  It also assumes that the Web.config or App.config files contain the connection string for the database as well as the "Schema" application setting being set to "UPDATE"._
## Create an Entity
1. Create a new Entity in the Persistence project (Persistence.Entities.<i>TableName</i>) 
 1. Make sure the new class is public.
 2. Make the class inherit from EntityBase<_TableName_>.
 3. Make sure all properties are virtual in order for NHibernate to do its stuff.
 4. Add documentation for the class and each property.

```csharp
using System;

namespace Cmich.LmsConnect.Persistence.Entities
{
	/// <summary>
	/// Stores queueing and audit records that pertain to courses.
	/// </summary>
	[ExcludeFromCodeCoverage]
	public class CourseAudit : EntityBase<CourseAudit>
	{
		/// <summary>
		/// The section number used to identify the suite of related courses (labs, lectures, ...)
		/// In SAP, this is the event package number.
		/// </summary>
		public virtual string SectionNumber { get; set; }
...
```

## Create a Mapping
2. Create a new Map file (Persistence.Maps.<i>TableName</i>Map)
 1. Make sure the new class is public.
 2. Make the class inherit from EntityMapBase<_TableName_>.
 3. Create a constructor for the map and register the fields/columns in the table.

```csharp
using Cmich.LmsConnect.Persistence.Entities;

namespace Cmich.LmsConnect.Persistence.Maps
{
	public class CourseAuditMap : EntityMapBase<CourseAudit>
	{
		public CourseAuditMap()
		{
			Map(t => t.SectionNumber);
...
```

## Create a Data Access Object (DAO) Interface
3. Create Data Access Object Interface (Persistence.Dao.I<i>TableName</i>Dao)
 1. Make the class inherit from IRepository<_TableName_, int>.

```csharp
using Cmich.LmsConnect.Persistence.Entities;

namespace Cmich.LmsConnect.Persistence.Dao
{
	public interface ICourseAuditDao : IRepository<CourseAudit, int>
	{
	}
}

```

## Create a Data Access Object (DAO)
4. Create Data Access Object (Persistence.Dao.<i>TableName</i>Dao)
 1. Make the class inherit from IRepository<_TableName_, int>.
 2. Make the class reference its interface: I<i>TableName</i>Dao.

```csharp
using Cmich.LmsConnect.Persistence.Entities;

namespace Cmich.LmsConnect.Persistence.Dao
{
	public class CourseAuditDao: Repository<CourseAudit, int>, ICourseAuditDao
	{
	}
}
```

## _Intermission_
_At this point, building and running the application will create the table in the database (assuming the config (Web or App) file is configured correctly).  It will not, however, be able to store values in the new table until the following steps are performed._

## Update AutoFacConfig.cs 
_(This file can be found in the App_Start folder in the Web project)_
1. Update the AddTypes method in the AutofacConfig.cs file.
 1. Register a new component for the new table using the DAO object created earlier (<i>TableName</i>Dao)
 2. Expose the service defined by the DAO interface (I<i>TableName</i>Dao).

    ```csharp
    private static void AddTypes(ContainerBuilder builder)
    {
    ...
       builder.Register(t=> new CourseAuditDao())
          .OnActivated(e => e.Instance.Session = e.Context.Resolve<ISessionFactory>().OpenSession())
          .InstancePerLifetimeScope()
          .As<ICourseAuditDao>();
    ...
    ```

2. Add an instance of the I<i>TableName</i>Dao object in each class that needs to interact with the new table.

## Tags
[[Database]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=DatabaseTag)
[[NHibernate]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=NHibernateTag)
[[AutoFac]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=AutoFacTag)
