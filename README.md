cscommandlets
=============

PowerShell commandlets for Content Server. The master branch is for 64 bit IDs (10.5), the master-32bit branch is for the older ID numbers (i.e. 9.7.1 to 10.0).

It's just a PowerShell wrapper to the Content Server SOAP based web services. It's written to support a few admin and SharePoint integration requirements. Current calls are:

### Open-CSConnection
Simple Content Server based login, no OTDS or single sign-in support.

Parameters:
- Username **mandatory**
- Password **mandatory**
- ServicesDirectory, e.g. http://server.domain/cws/ **mandatory**

### Add-CSFolder
Creates a folder. Just support for naming at the moment.

Parameters:
- Name **mandatory**
- ParentID **mandatory**

### Add-CSProjectWorkspace
Creates a project workspace.

Parameters:
- Name **mandatory**
- ParentID **mandatory**
- TemplateID optional

### Add-CSUser
Creates a user

Parameters:
- Login **mandatory**
- DepartmentGroupID **mandatory** 1001 is DefaultGroup
- Password optional
- FirstName optional
- MiddleName optional
- LastName optional
- Email optional
- Fax optional
- OfficeLocation optional
- Phone optional
- Title optional

### Remove-CSUser
Deletes a user. Can't find a disable function in the API.

Parameters:
- UserID **mandatory**

### Remove-CSNode
Deletes most Content Server objects

Parameters:
- NodeID **mandatory**

### Add-CSClassifications
Adds the specified list of classification IDs to the specified item.

Parameters:
- NodeID **mandatory**
- ClassificationIDs **mandatory** - array of long integers, e.g. -ClassificationIDs @(123456,234567,345678)

### Add-CSRMClassification
Adds an RM classification to the specified item.

Parameters:
- NodeID **mandatory**
- RMClassificationID **mandatory**

### ConvertTo-EncryptedPassword
Outputs an encrypted version of a password when you want to store your password in a script

Parameters:
- Password **mandatory**

I'll be adding more as there's a need.

Build
-------
Basically this project is the cscommandlets.dll. In the dll there's a snapin called, unsuprisingly, cscommandlets. Feel free to use it if you want to install the cmdlets. InstallUtil under .NET 2 for prior to Windows 8.1, .NET 4 for Windows 8.1. Personally I just use `ImportModule \path\to\dll`

If you're getting an error about running scripts, run `Set-ExecutionPolicy RemoteSigned`

Testing
-------
There's a project in the solution using MSUnit. It does the basics, but it could do with some work. Maybe one day. If you're adding anything new please add your own tests.