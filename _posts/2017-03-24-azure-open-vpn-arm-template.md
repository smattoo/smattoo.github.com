---
author: sagarmattoo
layout: post
title: "Azure OpenVPN ARM template"
description: ""
category: VPN
comments: true
tags:
- Azure ARM
- OpenVPN
- by-pass Proxy
---


 Want to access the Internet safely and securely by-passing the proxy servers, here's an Azure ARM template to setup an OpenVPN server within couple of minutes.

**Prerequisites**

- Microsoft Azure Subscription with some credits:-)

**Clients**

- Tested for [OpenVPN 2.4.1 and 2.3.14](https://openvpn.net/index.php/open-source/downloads.html "OpenVPN client download") clients on Windows 8.1 and above.

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fsmattoo%2Fopenvpn-azure-arm-template%2Fmaster%2Fopenvpn-azuredeploy.json" target="_blank">
    <img src="http://azuredeploy.net/deploybutton.png"/>
</a>
<a href="http://armviz.io/#/?load=https%3A%2F%2Fraw.githubusercontent.com%2Fsmattoo%2Fopenvpn-azure-arm-template%2Fmaster%2Fopenvpn-azuredeploy.json" target="_blank">
    <img src="http://armviz.io/visualizebutton.png"/>
</a>

**Github:** [source](https://github.com/smattoo/openvpn-azure-arm-template "GitHub link") 

The template provisions an Ubuntu 16.04 vm and sets up the OpenVPN server. Post deployment of the template, you just need to download the **.ovnpn** configuration file and pass the same to the OpenVPN client running on your machine.

That's it you now have established a private tunnel to access the internet.
  


