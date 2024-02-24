+++
author = "Gianluca Cini"
title = "Blazor Interactive Server Page Speed Optimization (.NET 8)"
date = "2024-02-24"
description = ""

tags = [
    ".net 8", "blazor", "SEO"
]

draft = false

+++

Upon deploying my hobby project, cadjobs.com, I wanted to make sure it worked smoothly for users and search engines. So, I checked its performance using Google's PageSpeed Insights tool.

To my surprise, my website got a shockingly low 14/100 points for performance. 

After a moment of disbelief, I did some research to fix the issues. Here's what I learned:

## Enable WebSocket:
If you're using IIS to host your website, make sure the WebSocket feature is enabled in your Windows Features. Otherwise Blazor will fall back to Long Polling, increasing the time of startup.

## Use Progressive Loading:
Instead of loading all the data at once, especially for long lists on the homepage, load just a bit of it first. Then, let users load more if they want. 
Another option is if you have a long list, you can use the Virtualize component. 
For my site i chose the former method. As i wasn't fully satisfied with how the Virtualize component behaves when using a flexbox layout.

## Make CSS and JS Files Smaller:
To speed up loading times, shrink the size of your CSS and JavaScript files. You can do this by hosting them locally and minimizing them. I used a tool called Bundler Minifier in Visual Studio for this.

## Turn on Response Compression:
With ASP.NET Core, you can compress your website's responses to make them smaller and faster. It's best to use the most effective compression method. According to Microsoft's documentation, the smallest size is achieved by setting compression to  optimal.

After making these changes, my website's performance score shot up to 95/100 on PageSpeed Insights.

I hope sharing these tips helps other developers improve their websites too!

Sources:
 - https://learn.microsoft.com/it-it/aspnet/core/blazor/components/virtualization?view=aspnetcore-8.0 
 - https://marketplace.visualstudio.com/items?itemName=MadsKristensen.BundlerMinifier
 - https://learn.microsoft.com/en-us/aspnet/core/performance/response-compression?view=aspnetcore-8.0
