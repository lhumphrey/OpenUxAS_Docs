# OpenUxAS_Docs
A placeholder for jekyll gh-pages style UxAS documentation

# Steps to use remote themes with jekyll and GitHub pages

Assumption: we are stating from an existing repository and adding a branch `gh-pages`

- From within the repository, create an orphan branch gh-pages that is empty
   - `git checkout --orphan gh-pages`
   - Remove all files in the directory
- Run jekyll in the repository and delete the default files it creates
   - `jekyll new .`
   - `rm -rf _posts; rm about.markdown; rm index.markdown`
- Modify the jekyll gem version in your Gemfile to one supported by GitHub pages
   `gem "jekyll", "~> 4.2.0"` to `gem "jekyll", "~> 3.9.0"
- Follow the instructions on https://github.com/benbalter/jekyll-remote-theme, including:
   - Remove the following from your Gemfile: `gem "minima", "~> 2.5"`
   - Add the following to your Gemfile
      - `gem "jekyll-remote-theme"`
      - `gem "github-pages", group: :jekyll_plugins`
- Run `bundle update jekyll`
- Run `bundle install`
- Update relevant fields in your _config.yml
- Change the following in your _config.yml file
   - `theme: minima` to `remote_theme: rundocs/jekyll-rtd-theme`
- Delete the entries for `baseurl`, `url`, and `github_username`
- Add the following to your _config.yml
```
plugins:
  - jekyll-remote-theme (necessary for using a remote theme)
  - jemoji
  - jekyll-avatar
  - jekyll-mentions

readme_index:
       with_frontmatter: true
```
- Create content in a `README.md` file at the top level
- Run the command `bundle exec jekyll serve`
- As the command instructs, view the results in a browser: http://127.0.0.1:4000/
- Add and commit all files except those in _site (which should be in the .gitignore file anyway)
- Issue command `git push` or `git push --set-upstream origin gh-pages` if this is the first time
- In the settings for the repository, set GitHub pages to point to branch gh-pages
