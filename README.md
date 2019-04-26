# Deploy SharePoint Online Framework Web Parts on SharePoint 2019
Here we will explain how to deploy SharePoint Framework Client-Side Web Parts made for SharePoint Online onto SharePoint 2019 On-Premises Servers.

## Step 1: Find on GitHub a SharePoint Online Web Part that you want to add on your SP2019 Server

For example, let's consider the React Script Editor Web Part. This web part is really important since it brings an equivalent of the Content Editor Web Part to the Modern pages.

You can donwload the react-script-editor web part here:
https://github.com/SharePoint/sp-dev-fx-webparts/tree/master/samples/react-script-editor

(to download this repository, you can go to the root folder https://github.com/SharePoint/sp-dev-fx-webparts and click on "Clone or download" -> Download ZIP)

## Step 2: Prepare your SharePoint 2019 On-Premises environment

Create and configure the app catalog
Add a library named "CDN" and make sure every member of your organisation has read access on it

## Step 3: Modify the downloaded folder to make it work with SharePoint 2019 Framework

Once the repository downloaded on your computer, please unzip the downloaded file and go to the "script-editor" folder (in sp-dev-fx-webparts-master\samples\react-script-editor).

From here, you'll have to modify the following files to make them compatible with SharePoint 2019:
* package.json
* config\write-manifests.json

### Modify the package.json file
Edit the "package.json" file and replace every value in front of "@microsoft/..." by "^1.5.1".
For example,
```shell
"@microsoft/load-themed-styles": "^1.5.1"
```
will be changed in
```shell
"@microsoft/load-themed-styles": "^1.4.1"
```

### Modify the config\write-manifests.json
Open the "config" folder and then edit the "write-manifests.json" file to add the path to the CDN SharePoint library you have created at step 3.

For example,
```shell
"cdnBasePath": "<!-- PATH TO CDN -->"
```
will be replaced by
```shell
"cdnBasePath": "https://intranet.mysharepointdomain.com/sites/AppCatalog/CDN"
```

## Step 4: Package the solution
Open a command prompt (cmd.exe), go to the "react-script-editor" directory you have modified and run the following commands:
```shell
npm install
gulp –ship
gulp package-solution –ship
```

## Step 5: Add the solution to the SharePoint 2019 App Catalog
