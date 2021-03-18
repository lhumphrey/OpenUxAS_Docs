# OpenUxAS_Docs
A placeholder for jekyll gh-pages style UxAS documentation

## To start working with this repository locally
- One-time "installation" steps:
   - Install [jekyll and everything else needed to simulate a website](https://jekyllrb.com/docs/)
   - `git clone https://github.com/lhumphrey/OpenUxAS_Docs.git`
   - `cd OpenUxAS_Docs; git checkout gh-pages`
   - `bundle update`
- To interactively edit and view the site
   - `bundle exec jekyll serve`
      - This should serve the website locally at http://127.0.0.1:4000 
      - Enter this address in a browser window
   - Note that updates to the website based on new/removed/edited files will automatically be generated, though you have to refresh the website in your browser to see them
      - Exception: changes to _config.yml
- The theme for this website is based on jekyll-rtd-theme, which has some self-documentation
   - Recommend following the steps of the next section to get a copy of the theme and see demonstrations of its features
   
## To play with features locally in the jekyll-rtd-theme
- One-time "installation" steps:
   - Install jekyll and everything else needed to simulate a website (if you have not already)
   - Create a fork of https://github.com/rundocs/jekyll-rtd-theme.git
   - Clone your fork to your local machine, e.g. `https://github.com/{username}/jekyll-rtd-theme.git`
   - `cd jekyll-rtd-theme`
   - `bundle update`
- To interactively edit and view the site, follow the same steps as in the previous section

## Tips for working with remote themes with jekyll and GitHub pages
- If you push changes to the `gh-pages` branch of this repository back to GitHub, they'll show up at https://lhumphrey.github.io/OpenUxAS_Docs/
- GitHub pages can take a long time to propagate these changes
   - Look at the revision number on the generated website to tell whether the newest changes have been propagated
   - GitHub does seem to email you really quickly if there is a build failure though 

## Steps used to set up gh-pages on a repository like this one (for reference)
Assumption: We are stating from an existing repository and adding a branch `gh-pages`

Steps:
- From within the repository, create an orphan branch gh-pages
   - `git checkout --orphan gh-pages`
   - Remove all files in the directory
- Run jekyll in the repository and delete the default files it creates
   - `jekyll new .`
   - `rm -rf _posts; rm about.markdown; rm index.markdown`
- Modify the jekyll gem version in your Gemfile to one supported by GitHub pages
   - `gem "jekyll", "~> 4.2.0"` to `gem "jekyll", "~> 3.9.0"`
- Follow the instructions on https://github.com/benbalter/jekyll-remote-theme, including:
   - Remove the following from your Gemfile
      - `gem "minima", "~> 2.5"`
   - Add the following to your Gemfile
      - `gem "jekyll-remote-theme"`
      - `gem "github-pages", group: :jekyll_plugins`
- Run `bundle update jekyll`
- Run `bundle install`
- Update relevant fields in your _config.yml
- Delete the following fields in your _config.yml
   - `baseurl`
   - `url`
   - `twitter_username`
   - `github_username`
- Change the following in your _config.yml file
   - `theme: minima` to `remote_theme: rundocs/jekyll-rtd-theme`
- Modify the plugins section of your _config.yml (the first plugin jekyll-remote-theme is necessary, the rest are defaults for the jekyll-rtd-theme)
```
plugins:
  - jekyll-remote-theme
  - jemoji
  - jekyll-avatar
  - jekyll-mentions
```
- Add this to your _config.yml
```
readme_index:
  with_frontmatter: true
```
- Create content in a `README.md` file at the top level
- Run the command `bundle exec jekyll serve`
   - As the command instructs, view the results in a browser: http://127.0.0.1:4000/
- Add and commit all files except those in _site (which should be in the .gitignore file anyway)
- Issue command `git push` or `git push --set-upstream origin gh-pages` if this is the first time
- In the settings for the repository, set GitHub pages to point to branch gh-pages (you only need to do this once)
- You should be able to see the results at [https://lhumphrey.github.io/OpenUxAS_Docs/](https://lhumphrey.github.io/OpenUxAS_Docs/)
   - It can take awhile for results to propagate to GitHub pages
   - The template includes a git revision number, so you can compare the number that shows up on GitHub pages to the one from your most recent push to check whether the most recent changes are being displayed on the site
