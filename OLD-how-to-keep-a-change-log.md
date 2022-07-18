# Why keep a changelog?
Keeping a changelog makes it easier for users and contributors to see precisely what notable changes have been made between each release (or version) of the project. This meant for people. Whether consumers or developers, the end users of software are human beings who care about what's in the software. When the software changes, people want to know why and how.

# Adding a new changelog
1. Click **Add Changelog** from the main project page *(Skip to step* ***3.*** *)* **OR**

![add-change-log-button](/uploads/bdf47f49259854f759c3f895ea7afe7b/add-change-log-button.png)

1. Go to the **Files** section of your project in GitLab
2. Click the *plus sign* beside the *MyProject /* **[ + ]**  Plus sign and select New File
3. Enter the new File name as CHANGELOG.md (`.md` is for Markdown)
4. Paste in this [base template](how-to-keep-a-change-log#base-template) (below) and begin editing
5. Reference [Types of changes](https://keepachangelog.com/en/1.0.0/#types) and use them as sub-headers to group your changes under such items as `Added`, `Changed`, `Deprecated` `Security`,  `Removed`, `Fixed` and `Security`
6. You are all done! If your project is becoming a NuGet package for others to consume, continue on to [Steps to Make a Tag]
(how-to-keep-a-change-log#steps-to-make-a-tag-only-applies-to-cmich-nuget-packaged-items-like-the-core-api)

# Base Template
```md
# Change Log
All notable changes to this project will be documented in this file.

## Unreleased

> None at the moment

## **1.0.1** - yyyy-mm-dd
### Changed
- [Change ID: 2982419](https://cmich.teamdynamix.com/TDNext/Apps/393/Tickets/TicketDet.aspx?TicketID=2982419) This is an example link to a ticket.
- Now using CMich Projects not the NuGet DLLs and auto-deploy since they has security issues

## **1.0.0** - yyyy-mm-dd
### Added
- Initial release of this application
 
Format specified by [Keep a CHANGELOG](https://keepachangelog.com)
and this project adheres to [Semantic Versioning](http://semver.org/).
```

# [LEGACY] Pre 2017 Changelog
## ​CSS

### 1.5.1

*   <span style="line-height: 22.4px;"><span style="line-height: 1.6;">Added sr-only-tableCaption class to address table caption screen reader issue.​</span></span>
*   <span style="line-height: 22.4px;"><span style="line-height: 1.6;">.Added styles for multiselect  
    </span></span>

### 1.5.0

*   <span style="line-height: 1.6;"></span><span style="line-height: 1.6; display: inline;">Added .maroon class.</span>
*   <span style="line-height: 1.6; display: inline;"></span>Added .maroon class styles for anchors.
*   Added styles for the Testing Information switcher
*   Added the .testMode class to define the test mode background  

### 1.4.1

*   <span style="line-height: 1.6;"></span><span style="line-height: 1.6; display: inline;">Added media query at 768px and less to remove 15px gutter outside of content area container.</span>
*   <span style="line-height: 1.6; display: inline;">Removed 20px bottom padding on collapsed sidebar navigation.</span>

## JS

### 1.1.0

*   Added code for the new Testing Information switcher
*   Added code to change the background to display "Test" if the Testing Information switcher is present  

*   Added code for RequiredIf validation
*   Added code for overall validation summary to be screen reader accessible

### 1.0.0

*   Added code to toggle "aria-expanded" upon click of ".navbar-toggle"
*   Added code for Validation Summary

## Tags
[[Development]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=DevelopmentTag)
[[FrontEnd]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=FrontEndTag)
[[Template]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=TemplateTag)
[[OldWiki]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=OldWikiTag)
[[Logging]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=LoggingTag)
[[Git]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=GitTag)
