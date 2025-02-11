# Obaki.LocalStorageCache
[![NuGet](https://img.shields.io/nuget/v/Obaki.LocalStorageCache.svg)](https://www.nuget.org/packages/Obaki.LocalStorageCache)
[![NuGet Downloads](https://img.shields.io/nuget/dt/Obaki.LocalStorageCache?logo=nuget)](https://www.nuget.org/packages/Obaki.LocalStorageCache)

> **⚠️ Hey there! Important Update:**
>
> I recommend switching to this new library instead: [browser-cache-extensions](https://github.com/jjosh102/browser-cache-extensions).  
> It's a simple extension on local storage and cuts out the extra  wrapper from the old library.


This is a simple library that allows you to easily cache data in the browser's local storage. It provides a simple API for storing and retrieving data  based on a specified time-to-live (TTL). The library make use of [Blazored LocalStorage](https://github.com/Blazored/LocalStorage) for storing cache data.

Overall, Obaki.LocalStorageCache is a simple and easy-to-use library that can help you improve the performance of your web application by caching data locally in the browser.

## Installing

To install the package add the following line inside your csproj file with the latest version.

```
<PackageReference Include="BrowserCache.Extensions" Version="x.x.x" />
```

An alternative is to install via the .NET CLI with the following command:

```
dotnet add package BrowserCache.Extensions
```

For more information you can check the [nuget package](https://www.nuget.org/packages/BrowserCache.Extensions).

## Setup
Register the needed services in your Program.cs file as **Scoped**

```c#
public void ConfigureServices(IServiceCollection services)
{
    services.AddLocalStorageCacheAsScoped();
}
``` 

Or as **Singleton**

```c#
public void ConfigureServices(IServiceCollection services)
{
    services.AddLocalStorageCacheAsSingleton();
}
```
## Usage 
**Asynchronous(Non-Blocking)**
```c#
using Obaki.LocalStorageCache;

public class TestAsync {
  private readonly ILocalStorageCache _localStorageCache;
  
  public TestAsync(ILocalStorageCache localStorageCache) {
    _localStorageCache = localStorageCache;
  }

  public async Task<TCacheData> GetDataAsync() {
    var cache = await _localStorageCache.GetOrCreateCacheAsync(
      Key, //Define Key
      TimeSpan.FromHours(1), //TTL
       async () =>
         return await GetNewData<TCacheData>(); //Refresh cache data.
      });
      
    return cache ?? default;
  }
}
```
**Synchronous(Blocking)**
```c#
using Obaki.LocalStorageCache;

public class TestSync {
  private readonly ILocalStorageCacheSync _localStorageCacheSync;
  
  public TestSync(ILocalStorageCacheSync localStorageCacheSync) {
    _localStorageCacheSync = localStorageCacheSync;
  }

  public TCacheData GetDataSync() {
    var cache = _localStorageCacheSync.GetOrCreateCache(
      Key, //Define Key
      TimeSpan.FromHours(1), //TTL
        () =>
         return GetNewData<TCacheData>(); //Refresh cache data.
      });
      
    return cache ?? default;
  }
}
```
## Disclaimer
Use only this library for caching non sensitive data.
If you are working with highly private and confidential data , you should not be storing this data in your client's browser.
# License
MIT License
## Star History




