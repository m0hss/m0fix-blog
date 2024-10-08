+++
title = 'Deploy Hugo to Vercel Step by Step'
date = 2024-10-06
draft = false
+++

**This guide will walk you through deploying a Hugo website to Vercel. 
I will ensure you avoid at least one common mistake.**
<br>
## 1. Create Your Hugo Site Locally
Assuming Hugo is already installed:

`hugo new site <my-hugo-site>` 

***
## 2. Push Your Hugo Site to GitHub

Then set up a git repository for the site.

`git init`

Add commit and push your project files:

`git add .
git commit
git push -u origin master`


***

## 3.Add a theme for your Hugo site. 

For instance, you can use a Nno jQuery, no Bootstrap super fast theme like [hugo-blog-awesome](https://github.com/hugo-sid/hugo-blog-awesome):

As a github module:
`git submodule add https://github.com/hugo-sid/hugo-blog-awesome.git`

Or a Hugo module
`hugo mod get github.com/hugo-sid/hugo-blog-awesome`

***
## 4. Add vercel configuration (vercel.json)

In root dir add vercel.json where we gonna define hugo version Go version and the buildCommand, after defining hugo as Framework Preset in vercel those config will be auto detected.
<br>
<a name="anchor1">vercel.json</a>
```
{
  "build": {
    "env": {
      "HUGO_VERSION": "0.135.0",
      "GO_VERSION": "1.19.5"
    }
  },
 "buildCommand": "hugo --gc --minify"
}
```
_- use_ `hugo env` _to show versions of Go and Hugo you're using_

Then push update to Github:
`git add .
git commit -m "vercel deploy"
git push -u origin master`

***
##5 . Deploy Your Site on Vercel

During the import process, ensure that the project is connected correctly to your Hugo repository.

Vercel detect env and command build:

![vercel pre build](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/smdpzbyrkgomhsgqki4s.jpg)

Or you ou can set it manually in Vercel environment variables here
![Vercel set env](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/veolvq2z0nd2mofyxmei.jpg)

<br>
Deployement logs:

![deploy logs](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/4y808ll4mp33f34qst4g.jpg)

![Fast deploy](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/81xyhdgsyehfbbcn8a7r.gif)

After a successful build 🎉🎉, Vercel will provide a preview link where you can view your live Hugo website. You can also configure a custom domain through Vercel's settings for your project.
![Vercel deploy ok](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/xwjh5s194k7452xns1pw.jpg)

***
## 6. Add a Domain

If you have a domain name you can add the domain name to the vercel in domains section of the project settings. Then add a CNAME to your domain provider to point to the vercel domain.
***
## 🛠️ _Fix Common Deployment Issues_ 

**The main problem is that hugo support is not that good even if vercel already updated their Node image to have Hugo and with default settings, I met with the error of hugo layout not found and my deployment leads to an XML page. 
This is because the env parameter Hugo and Go versions need to be defined  with in the json file [vercel.json](#anchor1)**

Setting up a personal site with Hugo and Vercel is really easy, despite some minor problems. I hope this post can help you to set up your own site. For more details about the changes I made to the site, see the [commit history](https://github.com/m0hss/m0fix-blog/commits/master/) of [my site](https://tn.m0fix.me/).



![NEGAN GIF](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/2oj35526g1vv8fuftaor.gif)


---
**Some Sources:**
https://vercel.com/guides/deploying-hugo-with-vercel
https://vercel.com/docs/projects/project-configuration
https://blog.gusibi.site/article/Best-Practices-for-Deploying-Hugo-on-Vercel
