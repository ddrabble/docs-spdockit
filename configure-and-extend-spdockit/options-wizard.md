---
title: Options Wizard
description: >-
  This article explains how to use the Options wizard to adjust and change your
  SPDocKit settings.
author: Tomislav Kunaj
date: 25/5/2017
---

# Options Wizard

## General

Here you can change the startup options:

* Enable Verbose logging – use this only for diagnostics purposes or when asked by the support team.
* Adjust proxy settings.
* Turn on the automatic update check.

## Report Options

Allows you to customize how documents are saved. Tags used while constructing the header and footer are: **CompanyName, Logo, AppName, Date, Page, TotalPages and Server.**

By using the \| separator, the location of each tag can be specified i.e. if the header is set to **{CompanyName}\|\|{Logo}**, the company name will appear in the upper left corner of the page, the upper center will be blank, and the upper right corner of the page will contain the logo \(if uploaded\).

The default footer is set to **Generated by {AppName} on {Date}\|Page {Page}/{TotalPages}** i.e. the application name and the date the export was made will appear in the lower left corner of the page, the lower center will be blank and the lower right corner of the page will contain the number of the page currently opened along with the total page number.

Here you can also change the report throttling options:

* Modify how many site collections will be shown in the Site Topology report.
* Modify the maximum number of principals that will be used to generate data for in throttled reports.
* Modify the maximum number of site collections that will be used to generate data for in throttled reports.
* Modify the maximum number of query results per site collection.
* Modify the maximum number of permissions to use in the Permission Details reports.
* Modify the maximum number of rows in a report.
* Modify the maximum number of rows supported in report export.
* Modify the maximum number of audit logs supported in the Audit Log Details report. 

## Service settings

The snapshots are by default saved to the SPDocKit database. To back up your snapshots, enable the **Save backup of snapshot file to disk** option. You can also define a preferred disk location, where the backup files will be saved.

Here you can also define the **SPDocKit Service running period**. The time you set here determines when the Service will start taking an automatic snapshot to collect the data you specified in the **Snapshot Options** and **Load Target** tabs of the Options Wizard. The **SPDocKit Service** will repeat that task whenever the selected recurrence period runs out. The minimal period is 4 hours, while the default value is 1 day.

Check the **Enable collection of site analytics from SharePoint's Usage and Health Data Collection service** option if you want SPDocKit to collect data used for generating the Site Collections Analytics and Inactive Sites report. After being enabled for the first time, the Analytics job will immediately start to collect data for the last 7 days. It will further run on a daily basis \(between 1AM and 5AM\) and collect data for the previous day.  
You can also define accounts for which the data will not be collected.

Enabling the **automatic index reorganization** will result in better space usage and performance of the SPDocKit database. This job will always be run outside of regular business hours \(around 5 AM by default\).

## Snapshot options

This section allows you to choose what will be loaded by both the **SPDocKit Service** when taking an **automatic snapshot**, and if you select the **Default** mode in the Take Snapshot wizard.

The options are grouped into 4 categories:

* **SharePoint**
  * The **Farm Settings** checkbox will be selected by default. That means that SPDocKit will load farm settings by default and this option cannot be changed. 
  * **Content Types** - When this option is selected, you’ll need to crawl down to each list on the farm since that is where the content types are defined.
  * SPDocKit also allows you to backup all **\*.wsp files** in use by your farm, but you’ll need to define a location for this backup. This data can also be used later to find out whether there are any problems with the assemblies deployed on your farm.
  * **Features and Solutions**, **Workflows**
  * **Document Versions, Extensions and Sizes** - Enable this option to collect data about the **number of documents on a farm and their total size by extension**, which is used in Document Extensions Overview and Document Extension Details report.
* **Security**
  * **Database Permissions** - Selecting this will enable you to view the Database Permissions report. This report shows information about all users, across all databases on a SQL Server. 
  * **Permissions** - If you want to know the permissions of each list item on the farm, you can get that information by selecting the **Permissions check box** and setting the Load Depth to list item. You can also select the **Active Directory Group Members** check box if you wish to load members of the AD groups. 
  * **Administrative Actions Log** - this option will be visible only for SharePoint 2016 FP1 farms and enables you to browse and analyze administrative actions logs collected from your SharePoint farm.
  * **Audit Logs** - this option is required to collect data for Audit Reports where a complete history of changes made on site collections is shown. Enable the **Include Changes Made by System Account** to load actions made by the System Account. 
* **Server Settings**
  * **Installed Programs and available Updates**
  * **SQL Server and IIS Settings Information**
* **Project Server**
  * **Settings**
  * **Projects**  

From version 7 and onwards, you can document Project Server settings, list of projects and their permissions.

You can also specify the load depth, which means how deep you want to crawl your SharePoint with SPDocKit. Possible choices are: site collection. subsites, list, and list items. Be aware that there are some dependencies related to the load depth selection and the available SharePoint information SPDocKit can retrieve. For example, if you want to load content types and workflows, lists are the minimum required load depth. SPDocKit will warn you if your current selection is not possible and provide instruction messages for enabling certain load options.

Finally, you can customize the **snapshots name template**. Under Snapshot Configuration, note the Snapshot Name Template field. We have prepared the Farm Name, Snapshot Mode \(which can be either Automatic or Manual\), and Date \(which you can customize any way you like\), keywords that can be included in the name template. The default date format is: “Date:yyyyMMdd\_HH\_mm\_ss”. You can change the format by rearranging the item order and delimiter type. You can observe this name if you go to the Snapshots tab and include the File Name column using the View ribbon button called \_\_**Choose Columns**.

To reduce the farm load time we recommend unchecking Personal Sites. You can use the load performance slider to switch between low resource usage and a high-performance load.

## Load target

This section allows you to customize how SPDocKit crawls your SharePoint farm. If you know exactly what data you are interested in and want to reduce the loading time, you can narrow down your loading scope to a specific Web application, site collection or even subsite. If you want to be sure you’ve loaded the whole farm's content, farm is the recommended scope.

The selection you make here applies both for the **SPDocKit Service taking an automatic snapshot** and when using the **Default mode** in the Take Snapshot Wizard.

## Data retention

In this section, the user can set how long data will be kept in the database.

{% hint style="info" %}
Data retention settings for audit logs and administrative actions can be defined separately to better suit your recordkeeping requirements.
{% endhint %}

**Data records from the SPDocKit database and on the disk older than the configured time value will be deleted.** By default, **data records are stored for 6 months** before the data retention job removes them. SPDocKit service will execute this job every day at a random time between 4:00AM and 5:00AM.

Set the preferred database size and SPDocKit will warn you when the database size passes that threshold.

If your SPDocKit database becomes too big, you can force a manual data retention using the **Execute** button.

{% hint style="warning" %}
**Please note!**  
This action will also try to execute the SHRINKDATABASE command on your SPDocKit database, which will fail unless you have the necessary permissions – being member of the sysadmin server role or db\_owner database role. Without those permissions, data will still be deleted, but the database size will not decrease. You can still attempt to manually decrease the size of SPDocKit's databases by executing the SHRINKDATABASE command manually after the data retention job has run.
{% endhint %}

{% hint style="warning" %}
**Please note!**  
There is an option to “Mark Configuration as Good”. Marking a snapshot this way will exclude it from the data retention. For more information on this go [here](../create-sharepoint-farm-snapshots/snapshots-screen.md).
{% endhint %}

## Subscription settings

If you wish to use the **Subscriptions and Alerts** feature, check the **Subscriptions Enabled** box. Configure the **job execution time** and the day on which the weekly reports are sent. The **time of day to send subscriptions** option determines at which time the daily, weekly, monthly, and quarterly subscription are sent, while the **Send weekly** subscriptions option only dictates the day on which weekly subscriptions are sent.

To enable **email** as the preferred delivery method, configure outgoing email server settings. After the outgoing email server settings are provided, you can test if these are valid by clicking the **Test Email Settings** button. There is also an option to customize the email footer and email body text.

[Read more about scheduling subscriptions and alerts.](../explore-reports-and-create-documentation/subscriptions-and-alerts/subscriptions-and-alerts.md)

## Compare

From SPDocKit 7.4.0. onwards you can define with which snapshot the current one is compared when detecting configuration changes.

1. **Previous snapshot** - the current snapshot is compared with the last snapshot taken. 
2. **Last good configuration** - with this option selected, the current snapshot is compared with the latest snapshot that is marked as good. 
3. **Selected snapshots** - when this option is selected, you can choose between all your snapshots taken beforehand.

{% hint style="warning" %}
**Please note!**  
If you choose option 2. and there are no snapshots marked as good, SPDocKit will compare the current snapshot to the last snapshot taken. The same rule applies if you choose option 3. and the selected snapshot gets deleted.
{% endhint %}

This section also allows you to define which farm settings should be compared in the Compare Wizard. The selection you make here will be used as a default template when comparing two farms, but you can modify it directly in the Compare Wizard each time you use it.

