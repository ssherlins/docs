---
title: "Moving from Mendix Studio Pro 8 to 9"
category: "General Info"
menu_order: 20
description: "Provides details on updating your project from Mendix 8 to Mendix 9, including sections on converting your project and deprecated features."
tags: ["studio pro", "studio"]
---

## 1 Introduction

Mendix Studio Pro 9 and Mendix Studio 9 give you powerful new tools to enhance your apps. For the full list of changes, see the Studio Pro 9 and Studio 9 release notes. If you want to upgrade an existing Studio Pro 8 or Studio 8 project to its respective 9 version, please check the information below:

* If you are upgrading your app in Studio from Mendix 8 to 9, see [Upgrading from Mendix 8 to 9 for Studio](#studio-upgrade) below.
* If you are converting your app from Studio Pro 8 to Studio Pro 9, see [Changing Your App Before Upgrading to Studio Pro 9](#studio-pro-upgrade) below.

## 2 Upgrading from Mendix 8 to 9 for Studio {#studio-upgrade}

### 2.1 Turn On RCSI for MS SQL Server

In order to improve performance and reduce the chance of deadlocks, Mendix 9 requires MS SQL Server to be used with **Read Committed Snapshot Isolation** (RCSI) turned **ON**. 

During the synchronization stage, Mendix 9 will perform a check for the RCSI status and could abort the process if it is not **ON** and the database user lacks the necessary privileges to do so automatically.

## 3 Update from Mendix 8 to 9 for Studio Pro {#studio-pro-upgrade}

The following sub-sections explain the steps to take in converting your app from Mendix 8 to Mendix 9. We recommend you first review the [Breaking Changes](/releasenotes/studio-pro/9.0#breaking-changes) section of the *Studio Pro 9.0* release notes as well as our updated [System Requirements](/refguide/system-requirements).

### 3.1 Back Up Your Project

Make sure that you have either committed your latest changes to Team Server, or created a backup of your local project before you start the conversion.

### 3.2 Upgrade to the Latest Release of Version 8

{{% alert type="warning" %}}
It is technically required for you to upgrade your app to Mendix 8.12 first to be able to update it to Mendix 9. However, we recommend you update to the latest version of Mendix 8: [8.17](/releasenotes/studio-pro/8.17).
{{% /alert %}}

To upgrade to Mendix 8.17, follow these steps:

1. Download the latest patch release of Studio Pro [v8.17](/releasenotes/studio-pro/8.17).
1. Open your app in Studio Pro v8.17.
1. Allow it to upgrade the app, if necessary.

### 3.3 Review Your Mendix 8 App

Review your app in combination with the sections below and assess if further action needs to be taken before upgrading to Mendix 9.

You should run your app, test all functionality, and ensure it works without error. You should also fix any depreciation warnings you see both in development in Studio Pro, as well as in the runtime using your console and browser console.

### 3.4 Save Your Version 8 App

Backup or commit your project so that you can return to it if necessary.

Your app is now ready to be upgraded to Mendix 9. You can now close the project in Studio Pro 8.

### 3.5 Upgrade Your App to Version 9

Open your project in Studio Pro 9 and allow Studio Pro to update your app to version 9. Mendix will upgrade your app for you automatically.

Review all error messages and messages about deprecated items and make changes where necessary.

### 3.6 Upgrade All Widgets and Modules {#upgrade-widgets}

To minimize the chance of problems, you should update all widgets and other Marketplace modules used by your project to the latest version.

Check if there is a newer version of your modules available in the Marketplace. Read the version release notes in the Marketplace to see whether you need to perform specific actions when upgrading.

Be sure to update these key widgets, resources, and actions:

* [Native Mobile Resources (Mx9 Beta)](https://marketplace.mendix.com/link/component/116537)
* [Nanoflow Commons (Mx9 Beta)](https://marketplace.mendix.com/link/component/116538)
* [Data Grid 2 (Mx9 Beta)](https://marketplace.mendix.com/link/component/116540)

In general you should not remove and reimport modules, unless this is recommended in the release notes. If you do remove and reimport them, you may lose data or configuration related to the module.

### 3.7 Update Atlas Module (Optional)

Mendix 9 comes with a new Atlas theme including new page templates and building blocks. To get this theme, you can download the [Atlas UI 3 (Mx9 Beta)](https://marketplace.mendix.com/link/component/116539) module package from the Marketplace.

### 3.8 Review and Test Your App

Finally, review the sections below and ensure that you have made all the changes necessary. Test the app for any unexpected results.

{{% alert type="success" %}}
Congratulations! Your app has been successfully upgraded to Mendix 9 and you can continue working as normal.
{{% /alert %}}

## 4 Runtime API Changes

Most of the Java API calls that were deprecated in Mendix 8 have been removed. If you were still using such methods in your Java actions, you must replace or delete them. To check which calls were depreciated, click the **Mendix 8 Server Runtime API** link in our [Runtime API Documentation](/apidocs-mxsdk/apidocs/runtime-api).

Additionally, refer to the Mendix Studio Pro 9.02 Release notes for more Runtime API change details.

### 4.1 Changes to Database Uniqueness

Before Mendix 9, Mendix could ensure data uniqueness using either the Mendix runtime or by relying on the database engine itself. Starting with Mendix 9, **Database** will be the only option. 

If your project is still using Mendix runtime for uniqueness validation, then you should set the custom runtime setting `DataStorage.EnableDiagnostics` to `true`  to check for potential data redundancy issues that might exist in the database. 

If any are found, an error like **An error occured while initializing the Runtime: Detected unique constraing violation...** will be logged. To solve this, your project will have to be prepared before moving to Mendix 9. You can obtain the tools you need by [submitting a support request](/developerportal/support/submit-support-request).

## 5 Testing Native Mobile Apps

To test and preview native mobile apps in Mendix 9, you must download the Mendix 9 version of the Make It Native app:

* Download Make It Native 9 for Android in the [Google Play Store](https://play.google.com/store/apps/details?id=com.mendix.developerapp.mx9)
* Download Make It Native 9 for iOS in the [Apple App Store](https://apps.apple.com/nl/app/make-it-native/id1542182000)

For best results with native apps, make sure you have updated the [Native Mobile Resources (Mx9 Beta)](https://marketplace.mendix.com/link/component/116537) module as described in the [Upgrade All Widgets and Modules](#upgrade-widgets) section above.

## 6 Client API Changes

Client APIs that were deprecated and marked for removal in Mendix 9 were indeed removed. Libraries like `big.js`, `react`, `react-native`, and a few others shipped with the Client have been updated to latest version. This might affect your custom and pluggable widgets and to JavaScript actions. Please refer to the [Breaking Changes](/releasenotes/studio-pro/9.0#breaking-changes) section of the *Studio Pro 9.0* release notes for more details.

## 7 Native Dependencies

Mendix 9 native apps no longer include non-essential native libraries like `react-native-maps`, `react-native-ble-plx`, `react-native-geocoder`, and others by default. Instead, new functionality of declaring native dependencies for components has been introduced in Mendix 9. Every pluggable widget or JavaScript action must declare which native libraries it uses. This way, native apps can be bundled with only the libraries they need while unnecessary libraries are not included.

If your pluggable widget or JavaScript action uses libraries that require native linking, please update your widgets and actions in order to define those native libraries as dependencies for your components. Read more about native dependencies in [Declaring Native Dependencies](/apidocs-mxsdk/apidocs/native-dependencies).

## 8 Read More

* [Studio Pro 9 Release Notes](/releasenotes/studio-pro/9.0)
