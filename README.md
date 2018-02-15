# jekyll-tutorial
This repository is for a Jekyll tutorial in CHI at MSU. This guide relies extensively on work done by Jonathan McGlone in his own guide, [Creating and Hosting a Personal Site on GitHub](http://jmcglone.com/guides/github-pages/), including the much of the example .css and .html code he provides.

This tutorial assumes the the user has a basic understanding of GitHub's online user interface.

## Creating and naming the repository

### Naming convention and GitHub Pages
GitHub provides a static website hosting service, called GitHub Pages, which is potentially available for every repository a user might create on their website. The website will draw from one of the repo's branches, but the options available to choose from for the available branches is determined by the type of repo that has been created. 

For any individual account repository that follows the naming convention `[username].github.io`, GitHub will generate a website at `https://[username].github.io`. This type of site is called a "User Pages site," the website will generate automatically, and it will (at the moment) only allow a user to make the "master" branch the collection of files used to generate the website.

An organizational account repository that follows the convention `[organization].github.io` will similarly automatically generate a website at `https://[organization].github.io` and only allow reliance on the "master" branch. This type of site is called an "Organization Pages site."

For any individual or organizational repository that has some other naming convention, GitHub will give the option to generate a website at `https://[username].github.io/[repository-name]`. This type of site is called a "Project Pages site" and requires the user (or administrator, in the case of an organizational repo) to enable the website's generation. I will cover a bit about this generation process below.

More information about these conventions can be found on [GitHub's knowledge base](https://help.github.com/articles/user-organization-and-project-pages/).

### Repository creation options
After providing the desired repository name, there are several more options related to repo creation, including an optional description field, a README.md initialization option (which I recommend; every repo should have an explanatory repo, IMO), a .gitignore initialization option, and a copyleft public license generation option. When building a Jekyll site, it would be easier to simply choose "Jekyll" from the list of .gitignore options, but I will still explain the process of manually creating one below. Finally, some users may have either an educational GitHub account or are paying for additional options, in which case they might have the choice between making the repo public or private. These are self-explanatory, but for the purposes of this guide, I will assume users have made their repo public.

## Managing branches
Many people find using multiple branches for a repository particularly helpful, especially with keeping unintentional material from being public on one's website. But, for those of us who are building a Jekyll site that may not get much traffic, it would probably be easier to maintain just one repo branch - the "master" branch - and have that one selected as the source for the repo's GitHub Pages website. To generate a website on a project repo, simply navigate to the repo's Settings tab, scroll down to the GitHub Pages section, choose the "master branch" source for the website, and click "Save." Here you can see that "gh-pages" would be another acceptable source - if such a branch exists in the repo - as well as a folder within the "master" branch called "docs." If one would prefer to maintain two branches in the repo, then creating a "gh-pages" branch will automatically generate the website because GitHub's system automatically recognizes this specific branch name as the source of a desired website. A user can, at any time after creating the "gh-pages" branch, change the source setting to either "master" or "docs."

## Website Front Page
### index.html
Create a file named index.html and paste the following code into its body:

```html
<!DOCTYPE html>
<html>
	<head>
		<title>[PAGE TITLE]</title>
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
    		<div class="blurb">
        		<h1>Hi there, I'm SOMEONE!</h1>
				<p>Here is some example text. Here is <a href="/about">an example hyperlink</a> to another part of this same website</p>
    		</div><!-- /.blurb -->
		</div><!-- /.container -->
		<footer>
    		<ul>
        		<li><a href="https://github.com/[USERNAME]">github.com/[USERNAME]</a></li>
			</ul>
		</footer>
	</body>
</html>
```

Change the `[WEBSITE TITLE]` part to whatever you'd like, and replace both instances of `[USERNAME]` with your own GitHub username.

### style.css
The code above for the index.html file contains a referenced stylesheet. Create this file with the name `css/style.css`. **NOTE:** When a user types a file name and types `/` GitHub automatically detects the name as a directory and adjusts the interface to note that the next part of the name will be for the file, which will be created inside that directory.

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
Jekyll is a headless content management system - or headless CMS - that allows a user to quickly style new pages and blog posts using Jekyll's centralized layout and theme definitions. Jekyll is especially useful for people who want to write blog posts using Markdown, because it can not only automatically style Markdown (.md) files according to the defined layout and theme, but will also allow users to create a blog main page that will automatically generate a list of posts, using a comparatively light amount of programming.

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
name: [Website Name]
markdown: kramdown
```

I'll be honest, I do not fully understand why the specific type of markdown - known as kramdown - needs to be specified here, but this is something McGlone includes [in his guide](http://jmcglone.com/guides/github-pages/), so I am including it in mine. kramdown is an MIT-designed version of markdown that GitHub Pages accepts, but their kowledge base explains that [GitHub's markdown is supported by kramdown](https://help.github.com/articles/updating-your-markdown-processor-to-kramdown/), so it is entirely possible that including this designation here is circular. Who knows.

### \_layouts/page.html
As I previously wrote, Jekyll allows a user to create centralized layouts for each type of page within a website. Many tutorials direct readers to create an initial layout named `default.html`, but such a named layout is likely to interfere with some theme chosen in the future, so instead I am directing my readers to use a different initial layout name.

Create another new file in the repository and write its name as `_layouts/page.html` to create the `page.html` file inside the `_layouts` directory. In the body of this file, paste the following code:

```html
<!DOCTYPE html>
	<html>
		<head>
			<title>{{ page.title }}</title>
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
	        		<li><a href="https://github.com/[USERNAME]">github.com/[USERNAME]</a></li>
				</ul>
			</footer>
		</body>
	</html>
  ```

If you notice, much of this is the same as what was pasted into the index.html file, specified above. Once again, replace both instances of `[USERNAME]` with your own GitHub username, but leave the rest alone for now. This layout will take care of the bulk of the HTML needed to write any given page in the website, so that all is needed in a page that refrences it is a little bit of content (which Jekyll will recognize and plug into a generated page at the location occupied by the `{{ content }}` [Liquid tag](https://jekyllrb.com/docs/templates/) in this defined layout).

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

In this code, the portion between the two `---` lines is [referred to as the "front matter"](https://jekyllrb.com/docs/frontmatter/) and is where a user can specify all sorts of variables and values. Each page should have a at least a defined layout, and often will includ a defined title as well (as this one does), but can contain any number of other variables that relate to one's designed Jekyll layout or chosen theme (see below).

The portion of the code below the front matter is the previously-referenced content. It should be exactly the same as what was written before as the `<div class="blurb">` container.

### creating a blog.html page
As I wrote above, Jekyll is used quite extensively as a blog generator because of its ability to centralize webpage layouts and automatically generate lists of certain kinds of files as pages, as well as its ability to turn Markdown (.md) files into styled pages.

