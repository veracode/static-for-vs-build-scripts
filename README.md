<img src="https://help.veracode.com/internal/api/webapp/header/logo" width="200" /><br>

# Create a New Veracode Application and Sandbox

## Overview

The modifications here show how to create a new Veracode application and sandbox on the platform when you run a scan. The only file you need to update for this example is **veracode-project.json**. 

## Steps

 - Download the **veracode-project.json** file
 - Update the appName, criticality, and sandboxName values as appropriate
   - criticality values can be:
     - High
     - Low
     - Medium
     - VeryHigh
     - VeryLow
 - Add the **veracode-project.json** to your solution directory
 - From the extension menu, choose **Run Scan**

 After Run Scan syncs to the platform, and executes a build/package, you should see the scan start and the new application and sandbox being created on the platform.

 Note that when you run the scan again [the Wizard](https://marketplace.visualstudio.com/items?itemName=Veracode.StaticForVs2022#the-wizard) will appear asking if you want to select a sandbox (you cannot change your application name at this point). You can either select the sandbox you'd just created, or click next. If you selected a sandbox, an entry will be added to your **veracode-project-user.json** with your sandbox name reflected in the `sandboxName` property. Otherwise, the sandboxName property will be empty (but will still continue to use the sandboxName value in your **veracode-project.json** file).