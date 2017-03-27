---
author: sagarmattoo
layout: post
title: "Workaround: Proxy authentication issue Azure PowerShell build task for TFS 2015"
description: ""
category: TFS
comments: true
tags:
- Azure
- TFS 2015 
- PowerShell
- Proxy Authentication
- http-status-code-407
---

## Issue:-( ##
We had been working on setting up a Microsoft Azure PowerShell task on on-Premise TFS 2015 server, however the a NTML proxy sever on the network stood as a wall:-( not allowing the initial handshake between the task and the Azure Subscription.

Basically, Azure PowerShell build task tries to run **Add-AzureRmAccount** cmdlet which makes a call out to Azure to add an authenticated account to be used for Azure cmdlets and this is where it gets blocked by the proxy. This happens much before entering the custom script passed to the task as parameter.

## Options Tried:-( ##
Tried some initial options like, but didn't work:-(

Passing the default credentials by adding this `[System.Net.WebRequest]::DefaultWebProxy.Credentials = 
[System.Net.CredentialCache]::DefaultCredentials` to the custom PowerShell script that the task runs	  

Passing the proxy credentials through powershell.exe.config.

## Workaround:-) ##

Finally, had to go to the basics, we switched to simple PowerShell task instead of Azure PowerShell for doing the initial handshake and passing the default credentials to the proxy. Below is the code snippet we added to our PowerShell scripts(you would need to pass TenantId, ApplicationId, ServicePrincipleKey as params to the script):

    [System.Net.WebRequest]::DefaultWebProxy.Credentials = [System.Net.CredentialCache]::DefaultCredentials
    $SecureKey = ConvertTo-SecureString $ServicePricipalKey -AsPlainText -Force
    $secureCredential = New-Object System.Management.Automation.PSCredential($ApplicationId, $SecureKey)
    Add-AzureRmAccount -ServicePrincipal -Tenant $TenantId -Credential $secureCredential

