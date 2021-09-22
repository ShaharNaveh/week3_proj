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

![Select project template](https://github.com/ShaharNaveh/week3_proj/blob/DOC-build-publish/docs/img/SETUP-Template.png)

Next, choose where the location of the project is going to be stored, and also choose a name for the project, mine is going to be "bonus_website". (The "solution name" can be the same)

![Select project name](https://github.com/ShaharNaveh/week3_proj/blob/DOC-build-publish/docs/img/SETUP-Name.png)

Next, we will the select the "Target Framework", make sure to select ".NET 5.0 (Current)". Also make sure to turn off the option of "Configure for HTTPS" (Do like in the image below).

![Select project framework](https://github.com/ShaharNaveh/week3_proj/blob/DOC-build-publish/docs/img/SETUP-Framework.png)

#### Change build profile **(Optional)**
Choose the "Release" profile.

![Select "Release" profile](https://github.com/ShaharNaveh/week3_proj/blob/DOC-build-publish/docs/img/OPTIONAL-Profile.png)

### Install Dependencies

Right click on the project root directory, and select "Manage NuGet Packages".

![Project menu](https://github.com/ShaharNaveh/week3_proj/blob/DOC-build-publish/docs/img/GENERAL-Right_Click_Menu.png)

Next, click on "Browse" and search for

```
Newtonsoft.Json
```

And install the dependecy by clicking "install".

![Installing "Newtonsoft.Json"](https://github.com/ShaharNaveh/week3_proj/blob/DOC-build-publish/docs/img/DEP-Install_Newtonsoft_Json.png)

#### Make sure the dependecy was added to the csproj file **(Optional)**
We can see now that "Newtonsoft.Json" was added to our "csproj file".

![Csproj changed](https://github.com/ShaharNaveh/week3_proj/blob/DOC-build-publish/docs/img/OPTIONAL-Csproj_Changed.png)

### Publish the website

#### Setup

Right click on the project root directory, and select "Publish".

![Project menu](https://github.com/ShaharNaveh/week3_proj/blob/DOC-build-publish/docs/img/GENERAL-Right_Click_Menu.png)

Next, at the menu that opened select "Folder".

![Select "Folder" at the publish menu](https://github.com/ShaharNaveh/week3_proj/blob/DOC-build-publish/docs/img/PUBLISH-SETUP-Menu.png)

Next, at the location choose where you want to save the published website, I am going to leave the defaults which is

```
bin\Release\net5.0\publish\
```

![Select the publish location](https://github.com/ShaharNaveh/week3_proj/blob/DOC-build-publish/docs/img/PUBLISH-SETUP-Location.png)

Next, make sure that all the publish settings are correct. And click on "Publish".

![Publish to folder](https://github.com/ShaharNaveh/week3_proj/blob/DOC-build-publish/docs/img/PUBLISH-SETUP-Ready.png)

If all went good, you should see a message says that the publish was successful.

![Publish to folder](https://github.com/ShaharNaveh/week3_proj/blob/DOC-build-publish/docs/img/PUBLISH-SETUP-Successful.png)
