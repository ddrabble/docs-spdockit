---
title: Error: Check if your SQL Server is configured to use a named instance.
description: Configuring SQL Server
author: Mia Tomaić
date: 19/5/2017
---

# Error: Check if your SQL Server is configured to use a named instance.

## Problem:
The wrong database server name has been entered while trying to connect to the database server through the SPDocKit Configuration Wizard.

## Solution:
Check if your SQL server is configured to use a named instance, **e.g.Server/InstanceName**.

1. Run the Microsoft SQL Server Management Studio.
2. Right-click on the preferred server and select **Properties**.
3. Check the full server name, i.e. both server and instance name.
4. Change the server name in the SPDocKit Configuration Wizard according to the name written in the Microsoft SQL Server Management Studio.
5. SQL connection should now be available.