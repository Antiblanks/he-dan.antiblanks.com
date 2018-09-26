---
layout: post
title: "Journal system setup with Github Pages"
date: 2018-09-25 08:18:00 +0100
categories: [GAM710]
tags: [Diary, Contextual research]
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

### Taxonomy

Like I mentioned above, my goal is to support the suggested structure of the course which has five modules (categories) and three criteria (sub categories). The structure will look like the following:

> Note: I've added a 'Diary' sub category, I know the guidelines specifically state not to write your journal as a diary but I am including this to record notes in real time so that I can expand those notes into posts for placement in one of the assessed sub categories.

```
|-/GAM710
|--/Diary
|--/Contextual research
|--/Project development
|--/Coursework
|-/GAM720
|--/Diary
|--/Contextual research
|--/Project development
|--/Coursework
|-/GAM730
|--/Diary
|--/Contextual research
|--/Project development
|--/Coursework
|-/GAM740
|--/Diary
|--/Contextual research
|--/Project development
|--/Coursework
|-/GAM750
|--/Diary
|--/Contextual research
|--/Project development
|--/Coursework
```

I looked at using [collections](https://jekyllrb.com/docs/collections/) to facilitate this structure, though this approach would offer me more control over the properties of my vocabulary (categories) and terms (sub categories), there would have been a fair amount of setup with this approach. Fortunately Github Pages ships with post `categories` and `tags` so being this infrastructure already exists I didn't see a need to reinvent the wheel here. I used `categories` as my top level vocabulary (such as the module title `GAM710`) and then `tags` as my vocabulary terms (such as the sub category `Contextual research`). I then wrote my first post and added the following [front matter](https://jekyllrb.com/docs/front-matter/):

```
layout: post
title: "Get set go!"
date: 2018-09-24 22:52:41 +0100
categories: [GAM710]
tags: [Diary]
```

The part we're interested in is this:

```
categories: [GAM710]
tags: [Diary]
```

Unlike other frameworks such as Wordpress where you define your taxonomy as vocabulary and terms first and then relate these to posts, Github Pages works more like a document database in the sense that by adding a category to the `categories` property within a post I am creating a new category if that same category has not already been added to a post.

This is great, as you will see below when I loop through the `categories` to display the menu Github Pages only knows about `categories` that have been used so no dead links. You can add multiple `categories` and `tags` so a post can be related to anything (or nothing):

```
categories: [GAM710, GAM720]
tags: [Diary, Contextual research]
```

### Building the menu

Now that I have my taxonomy nutted out I needed to output the menu. I did this by overriding the default theme `header.html` and introducing the following loop:

{% raw %}
```
{% if site.categories.size > 0 %}
  <li class="site-navigation__menu-item" data-navigation-menu-item>
    <a class="site-navigation__menu-item-link" title="Posts" href="/">Posts</a>
    <ul class="site-navigation__sub-menu" data-navigation-sub-menu>
      {% for category in site.categories %}
        {% assign category_name = category[0] | escape %}
        {% assign category_path = category_name | downcase | replace: ' ', '-' %}
        <li class="site-navigation__sub-menu-item">
          <a class="site-navigation__sub-menu-item-link" title="{{ category_name }}" href="/post-collections/{{ category_path }}">
            {{ category_name }}
          </a>
          {% if site.tags.size > 0 %}
            <ul class="site-navigation__sub-menu">
              {% for tag in site.tags %}
                {% assign tag_name = tag[0] | escape %}
                {% assign tag_path = tag_name | downcase | replace: ' ', '-' %}
                <li class="site-navigation__sub-menu-item">
                  <a class="site-navigation__sub-menu-item-link" title="{{ tag_name }}" href="/post-collections/{{ category_path }}/{{ tag_path }}">{{ tag_name }}</a>
                </li>
              {% endfor %}
            </ul>
          {% endif %}
        </li>
      {% endfor %}
    </ul>
  </li>
{% endif %}
```
{% endraw %}

This part `for category in site.categories` loops through each category and then this nested loop `for tag in site.tags` loops through each tag. The outcome is a menu structure that mimics the taxonomy structure outlined above.

### Creating a layout to display posts by category and tag

Now that I have my menu I needed to display the posts. To do this I created a new layout `posts.html` and added the following code:

{% raw %}
```
---
layout: default
---

{% if page.posts_category and page.posts_tag %}
  {% assign show_by_category_and_tag = true %}
{% elsif page.posts_category %}
  {% assign show_by_category = true %}
{% endif %}

<div class="posts">
  {% if show_by_category_and_tag %}
    <h1 class="page-heading">Posts in '{{ page.posts_category }}' with tag '{{ page.posts_tag }}'</h1>
  {% elsif show_by_category %}
    <h1 class="page-heading">Posts in '{{ page.posts_category }}'</h1>
  {% endif %}

  {% assign has_posts = false %}
  {% if show_by_category_and_tag %}
    <ul class="post-list">
      {% for post in site.posts %}
        {% if post.categories contains page.posts_category and post.tags contains page.posts_tag %}
          {% include post-teaser.html post=post %}
          {% assign has_posts = true %}
        {% endif %}
      {% endfor %}
    </ul>
  {% elsif show_by_category %}
    <ul class="post-list">
      {% for post in site.posts %}
        {% if post.categories contains page.posts_category %}
          {% include post-teaser.html post=post %}
          {% assign has_posts = true %}
        {% endif %}
      {% endfor %}
    </ul>
  {% endif %}

  {% if has_posts == false %}
    {% if show_by_category_and_tag %}
      <p class="post-list-empty">Sorry but there are no posts matching this category and tag :(</p>
    {% elsif show_by_category %}
      <p class="post-list-empty">Sorry but there are no posts matching this category :(</p>
    {% endif %}
  {% endif %}
</div>
```
{% endraw %}

Purists will see some of this code as being cumbersome and I would agree. I spent a while trying to figure out how to make this more dynamic with less conditions but in the end I felt that I was battling against the [Liquid templating engine](https://jekyllrb.com/docs/liquid/) so I settled with this for the time being as it's clean enough and it does the job with room for improvement later.

If you inspect the code you will see that I `show_by_category_and_tag` and `show_by_category`. I am not interested at this point in `show_by_tag` but this could be supported later if required. In short if a `category` and a `tag` are defined by the loading page front matter then I will show posts by category and tag but if only a `category` is defined then I will show by category alone. This enables me to show all posts for a module (`GAM710`) or all posts of type (`Contextual research`) within a module (`GAM710`).

### Adding a page to display some posts

At this point I had put all the tools in place to organise and display posts but I needed a page to actually display some. I did this by using collections which I mentioned earlier. I created a new collection `post_collections` by adding the following to my `_config.yml`:

```
collections:
  post_collections:
    output: true
```

I then created a directory named `_post_collections` by required convention in order to expose pages for that collection. Finally I then created my first page named `gam710.md` by custom convention `{kebab-case-category}-{kebab-case-tag}.md` and added the following front matter:

```
layout: posts
title: App Development Synergies
posts_category: GAM710
permalink: /post-collections/gam710/
```

I then tested this page by visiting the permalink defined in the front matter as `/post-collections/gam710/` and what I could see was a list of all posts that I had created with the category `GAM710`.

Upon following this approach purists will see some of the above as duplication. For each category/tag combination I want to expose I will need to create a new page named by convention `{kebab-case-category}-{kebab-case-tag}.md` and this would result in having a large number of these page files.

This bothered me at first as the purist in me wanted to create one page file and then drive the category/tag by URL parameters, however after much reading I discovered that again I was battling against the constraints of the Liquid templating engine. Also I came to realise that the content in these files was just front matter (data) and in the sense of a document driven data approach it does make some sense to do it this way. I'm not sure I'm 100% convinced of this and will invest more time later to try and better this but for the time being I am happy with this solution.

## Summary

In this post I've documented my reasoning with regard to why I choose to use Github Pages over Wordpress, I've then gone on to describe how to setup a Github Pages website and setup a local development environment with steps to run the website locally. I've then gone on to describe my Devops process and reasons for the components that comprise my chosen workflow. Finally I've gone on to describe some of the customisations I've made to ready my blog for adding and categorising posts. I feel that this meets the requirements for this weeks development task.

## What's next?...

In my next related Journal System post I will go on to implement a better styling solution using [SASS](https://sass-lang.com/) and [BEM](http://getbem.com/) and apply some much needed styling to give my blog some personality.

## References

In alphabetical order:

1. [BEM](http://getbem.com/)
2. [Forking a Github repository](https://help.github.com/articles/fork-a-repo/)
3. [Github](https://github.com/)
4. [Github Pages](https://pages.github.com/)
5. [Git Flow](https://guides.github.com/introduction/flow/)
6. [Jekyll](https://jekyllrb.com/docs/)
7. [Jekyll collections](https://jekyllrb.com/docs/collections/)
8. [Jekyll front matter](https://jekyllrb.com/docs/front-matter/)
9. [LAMP](https://tinyurl.com/3v9uyvm)
10. [Liquid templating engine](https://jekyllrb.com/docs/liquid/)
11. [Markdown](https://en.wikipedia.org/wiki/Markdown)
12. [Pantheon](https://pantheon.io/)
13. [Pull Requests on Github](https://help.github.com/articles/about-pull-requests/)
14. [Ruby](https://www.ruby-lang.org/)
15. [SASS](https://sass-lang.com/)
16. [YAML](https://en.wikipedia.org/wiki/YAML)
