# Summary
How to add CMU NuGet repository in Visual Studio.

## Adding CMU NuGet in Visual Studio
To use CMU NuGet repository (https://nuget.cmich.edu), you’ll need to add it as a package source:

1. Open a desired solution in Visual Studio 	
2. Click **Tools**, then **Options**
2. Expand the **NuGet Package Manager** folder node in the navigation pane, then select **Package Sources**
3. Click the button with the green :heavy_plus_sign: in the upper right of the  dialog
4. At the bottom of the dialog, enter a desired name (e.g. *CMU Repository* )  in the **Name** textbox and `https://nuget.cmich.edu/nuget` in the **Source** textbox.
5. Click **Update**, then click **OK**.

Once you’ve added the source, you will be able to select it in the NuGet Package Manager GUI in Visual Studio and browse/install packages.  

*Note: If you're connecting from a location other than campus, you need to use sg3.cmich.edu for your VPN connection.*

## Tags
[[VisualStudio]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=VisualStudioTag)
[[NuGet]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=NuGetTag)