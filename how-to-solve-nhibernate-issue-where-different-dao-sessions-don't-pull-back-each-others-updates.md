# Summary
This is to address a tricky gotcha with *nHibernate*. In cases where a parent object is also saving child objects such as in this [AgencyAddressService](https://code.cmich.edu/IT-AppDevelopment/CustomApplications/Agreements/blob/master/Web/Services/AgencyAddressService.cs) you need to use 

```c#
MyObjDao.Save(myObj); 
MyObj.Flush(); 
MyObj.Session.Clear(); // skipping this step will result in other sessions having stale data.
```

## Further reading
- https://stackoverflow.com/questions/4727307/nhibernate-updates-in-one-session-dont-get-reflected-in-another-open-session#comment91614809_4727383

## Tags
[[NHibernate]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=NHibernateTag)
