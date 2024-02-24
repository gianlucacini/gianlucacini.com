+++
author = "Gianluca Cini"
title = "Coding a Strong Internet Blocker (Part 1)"
date = "2021-03-21"
description = ""

tags = [
    "well-being"
]

draft = false
+++

Around the end of the COVID lockdowns, I developed an unhealthy relationship with YouTube, Netflix, and video games. With little else to occupy my time, I found myself spending hours playing video games with friends and scrolling through endless content until the early hours of the morning.

This behavior took a toll on both my mental and physical health, although I recognize that others faced even greater challenges during the pandemic.

Research has shown that excessive screen time can negatively impact well-being. And unfortunately, there are no good solutions on the market that solve this problem. So, armed with this knowledge and after several months of development, I created a minimalistic yet effective internet blocker.

You can find it here
[Link to GitHub](https://github.com/gianlucacini/Unplug)

## Must-Have Feature of an Internet Blocker
What this internet blocker has that most other don't is that it is very hard to bypass. 
Just like your father screaming at you to turn that thing off. I believe this should be a must have for any internet/website blocker.

## How to bypass an internet blocker
There are several ways to bypass an internet blocker:
 - by ending the process from the task manager
 - by uninstalling it
 - by deleting or overriding firewall rules
 - by tampering with your dns
 - by changing the clock of your computer
 - by changing the timezone of your computer
 - by tampering with the file configuration
 - by tampering with the registry

 ## What my internet blocker does once it's running
 - blocks internet using a rule in the firewall, and checks for its existance every 15 seconds, recreating it in case it gets deleted
 - sets process as critical (which forces a system restart if the process is ended from the task manager)
 - stores your timezone in a configuration file and takes the current time from an external NTP server
 - keeps its configuration file open so you cannot tamper with it.
 - starts several process monitors that check wheter you are tampering with the registry or with the service configuration
 - you cannot uninstall it because you cannot stop the service


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


