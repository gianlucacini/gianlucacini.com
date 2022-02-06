+++
author = "Gianluca Cini"
title = "How to block any (or all) website on your windows PC (forreal)"
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

I'm presenting you a couple of productivity apps (more specifically a parental control app and an internet blocker) for windows like you've never seen before. 

I wanted to bring forward and eventually monetize this software but I realized it would be too much of a hassle. 

So now you can find the code for both of these apps on my [GitHub](https://github.com/gianlucacini)

### Omg another productivity app? BORING 🥱 

The problem with almost 90% of all these kind of software (browser extensions and desktop software) is that they are very easy to delete or to disarm. 

I'd argue, if you can easily delete or disarm it, what's the point of installing and using it in the first place?

Yes they work great on a windows account with no Admin privileges, but what if you are not a baby anymore and you have your own computer? 

Is there software that can apply the same restrictions even on an administrator account with all privileges?

### Bill Gates Hates Me! The one secret He doesn't want you to know
Well, apparently the windows kernel has an undocumented function called `RtlSetProcessIsCritical` that, if applied to your windows service, can essentially make it unstoppable. 

If you run this method on your program and then terminate it, windows will shut down with it.

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
it means you can use this little snippet of code to create your own productivity app, your own parental control app, your own internet blocker app and that it will work even on an account with full admin privileges.

Please feel free to use my code from two of my 2021 projects.

### Unplug
Unplug is an internet blocker that uses your own firewall to block the internet. 

[Link to GitHub](https://github.com/gianlucacini/Unplug)

[![Unplug Video](https://img.youtube.com/vi/SWtYqL6xvuE/0.jpg)](https://www.youtube.com/watch?v=SWtYqL6xvuE)

### ForceDns
ForceDns is a program that forces your pc to browse the web with a custom DNS.

[Link to GitHub](https://github.com/gianlucacini/ForceDNS)

[![ForceDns Video](https://img.youtube.com/vi/7jko4yOmCnk/0.jpg)](https://www.youtube.com/watch?v=7jko4yOmCnk)


