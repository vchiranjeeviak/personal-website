---
title: How I setup my personal website in 10 minutes!
---

I was scrolling through youtube and suddenly out of no where I remembered that I setup my personal website some time back. When I opened it, this was the situation 👇

![[Screenshot 2025-02-05 at 12.03.11 AM.png]]

Yes, I used Notion to host my site which is part of the paid plan. I wanted to make a good use of the domain which I already bought long ago. So, I was searching for an easy way to setup a personal website without much hassle and that too for free. I came across this tool called Quartz which helped me set this website up in less than 10 minutes. This is how I did it.

There are 5 steps in this process. 4 are quick and remaining 1 may take some time and optional too.

## 1. Code setup for this ( programming knowledge not required... mostly )

- Install NodeJS version greater than or equal to 20. You can do that from [here](https://nodejs.org/en/download).
- You need to install Git if you already don't have it in your system. Get it from [here](https://git-scm.com/downloads).
- Open terminal or command prompt in your system and run the following commands:
```
git clone https://github.com/jackyzha0/quartz.git
cd quartz
npm i
npx quartz create
```
- You will be prompted to answer two questions for which you can select the default options if you don't understand them ( they are for those who use Obsidian ).

At this point, you are inside the codebase which serves the website to which you are going make changes and use as your own personal website. All you need to do is to run `npx quartz build --serve` to start running. It will give you a url something like `http://localhost:8080`. You can open this in browser and see how it looks.

To customize this from here, you need to know markdown. If you don't know it already, you can learn it. It is just a convention/way of writing text to make it look in certain way. This won't take more than one hour to learn. Once you know markdown, all you need to do is to add markdown files in `content` folder in the codebase that you are in right now.

## 2. Deploy to Github Pages

All you see in the browser with the localhost url can't be shared with others or in internet. It won't work outside of your computer. To make it available to internet, the easiest way is to deploy this to github pages.

- Go to [Github](https://www.github.com) and create a new repository.