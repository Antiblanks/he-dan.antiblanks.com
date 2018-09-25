---
layout: post
title: "Journal system setup with Github Pages"
date: 2018-09-25 08:18:00 +0100
categories: [GAM710]
tags: [Diary]
---

## Why Github Pages?

So this part of the post is an expansion on my earlier sweeping statement [here]({% post_url 2018-09-24-get-set-go %}) that goes nowhere to illustrate why I've decided to use [Github Pages](https://pages.github.com/) over Wordpress. I slept on it and felt that I needed to clarify my decision to some degree and in doing so might be able to document my learnings and help others along when making the same choice.

If you're here then you're probably reading or have probably read the **Journal System Setup** page in [Falmouth University Canvas](https://falmouthflexible.instructure.com/), you've got to the bit that reads **What platform should I use?** and you are faced with two suggested options 'Wordpress' or ['Github Pages'](https://pages.github.com/). As it rightly states:

> There are other blogging platforms available, which you are welcome to choose instead.

And there *are* a whole plethora of these and, while they all set out to do roughly the same thing, the tech and approach behind them is quite different. In my opinion choosing the right blogging engine is about you and your existing skillset or the skillset you want to develop. So let's look at those two options:

### Wordpress

Wordpress is built on a [LAMP](https://tinyurl.com/3v9uyvm) system. In short this means that it comprises of 'Linux', 'Apache', 'MySQL' and 'PHP'. When I said in my previous post that:

> Using Wordpress seemed a little old fashioned and ever so slightly contradictory...

I was actually being a little unfair, LAMP is a great system and one that when developed in a progressive manor (using Symfony or Laravel) can be both modern, relevant, scale well, and in fact is a system we use on many small to middle sized projects at [Antiblanks](http://www.antiblanks.com).

Updates to your Wordpress will be performed by way of using their admin system and creating your posts using a **WYSIWYG** editor. The setup is quite painless *if* you choose to have it hosted by Wordpress themselves or self host with [Pantheon](https://pantheon.io/).

There are a vast amount of themes to choose from and plugins to enrich your experience. All sounds great right? And it is for someone who wants to control their journal via a **CMS** and not want to get too heavily involved in the code base...

The problem for me with Wordpress is that I've been using it for well over a decade and I'm well versed in LAMP development and being that the industry is saturated with Wordpress developers which has diluted the day rate for this type of work, I don't think it's a system I would choose to learn in 2018.

### Github Pages

Github Pages is built on [Ruby](https://www.ruby-lang.org/) and utilises [Jekyll](https://jekyllrb.com/). Both are more modern and in my opinion the approach with Github Pages is more progressive. First of all it's super easy to host because [Github](https://github.com/) takes care of that for you. It's also easy to deploy because you simply define a production branch and when you push code into that branch it will automatically deploy to your production site. This is much more like real world modern development pipelines and encourages you to think in a more industry modern way.

Using something like [Git Flow](https://guides.github.com/introduction/flow/) to govern your workflow will introduce you to the sensibility and practicality of using a good branching structure and in my experience give you some notion of how to develop as part of a wider team.

Creating content for a Github Pages site is done in a more front end focused approach and the data is driven by [YAML](https://en.wikipedia.org/wiki/YAML) and the content by [Markdown](https://en.wikipedia.org/wiki/Markdown). These tools are more widely used now and in my opinion more valuable in 2018.

The approach is also more document driven and as a consequence is arguably easier to re-structure the taxonomy, and being I'm not sure how the structure will grow I want to be able to change it easily later without being restricted by the data and relationships being baked into a database.

Finally, from a personal point of view, I have some experience with YAML and Markdown but it's limited and it could be improved so this is why I've decided to use Github Pages.

## Setting up a Github Pages website on Github

After making the decision to use Github Pages it was time to do some reading and figure out how to create my first Github Pages website. Thankfully the process is very simple and the [Github Pages documentation](https://pages.github.com/) will guide you through this in no time. This will be much easier to digest if you've worked with Git and Github before, if you haven't it might take a little more to time to get your head around this.

In short you need to create a Github repository and adjust the settings to expose the `master` branch as a GitHub Pages site. There are a couple of other options such as creating a custom domain which is a bit more complicated but can be achieved by reading the documentation in the GitHub Pages section of your repositories settings.

> Note: Creating a custom domain does require some understanding of Domain Name Servers (DNS). I remember when I started experimenting with DNS it was quite confusing. In hindsight I can assure you it's not that complicated, but if you've no experience with this you may need to do some reading to understand the basics before attempting this.

Once you've setup your Github Pages website you just need to clone the repository and you'll have a very basic site on which you can make changes to add the content for your blog.

Alternatively (for ease of getting started) I've created a boilerplate of my blog with the default (suggested) taxonomy preconfigured and a basic theme applied which is ready for creating posts and applying custom styling. To fork my repository please read this [help article](https://help.github.com/articles/fork-a-repo/).

## Setting up your local environment for development

Now that you have your website on your local machine you will need to get setup for development. As I mentioned before, Github Pages websites are built with Ruby and Jekyll so you need to install both of these first. For more information checkout the [Ruby](https://www.ruby-lang.org/en/documentation/) and [Jekyll](https://jekyllrb.com/docs/) documentation.

I already had Ruby installed from working on previous projects and the Ruby documentation mentioned above offers an easy way to check if you already have this. Bear in mind that Jekyll requires Ruby so you'll need to install Ruby first before attempting to install Jekyll. If you have forked my repository you will not need to install Jekyll as it is included in the project `GemFile`. The instructions in the **Running the website locally** section below explain this in more detail.

> Note: This is not a necessity but if you are looking to develop on more than one Ruby website in future then you may run into version mismatches where one project requires a different version of Ruby than the other. Rather than constantly updating projects and bundles to sync with your global version of Ruby it's worth taking the time to install a version manager such as [RVM](https://rvm.io/) which will allow you to switch your version of Ruby easily dependent upon the project you are working on.

## Running the website locally

For those of you not experienced in web development, it's pretty standard to develop locally first and then deploy your changes to online environments for testing, preview and then production afterwards. There are many different workflows to consider and this is commonly known as Devops. I will touch upon this more below. For now, we just need to get the site running locally for development.

Running the website locally is very straight forward. Following the Jekyll documentation I was up and running in no time, assuming you've forked my repository into a local directory named `hedanandthemastersdegree.blog.starter` this is just a matter of following the below steps:

Change directory into the project root on your local machine:
```
cd ./hedanandthemastersdegree.blog.starter
```

Update all Ruby Gems:
```
bundle update
```

Run the local development environment:
```
bundle exec jekyll serve
```

Browse your local site [here](http://localhost:4000/).

## Devops and deployment

Now that you have your site running locally you need to think about how you will make, test and deploy your changes. This is all part of your workflow and Devops.

Based on the size and nature of the project you may have all manor of Devops in place to support your workflow. You may also have different online environments such as (for example) `Development` (for integrated developer testing), `Staging` (for quality assurance [QA]) and `Production` (for your public facing website).

For purpose of this website, being there is only one developer (me), no external QA team and the audience is mainly isolated to a small internal focus group, I am going to have a minimal yet appropriate workflow.

> In my opinion it's always worth having some Devops process even if you are the only developer on a project. Having a structure in place helps you to write and ship better code and have less bugs in your deployments.

I will be using an approach inspired by [Git Flow](https://guides.github.com/introduction/flow/). I will develop locally in `feature` branches and then create [pull requests](https://help.github.com/articles/about-pull-requests/) (PR's) to review my code and merge changes into an `integration` branch. This branch is where I will perform my own QA before creating a PR to merge my complete and verified changes to `master` which in turn will deploy my website to production.

## Adapting the default Jekyll theme to add the default taxonomy

As stated in the **How should I structure my blog?** section of the **Journal System Setup** page in Falmouth University Canvas, we will need to 'logically arrange our blog so posts that relate to certain things and are filed in a particular category', they then go on to suggest a structure and as a starting point I've decided to take this advice and structure my taxonomy to support this approach. Here's how I did this:

...

## Summary

In this post I've documented my reasoning with regard to why I choose to use Github Pages over Wordpress, I've then gone on to describe how to setup a Github Pages website and setup a local development environment with steps to run the website locally. I've then gone on to describe my Devops process and reasons for the components that comprise my chosen workflow. Finally I've gone on to describe some of the customisations I've made to ready my blog for adding and categorising posts. I feel that this meets the requirements for this weeks development task.

## What's next?...

In my next related Journal System post I will go on to implement a better styling solution using [SASS](https://sass-lang.com/) and [BEM](http://getbem.com/) and apply some styling to give my blog some personality.

## References

In alphabetical order:

1. [BEM](http://getbem.com/)
2. [Forking a Github repository](https://help.github.com/articles/fork-a-repo/)
3. [Github](https://github.com/)
4. [Github Pages](https://pages.github.com/)
5. [Git Flow](https://guides.github.com/introduction/flow/)
6. [Jekyll](https://jekyllrb.com/docs/)
7. [LAMP](https://tinyurl.com/3v9uyvm)
8. [Markdown](https://en.wikipedia.org/wiki/Markdown)
9. [Pantheon](https://pantheon.io/)
10. [Pull Requests on Github](https://help.github.com/articles/about-pull-requests/)
11. [Ruby](https://www.ruby-lang.org/)
12. [SASS](https://sass-lang.com/)
13. [YAML](https://en.wikipedia.org/wiki/YAML)
