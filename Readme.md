# Test.Automation.ChromeDriver
**Readme.md**
### Version History
|Version|Date|Notes|
|---|---|---|
|ChromeDriver v2.30 |2017-06-07|Supports Chrome v58-60|
### Download Link
[**ChromeDriver**](https://sites.google.com/a/chromium.org/chromedriver/)
### ChromeDriver Intro
- WebDriver is an open source tool for automated testing of webapps across many browsers.  
- It provides capabilities for navigating to web pages, user input, JavaScript execution, and more.  
- ChromeDriver is a standalone server which implements WebDriver's wire protocol for Chromium.

## NuGet 4.0+
[**Create .Net Standard Packages**](https://docs.microsoft.com/en-us/nuget/guides/create-net-standard-packages-vs2017)  
[**PackageReference in Project Files**](https://docs.microsoft.com/en-us/nuget/consume-packages/package-references-in-project-files)  
[**Packing Using a .nuspec**](https://docs.microsoft.com/en-us/nuget/schema/msbuild-targets)  
[**NuGet Documentation**](http://blog.nuget.org/20170316/NuGet-now-fully-integrated-into-MSBuild.html)  

NuGet 4.0+ can work directly with the information in a .csproj file without requring a separate `.nuspec` or `project.json` file. 
All the metadata that was previously stored in those configuration files can be instead stored in the `.csproj` file directly, as described here.

With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets. 
These targets allow you to work with NuGet as you would with any other MSBuild task or target.
### MSBUILD Command
- Naviage to the .csproj directory
- Run `MSBUILD` command

```
msbuild /t:pack /p:Configuration=Release 

# Output is copied to the tools folder instead of lib folder.
msbuild /t:pack /p:Configuration=Release /p:IsTool=true  

# Use .nuspec file.
msbuild /t:pack /p:Configuration=Release Test.Automation.ChromeDriver.csproj /p:NuspecFile=Test.Automation.ChromeDriver.2.30.0.nuspec /p:NuspecBasePath=.
```
### Test.Automation.Chromdriver.2.30.0.nuspec File
```
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2011/08/nuspec.xsd">
  <metadata>
    <id>Test.Automation.ChromeDriver</id>
    <version>2.30.0</version>
    <authors>jefsmo</authors>
    <owners>ChromeDriver is developed by members of the Chromium and WebDriver teams.</owners>
    <requireLicenseAcceptance>false</requireLicenseAcceptance>
    <iconUrl>https://raw.githubusercontent.com/jefsmo/Test.Automation/master/Test.Automation.ChromeDriver/chromedriver-logo.gif</iconUrl>
    <projectUrl>https://github.com/jefsmo/VSTest-Automation-BaseClass</projectUrl>
    <description>ChromeDriver is a Selenium WebDriver for the Chrome browser.</description>
    <releaseNotes>
      ChromeDriver v2.30 (2017-03-09)
      Supports Chrome v58-60
    </releaseNotes>
    <copyright>© 2016 jefsmo.</copyright>
  </metadata>
  <files>
    <file src="chromedriver.exe" target="content\chromedriver.exe" />
  </files>
</package>
```
### Test.Automation.ChromeDriver.csproj File  
```
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>netstandard1.6</TargetFramework>
    <PackageVersion>2.30.0</PackageVersion>
  </PropertyGroup>

  <PropertyGroup Condition="'$(Configuration)|$(Platform)'=='Release|AnyCPU'">
    <DocumentationFile></DocumentationFile>
  </PropertyGroup>
  
  <Target Name="CopyPackage" AfterTargets="Pack">
    <Copy SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg" DestinationFolder="C:\Packages\" />
  </Target>
  
  <ItemGroup>
    <None Remove="chromedriver.exe" />
  </ItemGroup>
  
  <ItemGroup>
    <Content Include="chromedriver.exe">
      <Pack>true</Pack>
      <PackagePath>content\</PackagePath>
    </Content>
  </ItemGroup>
  
  <ItemGroup>
    <Folder Include="icon\" />
  </ItemGroup>
  
  <ItemGroup>
    <None Update="chromedriver.exe">
      <CopyToOutputDirectory>Never</CopyToOutputDirectory>
    </None>
  </ItemGroup>
  
</Project>
```

