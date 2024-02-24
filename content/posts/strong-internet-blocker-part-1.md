+++
author = "Gianluca Cini"
title = "Coding a Strong Internet Blocker (Part 1)"
date = "2021-03-21"
description = ""

tags = [
    "well-being", "side-projects"
]

draft = false
+++

Around the end of the COVID lockdowns, I developed an unhealthy relationship with YouTube, Netflix, and video games. With little else to occupy my time, I found myself spending hours playing video games with friends and scrolling through endless content until the early hours of the morning.

This behavior took a toll on both my mental and physical health, although I recognize that others faced even greater challenges during the pandemic.

Research has shown that excessive screen time can negatively impact well-being. And unfortunately, there are no good solutions on the market that solve this problem. So, armed with this knowledge and after several months of development, I created a minimalistic yet effective internet blocker.

You can find it here
[Link to GitHub](https://github.com/gianlucacini/Unplug)

## Must-Have Feature of an Internet Blocker

What sets this internet blocker apart from most others is its high level of resistance to bypassing. It's akin to your father sternly ordering you to switch off that device. I believe this feature should be a necessity for any internet or website blocker.

## How to Bypass an Internet Blocker

There are several methods to bypass an internet blocker:

 - Terminating the process from the task manager
 - Uninstalling it
 - Deleting or overriding firewall rules
 - Tampering with your DNS
 - Changing the clock of your computer
 - Changing the timezone of your computer
 - Tampering with the file configuration
 - Tampering with the registry

## What My Internet Blocker Does Once It's Running

 - It blocks internet access using a firewall rule and checks its existence every 15 seconds, automatically recreating it if deleted.
 - It sets the process as critical, forcing a system restart if the process is terminated from the task manager.
 - It stores your timezone in a configuration file and retrieves the current time from an external NTP server.
 - It keeps its configuration file open to prevent tampering.
 - It initiates several process monitors to detect any attempts to tamper with the registry or service configuration.
 - You cannot uninstall it because you cannot stop the service.

## Code Components

### Snippet to set process as critical
how is this even legal idk

 ```csharp
[System.Runtime.InteropServices.DllImport("ntdll.dll", SetLastError = true)]
private static extern void RtlSetProcessIsCritical(UInt32 v1, UInt32 v2, UInt32 v3);

//sets process as critical
RtlSetProcessIsCritical(1, 0, 0);

//sets process as not critical
RtlSetProcessIsCritical(0, 0, 0);
```

### Snippet to create Firewall Rule
 ```csharp
 using NetFwTypeLib;

INetFwRule firewallRule = (INetFwRule)Activator.CreateInstance(Type.GetTypeFromProgID("HNetCfg.FWRule"));
firewallRule.Action = NET_FW_ACTION_.NET_FW_ACTION_BLOCK;
firewallRule.Description = "This rule blocks internet connection.";
firewallRule.Direction = NET_FW_RULE_DIRECTION_.NET_FW_RULE_DIR_OUT;
firewallRule.Enabled = true;
firewallRule.InterfaceTypes = "All";
firewallRule.Name = "Rule Name";
 ```

### Snippet to Get Set Registry Values 

 ```csharp

String subkeyPath = $@"SYSTEM\CurrentControlSet\Services\Internet Blocker Service\";

//get registry key values
var keys = Microsoft.Win32.Registry.LocalMachine.OpenSubKey(subkeyPath, true);


//set registry key values
//create key
Microsoft.Win32.Registry.LocalMachine.CreateSubKey(subkeyPath, true);

//open key
browserKeys = Microsoft.Win32.Registry.LocalMachine.OpenSubKey(subkeyPath, true);

//create subkey
browserKeys.SetValue("keyName", "keyValue");

browserKeys.Close();

 ```


