<img src="https://help.veracode.com/internal/api/webapp/header/logo" width="200" /><br>

# Don't Build, Just Upload Artifacts

## Overview

If you want to drop some folders/files into a specified directory and have them zipped and uploaded to the platform without doing a Veracode build, this workflow is a great starting point.

## Details

The following files in the main directory have been modified:
- Veracode.Package.build
- veracode-build-microsoft.json

Refer to the sections below for details of the modifications.

### veracode-build-microsoft.json

The modifications to this file were to remove the MSBuild statements from **buildArguments** and **publishArguments** that initiates the build. Also note that `/p:VeracodeBuildOutputPath='{BuildOutputPath}'` is being passed in case a fully qualified directory is specified.

### Veracode.Package.build

The modifications to this MSBuild file handle the zipping of the directories before they're moved, and to show setup errors and fix them if possible. The setup errors are:
- The folder $(VeracodeTemporaryBuildPath) was missing and has been created.
- The folder $(VeracodeTemporaryBuildPath) is empty. Please place the folders/files to upload to Veracode into this directory.

## Usage

Copy **Veracode.Package.build** and **veracode-build-microsoft.json** to your solution directory, replacing the existing files. If you've made other additional modifications to these files, you'll need to merge them as appropriate instead of replacing them.

Before developers run a scan they'll need to place the folders/files that need to be uploaded to the Veracode platform in the veracode-tmp/binary directory.

The only file you need to modify is the **Veracode.Package.build** file. Each folder you need to zip and upload to the Veracode platform will need to have an entry added.

If you need to upload individual files to the platform, you'll need to place them into a folder first. If you have files that are already zipped, they cannot be placed into folders that will be zipped, instead, you'll need to use the MSBuild Copy command as shown below.

```
<ZipDirectory 
	SourceDirectory="$(VeracodeTemporaryBuildPath)/WebGoatCore" 
	DestinationFile="$(VeracodeFinalPath)/WebGoatCore.zip" />

<ZipDirectory 
	SourceDirectory="$(VeracodeTemporaryBuildPath)/WebSite" 
	DestinationFile="$(VeracodeFinalPath)/WebSite.zip" />

<ZipDirectory 
	SourceDirectory="$(VeracodeTemporaryBuildPath)/XtremelyEvilWebApp" 
	DestinationFile="$(VeracodeFinalPath)/XtremelyEvilWebApp.zip" />

<Copy 
    SourceFiles="$(VeracodeTemporaryBuildPath)/javascript.zip"
    DestinationFolder="$(VeracodeFinalPath)" />

<Copy 
    SourceFiles="$(VeracodeTemporaryBuildPath)/other.zip"
    DestinationFolder="$(VeracodeFinalPath)" />

```

### Note

There is no MSBuild command that can simply point to a directory containing folders to zip, without adding the [MSBuild Extension Pack](https://www.nuget.org/packages/MSBuild.Extension.Pack/), or the [MSBuild.Community.Tasks](https://github.com/loresoft/msbuildtasks). 

In other words, without installing one of these extension packs, you need to manually add each folder you want to upload as shown above.

## Optional

### Changing the Default Directory Name

The default name for the directory you upload your folders to is *binary* (since the normal build processes produce binaries). You can easily change this by updating this line in the **Veracode.props** file:

```xml
<VeracodeTemporaryBuildPath>$(VeracodeBuildPath)binary/</VeracodeTemporaryBuildPath>
```

Just change *binary* to whatever folder name you'd like.