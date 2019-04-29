# Deploy SharePoint Online Modern Web Parts on SharePoint 2019
Here we will explain how to deploy SharePoint Framework Client-Side Web Parts made for SharePoint Online on SharePoint 2019 On-Premises Servers.

## 1. Find a SharePoint Online Web Part that you want to add on your SP2019 Server

For example, let's consider the React Script Editor Web Part. This web part is really important since it brings an equivalent of the Content Editor Web Part to the Modern pages.

You can donwload the react-script-editor web part from GitHub here :
https://github.com/SharePoint/sp-dev-fx-webparts/tree/master/samples/react-script-editor

(to download this repository, you can go to the root folder https://github.com/SharePoint/sp-dev-fx-webparts and click on "Clone or download" -> Download ZIP)

## 2. Prepare your SharePoint 2019 On-Premises environment and add a CDN library

Create and configure the App Catalog. Then **add a library named "CDN" to your App Catalog site** and make sure every member of your organisation has read access to it.

## 3. Modify the downloaded folder to make it work with SharePoint 2019 Framework

Once the repository downloaded on your computer, please unzip the downloaded file and go to the "script-editor" folder (in sp-dev-fx-webparts-master\samples\react-script-editor).

From here, you'll have to modify the package.json and config\write-manifests.json files to make them compatible with SharePoint 2019.

### 3.1 Modify the package.json file
Since Sharepoint Online and SharePoint 2019 don't use the same framework version, you'll have to **modify the framework settings**. To do so, please edit the **"package.json"** file and replace every value in front of "@microsoft/..." by "**1.4.1**".

For example,
```shell
"@microsoft/load-themed-styles": "^1.5.1"
```
will be changed in
```shell
"@microsoft/load-themed-styles": "^1.4.1"
```

### 3.2 Modify the config\write-manifests.json
Open the "config" folder and then **edit the "write-manifests.json" file and replace the PATH TO CDN by the path of your CDN library** (created at step 3).

For example,
```shell
"cdnBasePath": "<!-- PATH TO CDN -->"
```
will be replaced by
```shell
"cdnBasePath": "https://intranet.mysharepointdomain.com/sites/AppCatalog/CDN"
```

## 4. Package the solution
Open a command prompt (cmd.exe), go to the "react-script-editor" directory you have modified and run the following commands:
```shell
cd C:\mydownloads\sp-dev-fx-webparts-master\samples\react-script-editor
npm install
gulp --ship
gulp package-solution --ship
```

## 5. Add the solution to the SharePoint 2019 App Catalog
Now that the solution is packaged, you can add it to SharePoint.

### 5.1 Add the dependencies
Several .js and .json files have been generated into the **"\temp\deploy"** folder of your computer. Please **drag & drop them into the CDN library of your app catalog** (this library was created at step 2).

### 5.2 Add the app
Take the **.sppkg** file from the **"\sharepoint\solution"** folder of your computer and **upload it to the "Apps for SharePoint"** section of your App Catalog.

## 6. Add the Web Part to your sites

This app is now visible in the apps of your organization and can be added to your SharePoint 2019 site collections. Enjoy SharePoint Online Web Parts on SharePoint Server 2019! :-D

If you have any questions or feedback, please do not hesitate.

