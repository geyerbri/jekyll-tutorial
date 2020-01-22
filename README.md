# jekyll-tutorial
This repository is for a Jekyll tutorial in CHI at MSU. This guide relies extensively on work done by Jonathan McGlone in his own guide, [Creating and Hosting a Personal Site on GitHub](http://jmcglone.com/guides/github-pages/), including much of the example .css and .html code he provides.

This tutorial assumes the the user has a basic understanding of GitHub's online user interface.

## Tutorial Table of Contents
[Creating and naming the repository](#creating-and-naming-the-repository)
* [URL conventions, branch options, and GitHub Pages](#url-conventions-branch-options-and-github-pages)
* [Repository creation options](#repository-creation-options)

[Managing branches and generating the website](#managing-branches-and-generating-the-website)

[Website Front Page](#website-front-page)
* [index.html](#indexhtml)
* [css/style.css](#cssstylecss)

[Getting started with a GitHub-based Jekyll website](#getting-started-with-a-github-based-jekyll-website)
* [.gitignore](#gitignore)
* [\_config.yml](#_configyml)
* [\_layouts/page.html](#_layoutspagehtml)
* [index.html again](#indexhtml-again)

[Creating a blog.html page](#creating-a-bloghtml-page)
* [\_layouts/post.html](#_layoutsposthtml)
* [\_posts/\[DATE\]-\[ANYTHING\].md](#_postsdate-anythingmd)

["Project Pages site," Liquid tag {{ site.baseurl }}, and Liquid filter {{ "" | relative_url }}](#project-pages-site-the-liquid-tag--sitebaseurl--and-the-liquid-filter----relative_url-)
* [\_layouts/page.html revisited: Liquid tags and Liquid filters](#_layoutspagehtml-revisited-liquid-tags-and-liquid-filters)
* [blog/index.html](#blogindexhtml)

[Customize Blog Post URLs](#customize-blog-post-urls)

[Themes](#themes)
* [\_layouts/page.html revisited again](#_layoutspagehtml-revisited-again)
* [css/style.css revisited](#cssstylecss-revisited)

[GitHub user-created themes](#github-user-created-themes)
* [Remote_theme variable](#remote_theme-variable)

## Creating and naming the repository

Start by creating a new repository.

### URL conventions, branch options, and GitHub Pages
GitHub provides a static website hosting service, called GitHub Pages, which is potentially available for every repository a user might create on the platform. The website will draw from one of the repo's branches, but the options available to choose from for the available branches is determined by the type of repo that has been created. 

For any individual account repository that follows the naming convention \[username].github.io, GitHub will generate a website at https://\[username].github.io. This type of site is called a "User Pages site," the website will generate automatically, and it will (at the moment) only generate from the "master" branch of the repo.

An organizational account repository that follows the convention \[organization].github.io will similarly automatically generate a website at https://\[organization].github.io and only allow reliance on the "master" branch. This type of site is called an "Organization Pages site."

For any individual or organizational repository that has some other naming convention, GitHub will give the option to generate a website at https://\[username].github.io/\[repository-name]. This type of site is called a "Project Pages site" and requires the user (or administrator, in the case of an organizational repo) to enable the website's generation. I will cover a bit about this generation process below.

More information about these conventions can be found on [GitHub's knowledge base](https://help.github.com/articles/user-organization-and-project-pages/).

### Repository creation options
After providing the desired repository name, there are several more options related to repo creation, including an optional description field, a README.md initialization option (which I recommend; every repo should have an explanatory repo, IMO), a .gitignore initialization option, and a copyleft public license generation option. When building a Jekyll site, it would be easier to simply choose "Jekyll" from the list of .gitignore options, but I will still explain the process of manually creating one below. Finally, some users may have either an educational GitHub account or are paying for additional options, in which case they might have the choice between making the repo public or private. These are self-explanatory, but for the purposes of this guide, I will assume users have made their repo public.

## Managing branches and generating the website
Many people find using multiple branches for a repository particularly helpful, especially with keeping unintentional material from being public on one's website. But, for those of us who are building a Jekyll site that may not get much traffic, it would probably be easier to maintain just one repo branch - the "master" branch - and have that one selected as the source for the repo's GitHub Pages website. To generate a website on a project repo, simply navigate to the repo's Settings tab, scroll down to the GitHub Pages section, choose the "master branch" source for the website, and click "Save." Here you can see that "gh-pages" would be another acceptable source - if such a branch exists in the repo - as well as a folder within the "master" branch called "docs." If one would prefer to maintain two branches in the repo, then creating a "gh-pages" branch will automatically generate the website because GitHub's system automatically recognizes this specific branch name as the source of a desired website. A user can, at any time after creating the "gh-pages" branch, change the source setting to either "master" or "docs" inside of "master."
 
## Website Front Page
**Note:** From this point onward, I will refer to the reader's username as \[username] and anyone following this tutorial while building a site in an organizational repository should substitute the organization name (\[organization] above) for the username.

### index.html
Create a file named `index.html` and paste the following code into its body:

```html
<!DOCTYPE html>
<html>
	<head>
		<title>[PAGE TITLE]</title>
		<!-- link to main stylesheet -->
		<link rel="stylesheet" type="text/css" href="css/style.css">
	</head>
	<body>
		<nav>
	    		<ul>
        			<li><a href="/">Home</a></li>
        			<li><a href="/blog">Blog</a></li>
    			</ul>
		</nav>
		<div class="container">
    			<div class="blurb">
        			<h1>Hi there, I'm SOMEONE!</h1>
				<p>Here is some example text. Here is <a href="/about">an example hyperlink</a> to another part of this same website</p>
    			</div><!-- /.blurb -->
		</div><!-- /.container -->
		<footer>
    			<ul>
        			<li><a href="https://github.com/[username]">github.com/[username]</a></li>
			</ul>
		</footer>
	</body>
</html>
```

Change the \[PAGE TITLE] part to whatever you'd like, and replace both instances of \[username] with your own GitHub username. If you follow this guide and notice that the link to "Home" isn't working, please see ["Project Pages site," Liquid tag {{ site.baseurl }}, and Liquid filter {{ "" | relative_url }}](#project-pages-site-the-liquid-tag--sitebaseurl--and-the-liquid-filter----relative_url-) below for a detailed explanation.

### css/style.css
The code above for the index.html file contains a referenced stylesheet. Create this file with the name `css/style.css`. **NOTE:** When a user types a file name and types `/` GitHub automatically detects the name as a directory and adjusts the interface to note that the next part of the name will be for the file, which will be created inside a directory with the just-provided name.

Within the body of `style.css` paste this code:

```css
body {
    margin: 60px auto;
    width: 70%;
}
nav ul, footer ul {
    font-family:'Helvetica', 'Arial', 'Sans-Serif';
    padding: 0px;
    list-style: none;
    font-weight: bold;
}
nav ul li, footer ul li {
    display: inline;
    margin-right: 20px;
}
a {
    text-decoration: none;
    color: #999;
}
a:hover {
    text-decoration: underline;
}
h1 {
    font-size: 3em;
    font-family:'Helvetica', 'Arial', 'Sans-Serif';
}
p {
    font-size: 1.5em;
    line-height: 1.4em;
    color: #333;
}
footer {
    border-top: 1px solid #d5d5d5;
    font-size: .8em;
}
ul.posts { 
    margin: 20px auto 40px; 
    font-size: 1.5em;
}
ul.posts li {
    list-style: none;
}
```
For now, this css file will style the index.html page. This will be enough to view a styled version of your project repo's main page, at `https://[username].github.io/[repository-name]`.


## Getting started with a GitHub-based Jekyll website
Jekyll is a headless content management system - or headless CMS - that allows a user to quickly style new pages and blog posts using Jekyll's centralized layout and theme definitions. Jekyll is especially useful for people who want to write blog posts using Markdown, because it will not only automatically style Markdown (.md) files according to the defined layout and theme, but will also allow users to create a blog main page that will automatically generate a list of posts, using a comparatively light amount of programming.

Deploying Jekyll on GitHub requires creating a number of crucial files that serve to keep GitHub from tracking the wrong parts of the website, that connect one's website with the desired theme, and connects different pages and posts with the appropriate layouts and chosen theme. I will begin with explaining the basics of Jekyll, its required files, and how to use layouts, before I get into picking a GitHub-provided theme or explaining how to use themes created by other GitHub users. (or yourself!)

### .gitignore
The first step to creating a Jekyll website on GitHub is to confirm that the repo contains a .gitignore file. If a Jekyll-specific one was generated during the creation process, then feel free to skip this section. If not, create a new file and name it `.gitignore`. In the body of the file, add this:

```
_site/
```

This tells GitHub's system to ignore any changes that happen in the `_site/` directory that Jekyll automatically creates whenever a change is commited to the repo. Commit this new file.

### \_config.yml
Next, create a new file named `_config.yml` and in its body add the following:

```
title: [WEBSITE NAME]
markdown: kramdown
```

I'll be honest, I do not fully understand why the specific type of markdown - known as kramdown - needs to be specified here, but this is something McGlone includes [in his guide](http://jmcglone.com/guides/github-pages/), so I am including it in mine. kramdown is an MIT-designed version of markdown that GitHub Pages accepts, but their kowledge base explains that [GitHub's markdown is supported by kramdown](https://help.github.com/articles/updating-your-markdown-processor-to-kramdown/), so it is entirely possible that including this designation here is circular. ¯\\\_(ツ)\_/¯

### \_layouts/page.html
As I previously wrote, Jekyll allows a user to create centralized layouts for each type of page within a website. Many tutorials direct readers to create an initial layout named `default.html`, but such a named layout is likely to interfere with some theme chosen in the future, so instead I am directing my readers to use a different initial layout name.

Create another new file in the repository and write its name as `_layouts/page.html` to create the `page.html` file inside a new `_layouts` directory. In the body of this file, paste the following code:

```html
<!DOCTYPE html>
<html>
	<head>
		<title>{{ page.title }} | {{ site.title }}</title>
		<!-- link to main stylesheet -->
		<link rel="stylesheet" type="text/css" href="/css/style.css">
	</head>
	<body>
		<nav>
	    		<ul>
	        		<li><a href="/">Home</a></li>
	        		<li><a href="/blog">Blog</a></li>
	    		</ul>
		</nav>
		<div class="container">
			
			{{ content }}
			
		</div><!-- /.container -->
		<footer>
	    		<ul>
	        		<li><a href="https://github.com/[username]">github.com/[username]</a></li>
			</ul>
		</footer>
	</body>
</html>
  ```

If you notice, much of this is the same as what was pasted into the index.html file, specified above. Once again, replace both instances of \[username] with your own GitHub username, but leave the rest alone for now. This layout will take care of the bulk of the HTML needed to write any given page in the website, so that all is needed in a page that refrences this layout is a little bit of content (which Jekyll will recognize and plug into a generated page at the location occupied by the `{{ content }}` [Liquid tag](https://jekyllrb.com/docs/templates/) in this defined layout).

### index.html again
Now, go back to `index.html`. Replace all of it with the following code:

```jekyll
---
layout: page
title: [PAGE TITLE]
---
<div class="blurb">
	<h1>Hi there, I'm SOMEONE!</h1>
	<p>Here is some example text. Here is <a href="/about">an example hyperlink</a> to another part of this same website.</p>
</div><!-- /.blurb -->
```

In this code, the portion between the two `---` lines is [referred to as the "Front Matter"](https://jekyllrb.com/docs/frontmatter/) and is where a user can specify all sorts of variables and values. Each page should have a at least a defined layout, and often will include a defined title as well (as this one does), but can contain any number of other variables that relate to one's designed Jekyll layout or chosen theme (see below).

The portion of the code below the Front Matter is the previously-referenced content. It should be exactly the same as what was before written inside of the `<div class="container">` container.

## Creating a blog.html page

As I wrote above, Jekyll is used quite extensively as a blog generator because of its ability to centralize webpage layouts and automatically generate lists of certain kinds of files as pages, as well as its ability to turn Markdown (.md) files into styled pages. It does this all for a static site.

### \_layouts/post.html
The first step here is to create a "post" layout, which relies on the "page" layout. Create a new file in the `_layouts` directory, name it `post.html`, and paste in the following code:
```html
---
layout: page
---
<h1>{{ page.title }}</h1>
<p class="meta">{{ page.date | date_to_string }}</p>

<div class="post">
	{{ content }}
</div>
```

### \_posts/\[DATE]-\[ANYTHING].md
Now that the "post" layout exists, it is possible to create a post that relies on the layout for its styling. Each post file must be named as \[YEAR]-\[MONTH]-\[DAY]-\[ANYTHING].md, with \[ANYTHING] being a string of words separated by dashes (`-`). 

First, when creating a new file, type in the new directory name `_posts` and then give an appropriately-formatted post file name. For an example, you could use `2020-01-24-introductory-post.md`. Finally, for its content, paste in the following:
```kramdown
---
layout: post
title: [POST TITLE]
date: [DATE(follow XXXX-XX-XX format, corresponding to YEAR-MONTH-DAY)]
---
This is an example blog post. I am terrible at writing blog posts, so this is pretty much as 'great' as it gets. Notice how this isn't written with HTML, but instead with Markdown (**more specifically**, _GitHub's Markdown_, which works with _kramdown_).
```
The date in the Front Matter and the date specified in the file name _must_ be the same for a Jekyll site to properly detect the post when creating a main blog overview page. The title specified in the Front Matter is what will generate the title used on the blog overview page. Finally, notice that the file itself is a Markdown file (hence the `.md`) and uses Markdown styling for its text.

## "Project Pages site," the Liquid tag {{ site.baseurl }}, and the Liquid filter {{ "" | relative_url }}
At this point, a reader who is using this guide to build a simple "User (or Organization) Pages site" can view this test blog post at https://\[username].github.io/\[repository-name]/year/month/day/\[ANYTHING].html (e.x. `https://[username].github.io/test-repository/2020/01/24/introductory-post.html` for a blog post with the file name `2020-01-24-introductory-post.md`). The Liquid tag and filter mentioned in this section's title aren't strictly needed because such a site has the most basic URL structure possible. 

However, for readers making a "Project Pages site," the Liquid tag and Liquid filter will be crucial to keeping all your relative links within your code working. In fact, if you've been building a "Project Pages site" by following this guide and try to go to the url for the blog post this guide just directed you to create, you will immediately notice that the blog post isn't styled at all, because the browser doesn't have the proper path to the relevant .css file. Additionally, none of the menu links have worked properly up to this point. The Liquid tag and Liquid filter will fix this and will allow for greater flexibility in a site's structure.

### \_layouts/page.html revisited: Liquid tags and Liquid filters
The `page.html` file inside of the `_layouts` directory will need to have its content adjusted to account for any website structure that isn't exactly what is generated for a "User Pages site." To account for the more complex structure, please replace the file's content with this:

```html
<!DOCTYPE html>
<html>
	<head>
		<title>{{ page.title }} | {{ site.title }}</title>
		<!-- link to main stylesheet -->
		<link rel="stylesheet" type="text/css" href={{ "css/style.css" | relative_url }}>
	</head>
	<body>
		<nav>
    			<ul>
        			<li><a href="{{site.baseurl}}">Home</a></li>
        			<li><a href={{ "blog" | relative_url }}>Blog</a></li>
    			</ul>
		</nav>
		<div class="container">
		
			{{ content }}
		
		</div><!-- /.container -->
		<footer>
	    		<ul>
        			<li><a href="https://github.com/[username]">github.com/[username]</a></li>
			</ul>
		</footer>
	</body>
</html>
```

Once more, replace both instances of \[username] with your own GitHub username.

Notice that "Home" has a path of `{{site.baseurl}}`; this is a Liquid tag. Also notice the use of `{{ "" | relative_url }}` for both the path for the stylesheet as well as the link for "Blog" in the site's menu; this is a Liquid filter.

For `{{site.baseurl}}`, this Liquid tag is telling Jekyll to provide the website's known address, which is either its defaulted value, or a value produced by entries in the website's `_config.yml` file. In the case of the default, GitHub Pages sets `site` to `https://[username].github.io` and `baseurl` to `[repository-name]`. Both `site` and `baseurl` can be overwritten in `_config.yml`, such as `site: https://example.com` and `basurl: new-value`. In such an example, using `{{ site.baseurl }}` would produce the value `https://example.com/new-value`. This is useful for those looking to set a custom domain name for the site hosted on GitHub.

For `{{ "" | relative_url }}`, Jekyll will recognize this Liquid filter and prepend the value between the quotation marks with the defined `baseurl` value. For example, in the new code provided for page.html above, Jekyll will define the path for the stylesheet as `[repository-name]/css/style.css`, which will lead to the appropriate location for that file because the layout serves itself from the location `site`.

As an aside, I have used both the Liquid tag and Liquid filter here to introduce both, but it would also be possible to rewrite each instance of their use to rely on one another, in this specific case. For instance, the "Home" path could be rewritten its present `{{site.baseurl}}` Liquid tag as `{{ "." | relative_url }}` or `{{ "/" | relative_url }}`, which are Liquid filters and would all produce the same functional result.

### blog/index.html
Using the knowledge above about where Jekyll positions files in folders that begin with `_`, it becomes possible to adjust code from McGlone's tutorial to work on a "Project Pages site". Create a new file, inside a new `blog` directory (notice the lack of a `_`), name the file `index.html`, and paste this code into the file:
```html
---
layout: page
title: [EXCELLENT MAIN BLOG NAME]
---
<h1>{{ page.title }}</h1>
<ul class="posts">
	{% for post in site.posts %}
	<li><span>{{ post.date | date_to_string }}</span> » <a href="{{ site.baseurl }}{{ post.url }}" title="{{ post.title }}">{{ post.title }}</a></li>
	{% endfor %}
</ul>
```
This code creates a new variable `post` and tells Jekyll that every entry inside the `posts` folder at the `site` location is a `post` value. This will serve up any file found inside `_posts` and create a list out of them. Then, it produces a list of links, which have all of their values defined by the file names and Front Matter. Using `{{ site.baseurl }}` will amend the post's path with the appropriate URL, so that this code will work in cases other than the most basic "User Pages sites" instances.

Creating this file as `index.html` inside of the directory `blog` creates a cleaner-looking URL for its page (`https://[username].github.io/[repository-name]/blog/` as opposed to, say, `https://[username].github.io/[repository-name]/blog.html`), which also segues nicely into an explanation of how to redefine the directory that each post appears to exist within in their URL.

## Customize Blog Post URLs
Jekyll also allows a user to define a directory in which posts appear to reside when looking at their URL. This is done via the `permalink` variable in the repository's `_config.yml` file. Edit this file, and add this line:

```
permalink: /blog/:year/:month/:day/:title
```
Setting this value will make post URLs appear to reside within the `blog` directory, as well as subdirectories defined by the post's year, month, and day, as they are defined in the post's Front Matter and file name (remember from this guide's [\_posts/\[DATE\]-\[ANYTHING\].md](#_postsdate-anythingmd) section, these are all supposed to match). Finally, the page will take its title from the post's file name (which I wrote as \[ANYTHING] above).

## Themes
GitHub Pages provides a number of ready-to-use themes, all of which can be implemented by navigating to the repository's Settings tab, scrolling down to the GitHub Pages section, clicking on "Choose a theme," clicking on the desired theme's thumbnail, and clicking "Select theme." You can confirm that the theme is active by checking for the `theme` variable in your repo's `_config.yml` file.

### \_layouts/page.html revisited again
After enabling a theme, it will be important to again rewrite portions of the "page" layout. Edit the `_layouts/page.html` file and replace its contents with the following code:
```html
---
layout: default
---
<head>
	<!--<link rel="stylesheet" type="text/css" href={{ "css/style.css" | relative_url }}>-->
</head>
<nav>
	<ul>
		<li><a href={{ "." | relative_url }}>Home</a></li>
		<li><a href={{ "blog" | relative_url }}>Blog</a></li>
	</ul>
</nav>
<div class="container">

	{{ content }}

</div><!-- /.container -->
<footer>
	<ul>
		<li><a href="https://github.com/[username]">github.com/[username]</a></li>
	</ul>
</footer>
```

And again, replace both instances of \[username] with your own GitHub username.

By pointing this layout to the "default" layout, Jekyll will implement the GitHub Pages theme's "default" layout site-wide. Additionally, because this layout now relies on the code in the supplied theme, much of the code previously written here is unnecesary, so I have removed it. I have also commented out the stylesheet, because its current code would override the styling done by the theme (but didn't remove it entirely to keep it for use in the next section). 

### css/style.css revisited
If you would like to continue using the stylesheet to style each page's `<nav>` and `<footer>` containers, you could simply remove the surrounding comment in the code above, then alter `css/style.css` to have only code related to `nav ul`, `footer ul`, `nav ul li`, and `footer ul li`. To do this quickly, just replace all of that file with:
```css
nav ul, footer ul {
    padding: 0px;
    list-style: none;
    font-weight: bold;
}
nav ul li, footer ul li {
    display: inline;
    margin-right: 20px;
}
```
## GitHub user-created themes
Many people find the easily-deployable themes provided by GitHub Pages to be undesirable. There are countless other themes available for use on GitHub, produced by other users. To utilize one of these themes, first locate one on github.com and take note of the user's name (\[theme-username]) and repository name (\[theme-repository]).

### Remote_theme variable
Edit your repository's `_config.yml` file and delete any theme variable and its defined value that might exist there. Next, add
```
remote_theme:
```
Set the value of `remote_theme` to the following format: \[theme-username]/\[theme-repository].

Finally, if you would like even more control over a given remote theme, feel free to fork its repository, make any changes you'd like, then direct your Jekyll site to it by defining the remote theme as the one you control: \[username]/\[forked-theme-repository].
