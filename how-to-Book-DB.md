# Book DB (WIP)
In case of tickets regarding the "Book DB": this is an Access front-end to certain tables used primarily by Marnie Roestel as of the time of writing this page. Marnie is the main contact for testing it and likely the one who will have submitted the ticket anyway. Other important people in case of needing to contact someone are:
- Andrew Wittbrodt: Developed the tables/views underlying the front-end
- Jason Kiley: Contact person about the actual Access database, access to it, etc.

## DB
Servers:
- Testing Server: `it-sql17-t-db1`
- Prod Server: `it-sql17-p-ocl`

Tables used:
- mis.dbo.CourseReserves
- mis.dbo.FC_BookLists_For_CMU_Online
- mis.dbo.FC_BookRequiredMaterials_For_CMU_Online

Views used:
- mis.dbo.VIEW_COURSE_RESERVES
- mis.dbo.VIEW_FC_BookLists_For_CMU_Online_filtered
- mis.dbo.VIEW_MBS_Book_List
- mis.dbo.VIEW_MBS_Book_List_Inclusive

## Testing
Personal testing can be done by accessing the tables and views directly, since the Access front-end doesn't seem to do anything additional with the data. Marnie has access to a testing copy of the Access front-end in question and can test to verify that what's seen is what she expects to see, allowing for differences in data between prod and testing.

## Tags
[[Database]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=DatabaseTag)