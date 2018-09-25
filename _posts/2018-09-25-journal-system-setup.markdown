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

## Setting up the website

Like I mentioned before, Github Pages are built with Ruby and Jekyll so you'll need to install those first. For more information checkout the [Ruby](https://www.ruby-lang.org/en/documentation/) and [Jekyll](https://jekyllrb.com/docs/) documentation.

> For Mac users it's very simple as your computer will likely have Ruby installed. Bear in mind that Jekyll requires Ruby so you'll need to install Ruby first.

## Running the website locally

For those of you not accustomed to web development and common Devops, it's pretty standard to develop locally first and then deploy changes to an online environment for testing.

Based on the size and nature of the project you may have all manor of Devops in place to support your workflow and with these will come several environments such as `Development`, `Staging` and `Production` (just for example). For purpose of this website, being that there is no external quality assurance (QA) and the audience is mainly isolated to an internal focus group, I am going to develop locally in `feature` branches and then create PR's (Pull Requests) to review my code and merge the changes into an `integration` branch. This branch is where I will perform my own QA before creating a PR to merge my complete and verified changes to `master` which in turn will deploy my website.

Running the website locally is really straight forward. Following the Jekyll documentation I was up and running in no time. I've created a public starter project to make this easy. The starter has my default taxonomy setup and is ready to start creating categorised posts. There will be more on this later.

To run the website locally:

Checkout the site from my public repository:
```
git clone https://github.com/Antiblanks/hedanandthemastersdegree.blog.starter.git
```

Change directory into the project root:
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

## Adapting the theme to add the default taxonomy

TODO: Add content here for the adapting the theme and inclusion of the ...

## The source code

TODO: Add the public source code repos here...
