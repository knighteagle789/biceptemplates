<!-- omit from toc -->
# Introduction 

This is the code behind for all Azure Resource templates that I have made available.  These templates will follow best practices for Bicep files, as well as follow Microsoft's Cloud Adoption Framework [naming](https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/ready/azure-best-practices/resource-naming) and [tagging](https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/ready/azure-best-practices/resource-tagging) strategies.  This area is meant for very generic resource types that are to be used.  Each resource that is added should be only 1 resource type.

- [1. Getting Started](#1-getting-started)
  - [1.1. Installation](#11-installation)
- [2. Build and Test](#2-build-and-test)
- [3. Contribute](#3-contribute)


# 1. Getting Started

## 1.1. Installation

1. Follow the installation and setup instructions found in the [DevOpsDevContainer repository](https://dev.azure.com/americanautoshield/DevOps/_git/DevOpsDevContainer)
2. Run `make clone-templaterepos` to automatically sync all the template repos
3. In the terminal windows of VSCode, change your directory the bicepTemplates (`cd bicepTemplates`)

# 2. Build and Test

1) `Invoke-Build` - This will clean, build, test and generate docs for all items found in the resources folder
2) `Invoke-Build cleanAll` - This will delete both the Build and Test Results directory
3) `Invoke-Build cleanBuild` - This will delete the Build directory
4) `Invoke-Build cleanTest` - This will delete the Test Results directory
5) `Invoke-Build BuildBicep` - This will build the bicep files in the resources folder (create ARM template versions)
6) `Invoke-Build TestBicep` - This will download and run the ARM-TTK powershell modules for testing of your Bicep / ARM template files
7) `Invoke-Build ValidateBicep` - This will run your template against the PS Rules for any security or best practices issues
8) `Invoke-Build IntegrationTest` - This will run pester tests on your template.  This test will be pulled from the `.tests\integration` folder
9) `Invoke-Build GenerateDocs` - This will create a markdown file of the resource and add it to the `docs` directory
10) `Invoke-Build PublishBicep` - This will deploy the built Bicep files as a Template Spec to a specified resource group
11) `Invoke-Build Deploybicep` - Thiswill deploy the built Bicep files as a Bicep Module published to a specified Azure Registry (ACR) 
12) You can run each of those Invoke-Build in 1 command buy adding `-task` and then what you want to run
13) You can specify a specific resource to run the invoke-build on buy adding `-templatePath` and the directory of the resource.
14) Example for the above 2: `invoke-build -task clean, buildbicep, testbicep, publishbicep -templatepath resources/resourcegroup`

# 3. Contribute

1. Run the `generateResource.sh` script.  This will copy the .template folder found in the resources directory and rename it to the Resource Name.
1. Modify the module.\*.bicep and resource.\*.bicep files.
   1. Make the resource.\*.bicep file as generic as possible.  There should be no variables or 
   2. All parameters should be placed in the module.\*.bicep file
2. Run the commands in [2. Build and Test](#2-build-and-test)
3. Before resyncing / merging with the main repo, run `Invoke-Build clean`
