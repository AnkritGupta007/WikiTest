# Summary
The best practices for calling and resolving an Async method (asynchronous code) from code are shown below. Avoiding deadlock where the main thread and the asycn thread are both waiting for each other to return is one of the primary problems we are trying to avoid.

## Best Practices Summarized

### When calling Async from Synchronous
1. **Best Option "Transform Synchronous calling functions to Asynchronous Code All the Way Through"**: use `await` as your call each async method throughout the chain.
2. **Okay Option "Blocking Synchronous Work-around with Thread Pool Tasks"**: use `var result = Task.Run(() => GetAsync(id)).GetAwaiter().GetResult();` to get the real exception if one is thrown instead of the `AggregateException`

### Other Notes  
- Use `ConfigureAwait(false)` for non-".Net Core" when the calling thread isn't needed (most business logic doesn't need to return to the calling thread)
- Avoid `return await ...`
  - When `await` is only used to `return`, return a `Task<MyObject>` instead
  - **Don't** do this inside of `try/catch` or `using()` blocks


## Additional Resources
- https://www.youtube.com/watch?v=My2gAv5Vrkk&t=1420s
- https://channel9.msdn.com/Events/aspConf/aspConf/Async-in-ASP-NET
- https://stackoverflow.com/questions/17284517/is-task-result-the-same-as-getawaiter-getresult
- https://stackoverflow.com/questions/13140523/await-vs-task-wait-deadlock
- https://msdn.microsoft.com/en-us/magazine/mt238404.aspx
- https://msdn.microsoft.com/magazine/jj991977
- https://docs.microsoft.com/en-us/dotnet/csharp/async#key-pieces-to-understand


## Tags
[[Async]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=AsyncTag)
[[C#]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=CSharpTag)