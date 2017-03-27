---
author: sagarmattoo
layout: post
title: "Workaround: Proxy authentication issue Azure PowerShell build task for TFS 2015"
description: ""
category: TFS
comments: true
tags:
- Azure PowerShell build task
- TFS 2015 
- Azure Deployment
- Proxy authentication
---

# Issue:-( #
We had been working on setting up a Microsoft Azure PowerShell task on on-Premise TFS 2015 server, however the a NTML proxy sever on the network stood as a wall:-(, not allowing the initial handshake between the task and the Azure Subscription.

Basically, Azure PowerShell build task tries to run **Add-AzureRmAccount** cmdlet which makes a call out to Azure to add an authenticated account to be used for Azure cmdlets and this is where it gets blocked by the proxy. This happens much before entering the custom script passed to the task as parameter.

# Workaround:-) #

Finally, had to go to the basics, we switched to simple PowerShell task instead of Azure PowerShell for doing the initial handshake and passing the default credentials to the proxy. Below is the code snippet we added to our PoweShell scripts:

    [System.Net.WebRequest]::DefaultWebProxy.Credentials = [System.Net.CredentialCache]::DefaultCredentials
    $SecureKey = ConvertTo-SecureString $ServicePricipalKey -AsPlainText -Force
    $secureCredential = New-Object System.Management.Automation.PSCredential($ApplicationId, $SecureKey)
    Add-AzureRmAccount -ServicePrincipal -Tenant $TenantId -Credential $secureCredential

**Note:**

We tried some initial options, but did not work:-(

1. Passing the default fault credentials by adding the following line to the custom PowerShell script that the task runs:	

	`[System.Net.WebRequest]::DefaultWebProxy.Credentials = [System.Net.CredentialCache]::DefaultCredentials`		

2. Passing the proxy credentials through powershell.exe.config.

