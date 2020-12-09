--------------------------------------------------
# The Cmfive site refresh
--------------------------------------------------

Now using Github pages powered by Jekyll
(Commenced 2019)

Features:
 - All documentation can be truly open source - just like Cmfive
 - The site is only comprised of static components (HTML, CSS, JS) with no dynamic parts
   - The advantage of this is that there are minimal security risks
 - Hosting backed by Github
 - Versions of documents are maintained
   - Can be mapped to different versions of Cmfive through the use of branches
 - Editing documentation is much easier to do via the use of pull requests
 - Ongoing effort to update all of the Cmfive documentation and migrate it to this new set up
 - Support for local page development with Docker site hosting

--------------------------------------------------

--------------------------------------------------
# To host this Jekyll repository locally with Docker:
--------------------------------------------------

 - Install Docker including Docker-Compose (at least version 2.1). Install VSCode & MS "Docker for Visual Studio Code" for easy Docker control without CLI.
 - Clone-or-pull-or-download this repository into a local file directory
 - Add your repository to a VSCode workspace, then apply Docker up/down/restart using context menu options by right-click on "docker-compose.yml"

 - or, from your local file directory, run "docker-compose up jekyll tlsproxy", and to quit run "docker-compose down"


	  - The jekyll & tlsproxy services will **serve** pages locally
      - aim your browser at 'localhost:4001' to test pages by http
      - aim your browser at 'https://localhost:4002' to test by https
	     - let your browser accept the self signed cert.

 - note:
	- "docker-compose up jekyll" can work alone, but exposes http:4000 only to Docker "doc_app_net"
	- alternate configurations can be made by declaring new services in "docker-compose.override.yml"
		- eg: uncomment example "httpsjekyll" which is declared per the command line example in general notes below
		- then: docker-compose up httpsjekyll
		- serves only https on localhost:4000, useful to check action of absolute links by site URL
		- or: uncomment example "builddocs" to **build** with fixed URLs for deployment
		- then:  docker-compose up builddocs

--------------------------------------------------

--------------------------------------------------
# General notes on Jekyll framework / implementation
--------------------------------------------------

# Forty - Jekyll Theme

A Jekyll version of the "Forty" theme by [HTML5 UP](https://html5up.net/).

![Forty Theme](assets/images/forty.jpg "Forty Theme")

# How to Use

For those unfamiliar with how Jekyll works, check out [jekyllrb.com](https://jekyllrb.com/) for all the details,
or read up on just the basics of [front matter](https://jekyllrb.com/docs/frontmatter/), [writing posts](https://jekyllrb.com/docs/posts/),
and [creating pages](https://jekyllrb.com/docs/pages/).

- **GitLab**: Simply fork this repository and start editing the `_config.yml` file!
- **GitHub**: Fork this repository and create a branch named `gh-pages`, then start editing the `_config.yml` file.

## Starting Jekyll locally

The config requires SSL be set up, you can comment out that line, or use [mkcert](https://github.com/FiloSottile/mkcert) to generate a local SSL cert then reference them, [with your own PATH_TO_] when you launch Jekyll:

```
$ jekyll serve --ssl-key [PATH_TO_localhost-key].pem --ssl-cert [PATH_TO_localhost].pem --trace --config=_config.yml,_config_development.yml
```

When launching, it's important to specify the ```--config``` option with reference to the ```_config_development.yml``` in addition to the base ```_config.yml``` file. This stops Jekyll setting the base URL to https://cmfive.com.

# Added Features

* **[Formspree.io](https://formspree.io/) contact form integration** - just add your email to the `_config.yml` and it works!
* Use `_config.yml` to **set whether the homepage tiles should pull pages or posts**, as well as how many to display.
* Add your **social profiles** easily in `_config.yml`. Only social profiles buttons you enter in `config.yml` show up on the site footer!
* Set **featured images** in front matter.

# Issues

If you would like to report a bug, ask a question, request a feature, feel free to do so on [the GitLab repository](https://gitlab.com/andrewbanchich/forty-jekyll-theme) and I will be more than happy to help!

Alternatively, you can open an issue via email by emailing [incoming+andrewbanchich/forty-jekyll-theme@incoming.gitlab.com](mailto:incoming+andrewbanchich/forty-jekyll-theme@incoming.gitlab.com).

The GitHub repository is simply a mirror of the GitLab repository.

# Credits

Original README from HTML5 UP:

```
Forty by HTML5 UP
html5up.net | @ajlkn
Free for personal and commercial use under the CCA 3.0 license (html5up.net/license)


This is Forty, my latest and greatest addition to HTML5 UP and, per its incredibly
creative name, my 40th (woohoo)! It's built around a grid of "image tiles" that are
set up to smoothly transition to secondary landing pages (for which a separate page
template is provided), and includes a number of neat effects (check out the menu!),
extra features, and all the usual stuff you'd expect. Hope you dig it!

Demo images* courtesy of Unsplash, a radtastic collection of CC0 (public domain) images
you can use for pretty much whatever.

(* = not included)

AJ
aj@lkn.io | @ajlkn


Credits:

	Demo Images:
		Unsplash (unsplash.com)

	Icons:
		Font Awesome (fortawesome.github.com/Font-Awesome)

	Other:
		jQuery (jquery.com)
		html5shiv.js (@afarkas @jdalton @jon_neal @rem)
		background-size polyfill (github.com/louisremi)
		Misc. Sass functions (@HugoGiraudel)
		Respond.js (j.mp/respondjs)
		Skel (skel.io)
```

Repository [Jekyll logo](https://github.com/jekyll/brand) icon licensed under a [Creative Commons Attribution 4.0 International License](http://choosealicense.com/licenses/cc-by-4.0/).