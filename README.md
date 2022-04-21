## Static Blazor WASM Twitter "Public Client" Single Page App (SPA) sample

#### Config:
* L2T v6.14.0
* .NET 7 preview 3 SDK

When adding the package `LinqToTwitter.AspNet` (6.14.0) you'll get the build errors below when you try to compile it.

Adding the package `LinqToTwitter` works, the solution compiles without any problems but I believe for this ASP.NET Core Blazor WASM app `LinqToTwitter.AspNet`is needed? But I'm not sure. I don't know the exact difference between the two packages.

### To Reproduce

* You'll need [.NET SDK 7 Preview 3](https://dotnet.microsoft.com/en-us/download/visual-studio-sdks) 
* And [Visual Studio Preview](https://visualstudio.microsoft.com/vs/preview/)
* Download this repo
* Compile it

### Build Errors

`LT2-PackageTest\obj\Debug\net7.0\LT2-PackageTest.MvcApplicationPartsAssemblyInfo.cs(14,54,14,78): error CS0234: The type or namespace name 'ApplicationPartAttributeAttribute' does not exist in the namespace 'Microsoft.AspNetCore.Mvc.ApplicationParts' (are you missing an assembly reference?)`

`LT2-PackageTest\obj\Debug\net7.0\LT2-PackageTest.MvcApplicationPartsAssemblyInfo.cs(14,54,14,78): error CS0234: The type or namespace name 'ApplicationPartAttribute' does not exist in the namespace 'Microsoft.AspNetCore.Mvc.ApplicationParts' (are you missing an assembly reference?)`

### LT2-PackageTest.csproj
```
<Project Sdk="Microsoft.NET.Sdk.BlazorWebAssembly">
  <PropertyGroup>
    <TargetFramework>net7.0</TargetFramework>
    <Nullable>enable</Nullable>
    <ImplicitUsings>enable</ImplicitUsings>
    <LangVersion>preview</LangVersion>
  </PropertyGroup>

  <ItemGroup>
    <PackageReference Include="LinqToTwitter.AspNet" Version="6.14.0" />
    <PackageReference Include="Microsoft.AspNetCore.Components.WebAssembly" Version="7.0.0-preview.3.22178.4" />
    <PackageReference Include="Microsoft.AspNetCore.Components.WebAssembly.DevServer" Version="7.0.0-preview.3.22178.4" PrivateAssets="all" />
  </ItemGroup>
</Project>
```

### Program.cs

```
using LT2_PackageTest;
using Microsoft.AspNetCore.Components.Web;
using Microsoft.AspNetCore.Components.WebAssembly.Hosting;

var builder = WebAssemblyHostBuilder.CreateDefault(args);
builder.RootComponents.Add<App>("#app");
builder.RootComponents.Add<HeadOutlet>("head::after");

builder.Services.AddScoped(sp => new HttpClient { BaseAddress = new Uri(builder.HostEnvironment.BaseAddress) });

await builder.Build().RunAsync();
```

### launchSettings.json

```
{
  "profiles": {
    "LT2-PackageTest": {
      "commandName": "Project",
      "dotnetRunMessages": true,
      "launchBrowser": true,
      "inspectUri": "{wsProtocol}://{url.hostname}:{url.port}/_framework/debug/ws-proxy?browser={browserInspectUri}",
      "applicationUrl": "https://127.0.0.1:58443;http://127.0.0.1:58080",
      "environmentVariables": {
        "ASPNETCORE_ENVIRONMENT": "Development"
      }
    }
  }
}
```
