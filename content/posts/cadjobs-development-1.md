+++
author = "Gianluca Cini"
title = "CADJobs.com Development Diary: Planning and Developing a Niche Job Board"
date = "2023-01-17"
description = ""

tags = [
    "cadjobs","business"
]

draft = false

+++

A few months ago I inherited the domain cadjobs.com and decided to launch an aggregator of job offers focused on cad software (autocad, solidworks and the likes)

*check it out here >> [Cad Jobs](https://cadjobs.com) (shameless link building)*

Although the concept of a job board is not new at all and it's frankly even boring in the developer community, I thought launching and growing a web project from scratch would be a good opportunity to grow as a developer 

So after a very short and honestly very superficial market research, i decided to launch this project. 

Here's a few things I've learned after a few months of work

## - Advice 1: Start with the tech stack you are most comfortable with

biggest mistake I made so far is to start the project with technology I was not very familiar with, like a Ubuntu VPS with nginx and a mongoDB database (i choose them because they are very fast™™™™).

turns out it wase a huge waste of time and had a lot of unnecessary problems. So as a .NET Core developer, I decided to go back to a Windows Server with IIS and a SQL Server database. Which is not a very sexy technology but I was very comfortable with it. 

There is always time to change stack and to refactor the code once people start using the product. 

## - Advice 2: Spend more time planning and less time coding

it's not the most fun part of the job, but planning before coding can save lots of time and lots of problems down the line.

coding without planning first is fun, but I had a lot of "oh shit, what about this" moments that forced me to go back and modify existing code, which could have been avoided had I made some planning beforehand.

## - Advice 3: Learn from other people

chances are there are at least a few dozens of people who are working on a similar project as yours, and in those few dozens of people, 2 or 3 of them may have a blog or a twitter account.

Well follow them and learn from them. My project would have been shit had I not learned a few things about job boards from other people.