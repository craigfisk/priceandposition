# priceandposition
Mixed business and tech blog in PaperMod theme on Hugo (gohugio.io).

Create a new site
- hugo new site myblog
- see Flavio Copes "config.toml" in freecodecamp.org as a model

or

- git clone the site
// add forked submodule; see: https://www.andrewhoog.com/post/git-submodule-for-hugo-themes/
- git clone https://www.andrewhoog.com/post/git-submodule-for-hugo-themes/
- hugo serve
- open browser to http://localhost:1313
- posts are at content/post/<topic>.md
- If you get an error like 'found no layout file for "HTML" for layout "archives" for kind "page"',
then per
- See Aditya Telange: tested a new site with config.yml and instructions mentioned at https://adityatelange.github.io/hugo-PaperMod/posts/papermod/papermod-installation/
- So I forget why, but you wan to do this:
git submodule update --init --recursive
- Also, for PaperMod, config.toml must be converted to config.yml.  See Aditya Telange's documentation.

Netlify settings:
- PRODUCTION, Hugo version 0.97.0
To deploy to Netlify:
- create a project repo on Github
- on Netlify: "New site from Github" and select the repo 
- Netlify should automatically identify as a Hugo repo for the "build" command.
- Click "deploy site" start the deploy
- a random ".netlify.com" subdomain is attached to the site
- use this to see the site live.

Now local changes are deployed automatically:
- local changes
- push to Github
- Netlify automatically updates site (you can see the build happening in "Overview" panel) of the site.

