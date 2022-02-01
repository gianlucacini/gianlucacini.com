+++
author = "Gianluca Cini"
title = "How to Block Any (or All) Website You Want on Your Own Windows PC"
date = "2022-01-15"
description = ""

tags = [
    "productivity",
    "health",
    "digital-detox"
]

draft = false

+++

Please stop reading if you are not a .NET developer or if you are inclined to suing people for damaging your pc k thanks.

This is a project from early 2021, I wanted to keep working and eventually start selling this software but then i realized it would be too much of a hassle. 

So now you can find the code on my [GitHub](https://github.com/gianlucacini)

### Y u do dis?
I always wondered why programs or browser extensions that aim at blocking websites and apps are so easy to delete or to find workarounds. 

I mean, they could easily work on a windows account with no Admin privileges, but what if you are not a baby anymore and are on your own computer? 

Is there software that can apply the same restrictions even on an administrator account with all privileges?

### Bill Gates Hates Me! The one secret He doesn't want you to know
Well, apparently the windows kernel has an undocumented function called `RtlSetProcessIsCritical` that, if applied to your windows service, can essentially make it unstoppable. 

This is a sample class 

```
public static class CriticalProcessBase
{
    [System.Runtime.InteropServices.DllImport("ntdll.dll", SetLastError = true)]
    private static extern void RtlSetProcessIsCritical(UInt32 v1, UInt32 v2, UInt32 v3);

    private static void SetProcessAsCritical()
    {
        Log.Information("PROCESS SET AS CRITICAL");
        System.Diagnostics.Process.EnterDebugMode();
        RtlSetProcessIsCritical(1, 0, 0);
    }

    public static void SetProcessAsNotCritical()
    {
        Log.Information("PROCESS SET AS NOT CRITICAL");

        RtlSetProcessIsCritical(0, 0, 0);
    }
}
```

### What does this mean?
it means that you can use this little snippet of code to create your own productivity app, your own parental control app, your own internet blocker app and that you can use it on your account with full admin privileges.

Also please feel free to use my code from two of my 2021 projects.

### Unplug
Unplug is an internet blocker that uses your own firewall to block the internet. 

[Link to GitHub](https://github.com/gianlucacini/Unplug)

[![Unplug Video](https://img.youtube.com/vi/SWtYqL6xvuE/0.jpg)](https://www.youtube.com/watch?v=SWtYqL6xvuE)

### ForceDns
ForceDns is a program that forces your pc to browse the web with a custom DNS.

[Link to GitHub](https://github.com/gianlucacini/ForceDNS)

[![ForceDns Video](https://img.youtube.com/vi/7jko4yOmCnk/0.jpg)](https://www.youtube.com/watch?v=7jko4yOmCnk)


