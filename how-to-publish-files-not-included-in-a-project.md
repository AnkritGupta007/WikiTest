# Summary
How To ​Publish Files Not Included In A .Net Project by modifying the Test.pubxml or Staging.pubxml

In other words, **VS Web Publish: How to include files outside of the project to be published**

## Practical Example
It did end up working to modify my `Test.pubxml` to this, which fires the `CustomCollectFiles` target:

```xml
<?xml version="1.0" encoding="utf-8"?>
<!--
This file is used by the publish/package process of your Web project. You can customize the behavior of this process
by editing this MSBuild file. In order to learn more about this please visit 
   http://go.microsoft.com/fwlink/?LinkID=208121. 
-->
<Project ToolsVersion="4.0" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
   <PropertyGroup>
     <WebPublishMethod>FileSystem</WebPublishMethod>
     <LastUsedBuildConfiguration>Testing</LastUsedBuildConfiguration>
     <LastUsedPlatform>Any CPU</LastUsedPlatform>
     <SiteUrlToLaunchAfterPublish />
     <LaunchSiteAfterPublish>True</LaunchSiteAfterPublish>
     <ExcludeApp_Data>False</ExcludeApp_Data>
     <publishUrl>\\it-resweb01\d$\inetpub\apps\SearchRegister</publishUrl>
     <DeleteExistingFiles>False</DeleteExistingFiles>
     <!-- START ADDED CODE  BLOCK 1 -->
     <!-- This is taking advantage of the hook to pull in files not included in the project -->
     <PipelineCollectFilesPhaseDependsOn>CustomCollectFiles;         ;</PipelineCollectFilesPhaseDependsOn>
     <!-- END ADDED CODE BLOCK 1 -->
   </PropertyGroup>
   <!-- START ADDED CODE  BLOCK 2 -->
   <!-- In this project the csr.min.js file in a minified file generated from several generated js files from
    typescript files. If this file is included in the project, saving changes to the typescript files 
    causes visual studio 2015 to crash and become non responsive.
    -->
   <Target Name="CustomCollectFiles">
     <Message Text="Inside of CustomCollectFiles" Importance="high" />
     <ItemGroup> 
       <_CustomFiles Include="$(MSBuildThisFileDirectory)..\..\app\csr.min.js" /> 
         <FilesForPackagingFromProject Include="%(_CustomFiles.Identity)">
           <DestinationRelativePath>app\%(RecursiveDir)%(Filename)%(Extension)</DestinationRelativePath>
       </FilesForPackagingFromProject>
     </ItemGroup>
   </Target>
   <!-- END ADDED CODE BLOCK 2 -->
</Project>
```

## Tags
[[.NET]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=DotNETTag)
[[Deployment]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=DeploymentTag)
