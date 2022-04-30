# priceandposition
Mixed business and tech blog in PaperMod theme on Hugo (gohugio.io).

Updated and now using Go 1.18.1 and Hugo 0.97.0 (2022-4-29).

Create a new site:
- hugo new site myblog -f yml // yml instead of toml for configuration
- git submodule add --depth=1 https://github.com/adityatelange/hugo-PaperMod.git themes/PaperMod
- git submodule update --init --recursive 

or cloned:

- git clone this site
- git submodule add --depth=1 https://github.com/adityatelange/hugo-PaperMod.git themes/PaperMod
- git submodule update --init --recursive 

In either case, to work locally:
- hugo serve 
- open browser to http://localhost:1313
- posts are at content/post/<topic>.md
- main configuration is in config.yml (config.toml)
- More info, see Aditya Telange https://adityatelange.github.io/hugo-PaperMod/posts/papermod/papermod-installation/

Build, push, deploy:
- hugo      // build the site (so fast it looks like nothing happened)
- git add .
- git commit -m '<commit_message>'
- git push origin main  // push to Github deploys to Netlify

To deploy to Netlify:
- Assuming a project repo on Github - on Netlify: "New site from Github" and select the repo .
- Netlify should automatically identify this as a Hugo repo for the "build" command.
- Click "deploy site" start the deploy.
- a random "<xyz>.netlify.com" subdomain is attached to the site.
- Also, in settings, set to PRODUCTION and Hugo version to 0.97.0
- You can see the build happening in "Overview" panel) of the site.
- Once the random Netlify name version is working, add your domain name to the configuration (from Namecheap, etc.)
- Assuming you have a domain name from Namecheap etc., Netlify can create an https connection using Letsencrypt for free (cool!).

Now local development changes that are built and pushed are deployed automatically! Yay!

