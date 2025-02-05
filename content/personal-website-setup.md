---
title: How I setup my personal website in 10 minutes!
---

I was scrolling through youtube and suddenly out of no where I remembered that I setup my personal website some time back. When I opened it, this was the situation 👇

![[Screenshot 2025-02-05 at 12.03.11 AM.png]]

Yes, I used Notion to host my site which is part of the paid plan. I wanted to make a good use of the domain which I already bought long ago. So, I was searching for an easy way to setup a personal website without much hassle and that too for free. I came across this tool called Quartz which helped me set this website up in less than 10 minutes. This is how I did it.

There are 5 steps in this process. 4 are quick and remaining 1 may take some time and optional too.

## 1. Code setup for this (programming knowledge not required... mostly)

- Install NodeJS version greater than or equal to 20. You can do that from [here](https://nodejs.org/en/download).
- You need to install Git if you already don't have it in your system. Get it from [here](https://git-scm.com/downloads).
- Open terminal or command prompt in your system and run the following commands:
```bash
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
- Now, go to settings and select "pages" on the side menu.
- In the source dropdown, select "Github Actions".
- Go back to terminal and do `rm -rf .git`.
- Create a file with the path `.github/workflows/deploy.yml` and paste this content there:
```yaml
name: Deploy Quartz site to GitHub Pages
 
on:
  push:
    branches:
      - main
 
permissions:
  contents: read
  pages: write
  id-token: write
 
concurrency:
  group: "pages"
  cancel-in-progress: false
 
jobs:
  build:
    runs-on: ubuntu-22.04
    steps:
      - uses: actions/checkout@v4
        with:
          fetch-depth: 0 # Fetch all history for git info
      - uses: actions/setup-node@v4
        with:
          node-version: 22
      - name: Install Dependencies
        run: npm ci
      - name: Build Quartz
        run: npx quartz build
      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: public
 
  deploy:
    needs: build
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4
```
- Run the following git commands:
```bash
git init
git add .
git commit -m "first commit"
git branch -M main
git remote add origin <your repo url>
git push -u origin main
```
- Go back to your github repo page and confirm you can see the same code there.
- You should also see that the build is running when you click on "Actions".

## 3. Custom domain setup (optional)

- If you don't want custom domain, you can use the github provided url to share your website to anyone outside of your system as well. To get this, go to "Pages" menu in Settings and you can see the github provided url for your site. It will be of the form `<github-username>.github.io`
- If you want to use your custom domain which you have bought already, go to your DNS provider dashboard.
- Add 4 "A" records to each of these IP addressess:
```bash
185.199.108.153
185.199.109.153
185.199.110.153
185.199.111.153
```
- Go to "Pages" menu in Github Settings and input your domain name there and click "save".
- It might take some time inorder for your records to propagate, so I suggest you give 5 minutes gap before you do the previous step after adding records.
- Once these steps are successful, you can access your website using your custom domain name.

## 4. Google Analytics setup (optional)

It feels nice to see how many people visited our blog or our website and Google Analytics is one such platform which provides that for free. All you need to do is:

- Go to Google Analytics and create a stream. This will give you a tag id.
- Open `quartz.config.ts` file in the cloned repo, and identify `analytics` object in the config.
- Change the provider to `google` if that is not already there, and add another key in the `analytics` object called `tagId`.
- Give this the same value given by Google Analytics.
- It should look something like this:
```ts
analytics: {
  provider: "google",
  tagId: "G-KDQD9XXXXX"
},
```
- After this, save the file, commit and push to github which will automatically deploy this in few seconds and you can see the results live.


To be honest, I already have lot of things already like, custom domain purchased, Google analytics stream setup, prior programming and hosting knowledge. That is why it was done in 10 minutes. It might take a bit more if you lack any of these. To get started, I don't believe custom domain and analytics are necessary. You can enjoy with github provided url for some time before you setup other lengthy steps. Thanks for reading this far. Bye-bye.