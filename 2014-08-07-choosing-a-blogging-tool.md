Title: Choosing a Static Site Generator for Blogs
Date: 2014-08-06
Tags: Blogging

Choosing a blogging tool is not as simple as it seems<!-- PELICAN_END_SUMMARY -->

When I got started with my first blog, I chose Blogger. There were several reasons that helped me make up my mind. It was fairly simple to use, came as a part of Google apps, had a choice of themes, allowed me to assign my own domain name. Analytics were great too.

But it had many shortcomings. Getting it to do syntax highlighting of code was a daunting task. Many people reported being able to do it, but I could never get it to work. Themes and layouts were limited and modifying them was complex. Math typesetting appeared impossible. After using it for 3 years, it was time to look for better solutions. I decided to clarify for myself what I expected from a good blogging tool.

1. **Static site generators v/s blogging engines such as Wordpress et al:** Static site generators (SSGs) are simple, get the job done with the least fuss and generally get out of your way. Comments may need integration with external tools such as Disqus but overall, simple is better.

2. **Code syntax highlighting:** Many posts include code. Displaying code with syntax highlighting is an important requirement.

3. **Typesetting mathematics:** especially in $\LaTeX$ is essential to make posts containing mathematics meaningful and complete.

4. **Theme and layout:** Choosing simple and elegant themes without having to become a web designer is important.

5. **Including IPython Notebooks:** I use IPython Notebooks in my work. Being able to include them in my blog has become an important requirement.

### Static Site Generators
Static site generators provide a framework wherein you write your post in a markup language such as Markdown or reStructured Text and the SSG generates a static web site, complete with navigation, sidebar, categories, tags and archives. They are primarly blogging tools and treat posts in a special chronological way. Some allow creating pages, which are not posts. You also get a user  customizable theme and layout.

[Sphinx](http://sphinx-doc.org/#) does a similar thing, but for documentation and is not suited for a blog. Popular choices appeared to be [Nikola](http://getnikola.com/), [Pelican](http://blog.getpelican.com/) and [Mynt](http://mynt.uhnomoli.com/). Nikola and Pelican have similar features while Mynt lacked the completeness of the other two. These are some of the features Nikola and Pelican have:

1. Themable
2. Navigation, categories, tags, archives, feeds and pages
3. Posts are treated in a special way
4. Allow static pages, which are treated differently compared to posts
5. Support for both Markdown and reST

### Typesetting Math and render_math Plugin for MathJax
Both Markdown and reStructured text can syntax highlight code, but only reST can typeset math. But it is possible to customize Markdown to use MathJax to achieve this. I preferred Markdown so being able to typeset math in Markdown was a requirement. Pelican had a plugin for this purpose, `render_math`. Mynt did not have it, but Andrew Fricke was gracious enough to modify Mynt 0.3 beta to do this. Nikola didn't seem to have a plugin for MathJax. So the choice appeared to be Pelican.

I installed the `render_math` plugin. Initially I had some difficulty understanding how to integrate plugins. I put the configuration code in `settings.py` and it wasn't working at all. Then I realized I should have put that code in `pelicanconf.py`. Then it worked like a charm.

### Theme
I started off with a bare bones Pelican site with the `notmyidea` default theme. While it worked, the theme was not to my taste. I then found the `pelican-bootstrap3` theme and the Bootswatch customization of Bootstrap 3. That helped me make up my mind. I turned off categories from the navigation and created a single static page **About Me** and enabled static pages on the navigation. I chose the Bootswatch United theme which imitates the Ubuntu website.

### Final Verdict
It took me some time to copy paste posts from Blogger and convert them to markdown. I guess I could have found an import from blogger script somewhere, but the articles weren't too many and so I decided to do it manually. MathJax markup and code had to be done manually anyway. And here is the result for you to see. Google analytics is working and Disqus integration is planned. Google AdSense is some way off.

It was a great learning experience. I got to understand better how Jinja2 templates work. I got to get a look into how Bootstrap works. Understood a little bit about integrating MathJax into web pages. All in all, it was worth the time I spent.