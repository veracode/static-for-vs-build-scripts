<img src="https://help.veracode.com/internal/api/webapp/header/logo" width="200" /><br>

# Veracode for Visual Studio Build Scripts

## Overview

A repository for managing different build/publish/package/scan script use cases. The **main** branch contains the default scripts as created by Veracode Static for Visual Studio 2019 and Veracode Static for Visual Studio 2022. The branches referred to further below contain customizations of these files for various use cases.

## Table of Contents
- [Before You Begin](#before-you-begin)
- [Usage](#usage)
- [License](#license)
- [User Contributions](#user-contributions)
  - [How to Create a New Veracode Application and Sandbox](#how-to-create-a-new-veracode-application-and-sandbox)

## Before You Begin

If you haven't read the documentation, you should review it [here](https://marketplace.visualstudio.com/items?itemName=Veracode.StaticForVs2022#veracode-static-for-visual-studio-documentation-preview).

## Usage

All of the files mentioned below are either MSBuild scripts or JSON configuration files and can be customized accordingly.

The main folders and files contained in this repository are:
- main
  - Directory.Build.targets
  - Veracode.Package.build
  - Veracode.props
  - veracode-build-microsoft.json
  - veracode-project.json
- special
  - VeracodePublishProfile.pubxml
- user
  - veracode-build-microsoft-user.json
  - veracode-project-user.json

### main

These files are created by the extension if they don't already exist with [the Wizard](https://marketplace.visualstudio.com/items?itemName=Veracode.StaticForVs2022#the-wizard) (*veracode-project.json*) or when you [build/package](https://marketplace.visualstudio.com/items?itemName=Veracode.StaticForVs2022#buildpackage-and-publishpackage) (*Directory.Build.targets*, *Veracode.Package.build*, *Veracode.props*, *veracode-build-microsoft.json*).

They are placed in the solution root of the application.

### special

This file (*VeracodePublishProfile.pubxml*) is created by the extension when you [Publish/Package](https://marketplace.visualstudio.com/items?itemName=Veracode.StaticForVs2022#buildpackage-and-publishpackage) and you have at least one <span>ASP.</span>NET Framework project.

This file is placed in the `Properties/PublishProfiles` directory of each <span>ASP.</span>NET Framework project since that project type needs to be precompiled.

### user

The *veracode-build-microsoft-user.json* file is created by the extension when you [build/package](https://marketplace.visualstudio.com/items?itemName=Veracode.StaticForVs2022#buildpackage-and-publishpackage), and the *veracode-project-user.json* is created by the extension using [the Wizard](https://marketplace.visualstudio.com/items?itemName=Veracode.StaticForVs2022#the-wizard).

These files are placed in the `C:\Users\{UserName}\.veracode` directory, and will override the corresponding files in the solution directory.

## License
[![MIT license](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

See the [LICENSE](LICENSE) file for details.

## User Contributions

### How to Create a New Veracode Application and Sandbox

The modifications in the branch below show how to create a new Veracode application and sandbox on the platform when you run a scan. The only file you need to update for this example is **veracode-project.json**.

[dhabolt/add-veracode-app-sandbox](https://github.com/veracode/static-for-vs-build-scripts/tree/dhabolt/add-veracode-app-sandbox)