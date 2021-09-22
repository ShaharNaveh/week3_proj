# Week 3 Project - Build and publish a website

## Build

### Prerequisite

* install [Visual Studio](https://visualstudio.microsoft.com/) ("2019 community addition" preferably, as this is what we will be using in the documentation)


### Project setup

Select the

```
ASP.NET Core Web App
```

template from the selection menu

![Select project template](https://github.com/ShaharNaveh/week3_proj/blob/main/docs/img/SETUP-Template.png)

Next, choose where the location of the project is going to be stored, and also choose a name for the project, mine is going to be "bonus_website". (The "solution name" can be the same)

![Select project name](https://github.com/ShaharNaveh/week3_proj/blob/main/docs/img/SETUP-Name.png)

Next, we will the select the "Target Framework", make sure to select ".NET 5.0 (Current)". Also make sure to turn off the option of "Configure for HTTPS" (Do like in the image below).

![Select project framework](https://github.com/ShaharNaveh/week3_proj/blob/main/docs/img/SETUP-Framework.png)

#### Change build profile **(Optional)**
Choose the "Release" profile.

![Select "Release" profile](https://github.com/ShaharNaveh/week3_proj/blob/main/docs/img/OPTIONAL-Profile.png)

### Install Dependencies

Right click on the project root directory, and select "Manage NuGet Packages".

![Project menu](https://github.com/ShaharNaveh/week3_proj/blob/main/docs/img/GENERAL-Right_Click_Menu.png)

Next, click on "Browse" and search for

```
Newtonsoft.Json
```

And install the dependecy by clicking "install".

![Installing "Newtonsoft.Json"](https://github.com/ShaharNaveh/week3_proj/blob/main/docs/img/DEP-Install_Newtonsoft_Json.png)

#### Make sure the dependecy was added to the csproj file **(Optional)**
We can see now that "Newtonsoft.Json" was added to our "csproj file".

![Csproj changed](https://github.com/ShaharNaveh/week3_proj/blob/main/docs/img/OPTIONAL-Csproj_Changed.png)

### Publish the website

#### Setup

Right click on the project root directory, and select "Publish".

![Project menu](https://github.com/ShaharNaveh/week3_proj/blob/main/docs/img/GENERAL-Right_Click_Menu.png)

Next, at the menu that opened select "Folder".

![Select "Folder" at the publish menu](https://github.com/ShaharNaveh/week3_proj/blob/main/docs/img/PUBLISH-SETUP-Menu.png)

Next, at the location choose where you want to save the published website, I am going to leave the defaults which is

```
bin\Release\net5.0\publish\
```

![Select the publish location](https://github.com/ShaharNaveh/week3_proj/blob/main/docs/img/PUBLISH-SETUP-Location.png)

Next, make sure that all the publish settings are correct. And click on "Publish".

![Publish to folder](https://github.com/ShaharNaveh/week3_proj/blob/main/docs/img/PUBLISH-SETUP-Ready.png)

If all went good, you should see a message says that the publish was successful.

![Publish to folder](https://github.com/ShaharNaveh/week3_proj/blob/main/docs/img/PUBLISH-SETUP-Successful.png)

### Deploy the website to the server

#### Prerequisite

First, we need to install the IIS role.

Run the following command in an elevated powershell session (Run as administrator).

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

Next, we need to install the [Winodws Hosting Bundle](https://dotnet.microsoft.com/download/dotnet/thank-you/runtime-aspnetcore-5.0.10-windows-hosting-bundle-installer), in order for IIS to be able to run our project.

> **NOTICE**: It is very important to install the IIS role **BEFORE** the "Windows hosting bundle".

#### Setup the application pool

> **NOTE**: All the following commands needs to be executed in an elevated powershell session (Run as administrator).

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

Next, import the "WebAdministration" module, so we can manage the IIS server.

```powershell
Import-Module WebAdministration
```

Next, create new WebAppPool and call it what ever you want, we will call ours "Bonus_Website"

```powershell
New-WebAppPool -Name "Bonus_Website"
```

Next, we will set the "managedRuntimeVersion" to "No Managed Code", we can achive this by running:

```powershell
Set-ItemProperty -Path IIS:\AppPools\Bonus_Website managedRuntimeVersion ""
```

#### Setup the website

First, we need to create the directory for our website.

Usually the website sits in

```
C:\inetpub\wwwroot\
```

So we will create a folder in that location, and we will call our folder "bonus":

```powershell
New-Item -Path C:\inetpub\wwwroot\bonus -ItemType Directory
```

Next, transfter the content of the directory that you published in [here](#setup).

Next, we will create the website entry

```powershell
New-Website -Name "Bonus_Website" -ApplicationPool "Bonus_Website" -PhysicalPath "C:\inetpub\wwwroot\bonus\" -Port 5100
```

And, the last step is to enable trafic on that port.

```powershell
New-NetFirewallRule -DisplayName "Bonus Website" -Direction Inbound -Action Allow -Protocol TCP -LocalPort 5100
```

---

Result:

![Working-Proof](https://github.com/ShaharNaveh/week3_proj/blob/main/docs/img/WORKING_PROOF.png)
