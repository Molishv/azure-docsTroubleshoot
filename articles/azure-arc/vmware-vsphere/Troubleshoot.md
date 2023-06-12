
---
title: Troubleshoot Azure Arc enabled VMware vSphere (preview) issues
description: This article tells how to troubleshoot and resolve issues when using "Arc enabled VMware vSphere" service.
ms.date: 03/15/2023
ms.topic: conceptual
---

# Troubleshoot Azure Arc enabled VMware vSphere (preview) issues

This article provides information on troubleshooting and resolving issues that may occur while attempting to use, or remove the Azure Arc enabled VMware vSphere (preview). 
## Enable guest management related issues

### Domain-joined Linux Guest VM
For enabling Guest Agent on a Linux VM using active directory credentials (i.e., the Linux VM is domain-joined and some domain user credentials were supplied for PUT Guest Agent), the following configuration needs to be done on the VM by the user before enabling Guest Agent:

In the SSSD configuration file (typically /etc/sssd/sssd.conf), we need to add the following line under the section for the domain:

```azurecli
[domain/contoso.com]
ad_gpo_map_batch = +vmtoolsd
```
After making the changes to SSSD configuration, we need to restart the SSSD process. If SSSD is running as a systemd process, we can run ```sudo systemctl restart sssd``` to restart it.
