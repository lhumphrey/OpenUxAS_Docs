# OpenUxAS_Docs
A placeholder for jekyll gh-pages style UxAS documentation

## Tips for working with remote themes with jekyll and GitHub pages
- The remote theme jekyll-rtd-theme we will use is self-documented [here](https://jekyll-rtd-theme.rundocs.io)
   - I recommend downloading the files for the theme so you can see how they did things
   - This is [their download link](https://github.com/rundocs/jekyll-rtd-theme/zipball/develop)
- GitHub pages can take a long time to propagate changes
   - Look at the revision number on the generated website to tell whether the newest changes have been propagated
   - GitHub does seem to email you really quickly if there is a build failure though 

## Steps to use remote themes with jekyll and GitHub pages

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
