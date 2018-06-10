# Test.Automation.ChromeDriver

**Readme.md**

### Version History
|Version|Date|Notes|
|---|---|---|
|v2.40|2018-06-08|Supports Chrome v66-68|
|v2.35| 2018-01-10|Supports Chrome v62-64|
|v2.33| 2017-11-11|Supports Chrome v60-62|
|v2.30| 2017-06-07|Supports Chrome v58-60|

## WebDriver Download Links

|Browser | WebDriver | Download |Notes|
|-----|-----|-----|----|
| [Chrome](https://www.google.com/chrome/browser/desktop/index.html?system=true&standalone=1) | chromedriver.exe | [ChromeDriver](https://sites.google.com/a/chromium.org/chromedriver/downloads) | Use Chrome's 'alternative installer'<br>Recommended for testing Web applications built with moden javascript frameworks like React and Ember |
| HeadLess Chrome | chromedriver.exe | see above | headless web testing |
| [Internet Explorer (IE)](https://support.microsoft.com/en-us/help/17621/internet-explorer-downloads) | IEDriverServer.exe | [IEDriverServer](http://selenium-release.storage.googleapis.com/index.html) |Default browser prior to Windows 10 |
| [Microsoft Edge](https://www.microsoft.com/en-us/windows/microsoft-edge#AoPhgFHFcSwpqU6Z.97) | MicrosoftWebDriver.exe | [MicrosoftWebDriver](https://developer.microsoft.com/en-us/microsoft-edge/tools/webdriver/)| Default browser for Windows 10 |
| PhantomJS | phantomjs.exe | [PhantomJS](http://phantomjs.org/download.html) | PhantomJS is **deprecated!**<br>The project has been abandoned.<br>Use Headless Chrome for headless web testing |

## Create a Local NuGet Package with OctoPack
- Add a `.nuspec` file to each project in the solution that you want to package with NuGet.
- The `.nuspec` file name **must be the same name as the project** with the `.nuspec` extension
- Open a '`Developer Command Prompt for VS2017`' command window.
- Navigate to the solution or project that you want to OctoPack.
- Run the following command:

```
// To Create packages for each project in the solution:
MSBUILD Test.Automation.sln /t:Rebuild /p:Configuration=Release /p:RunOctoPack=true /p:OctoPackPackageVersion=1.0.0 /p:OctoPackPublishPackageToFileShare=C:\Packages

// To Create a package for a single project:
MSBUILD Test.Automation.ChromeDriver.csproj /t:Rebuild /p:Configuration=Release /p:RunOctoPack=true /p:OctoPackPackageVersion=1.0.0 /p:OctoPackPublishPackageToFileShare=C:\Packages

```

#### MSBUILD OctoPack Command Syntax
|Switch|Value|Definition|
|-----|-----|-----|
|`/t:Rebuild`|  |MSBUILD Rebuilds the project(s).|
|`/p:Configuration=`|`Release`|Creates and packages a Release build.|
|`/p:RunOctoPack=`|`true`|Creates packages with Octopack using the .nuspec file layout.|
|`/p:OctoPackPackageVersion=`|`1.0.0`|Updates Package Version.|
|`/p:OctoPackPublishPackageToFileShare=`|`C:\Packages`|Copies packages to local file location.|
    
#### Other OctoPack Options:

|Switch|Value|Description|
|-----|-----|-----|
|`/p:Configuration=`|`[ Release | Debug ]`|The build configuration|
|`/p:RunOctoPack=`|`[ true | false ]`|Enable or Disable OctoPack|
|`/p:OctoPackPackageVersion=`|`1.2.3`|Version number of the NuGet package. By default, OctoPack gets the version from your assembly version attributes. Set this parameter to use an explicit version number.|
|`/p:OctoPackPublishPackageToFileShare=`|`C:\Packages`|Copies packages to the specified directory.|
|`/p:OctoPackPublishPackageToHttp=`|`http://my-nuget-server/api/v2/package`| Pushes the package to the NuGet server|
|`/p:OctoPackPublishApiKey=`|`ABCDEFGMYAPIKEY`|API key to use when publishing|
|`/p:OctoPackNuGetArguments=`| `-Verbosity detailed`|Use this parameter to specify additional command line parameters that will be passed to NuGet.exe pack.|
|`/p:OctoPackNuGetExePath=`|`C:\MyNuGetPath\`|OctoPack comes with a bundled version of NuGet.exe. Use this parameter to force OctoPack to use a different NuGet.exe instead.|
|`/p:OctoPackNuSpecFileName=`|`<C#/VB_ProjectName>.nuspec`|The NuSpec file to use.|

## Viewing Local Packages
- Install NuGet Package Explorer to view local packages.  
- [NuGetPackageExplorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)

## NuGet Command Line Reference
Ensure that NuGet.exe is in your path.  
Running NuGet using a .nuspec file allows greater control over what files are packed and excluded.  
  
```
NUGET PACK Test.Automation.Selenium.nuspec -Verbosity detailed  -OutputDirectory "C:\Packages"
```

#### Explaination of Command Arguments
|Argument|Value|Description|
|----|----|----|
|`PACK`|`Test.Automation.Selenium.nuspec`|Create a package from .nuspec file|
|`-Verbosity`|`detailed`|Displays verbose command output for debugging|
|`-OutputDirectory`|`"C:\Packages"`|Copies package to local directory|



