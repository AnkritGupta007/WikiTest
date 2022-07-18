# Summary
This article explains how to resort a test database, such as `IT-WebTestLn` or `IT-DB2k12Dev01` from a nightly production backup, or `.bak` file within SQL Server Management Studio (SSMS).

## Issue with **High Availability Group** on `IT-WebTestLn`
- Note that because `IT-WebTestLn` is a listen for a pair of servers, `IT-DB2k12Test01` and `IT-DB2k12Test02`, linked to fail-over to each other as part of a *High Availability Group* this process will not work. Since it's a more [involved process](https://dba.stackexchange.com/questions/82548/restoring-a-sql-server-2012-database-in-high-availability) it is recommended to put in a [Database Hosting Ticket](https://cmich.teamdynamix.com/TDClient/Requests/ServiceDet?ID=15000) and get Jon Hughes help.

## Steps to Restore Test Database with a Full Copy (nightly) Backup
1. Open SQL Server Management Studio (SSMS) on a Test Database Server, for example `IT-DB2k12Dev01`. **Do not attempt to do this on a production database. Contact *Jon Hughes* on the IT-Applications team for help [hughe1jr@cmich.edu](
mailto:user@example.com)**
2. Identify the test database you intend to restore, for example `FMServiceRequest`
3. Right-click on the Databases name and choose *Tasks > Restore > Database...*
4. In the *Restore Database - {YourDatabaseName}* pop-up switch *Source* radio button to choice *Device:*
5. Click the `[...]` button to select a file from Windows Explorer
6. In the *Select backup devices* pop-up click the *Add* button
7. In the *Locate Backup File it-DB2K12DEV01* pop-up, in the *Backup File location:* paste `\\it-sr1\db-backup$\IT-DB2K12Cluster$Web_AG\{YourDatabaseName}\FULL_COPY_ONLY` , where `{YourDatabaseName}`, for example, might be `FMServiceRequest`
9. Select the desired `.bak` file based on the choices from recent dates
10. Click *OK* a bunch of times on all the open pop-up windows
11. On the top Left go to **Options** as you probably want to turn on [x] *Overwrite the Existing Database (WITH REPLACE)*
12. Note: If you have Queries or Stored Procedures open in SSMS, you will get an error when you try to run the restore.
 - Close the Queries or Stored Procedures you have open and try the restore again

## Updating By Transactional Backup **(Un-tested)**
1. Follow all the steps for the [Full Copy (nightly) Backup](https://code.cmich.edu/App-Doc/wiki/wikis/how-to-restore-a-test-database-from-a-production-backup#steps-to-restore-test-database-with-a-full-copy-nightly-backup) but choose the most recent `.bak` file
2. Follow the steps again but this time in step **7.** choose `\\it-sr1\db-backup$\IT-DB2K12Cluster$Web_AG\{YourDatabaseName}\LOG`
3. Now choose the desired `.trn` file for which is desired by time
4. Click *OK* a bunch of times on all the open pop-up windows
5. Note: If you have Queries or Stored Procedures open in SSMS, you will get an error when you try to run the restore.
 - Close the Queries or Stored Procedures you have open and try the restore again

## Further Reading
- https://docs.microsoft.com/en-us/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms

## Tags
[[Database]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=DatabaseTag)
[[Policy]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=PolicyTag)
