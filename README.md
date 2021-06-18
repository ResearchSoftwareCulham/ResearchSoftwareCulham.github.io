[![CC BY 4.0][cc-by-shield]][cc-by]

# ResearchSoftwareCulham.github.io
A blog for Research Software at Culham. To become a member of the ResearchSoftwareCulham organisation on Github, please email jonathan.maddock@ukaea.uk.

## Contributing a blog post or page
This site is hosted using [Github Pages](https://pages.github.com/) and is generated using the [Jekyll](https://jekyllrb.com/) static site generator. This means that a Markdown file (with some YAML front matter) on the `master` branch will be automatically published to [researchsoftwareculham.github.io](https://researchsoftwareculham.github.io/) as a blog post or page.

Please see the `CONTRIBUTING.md` for guidance on adding content.

## Setup for serving the site locally
To serve the site locally and preview your changes before committing, you will need to set up Jekyll. The full Gitlab documentation for setting this up can be found [here](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll).

First, [install Ruby](https://www.ruby-lang.org/en/documentation/installation/). On Ubuntu, using `apt`, this is:
```
sudo apt install ruby-full
```

Next, [install Bundler](https://bundler.io/), which manages Ruby gem dependencies:
```
gem install bundler
```

Then navigate to the project root directory and install the required gems:
```
bundle install
```

Then run `jekyll` using Bundler, generating and serving the Jekyll site locally:
```
bundle exec jekyll serve
```

To preview the site in your web browser, navigate to `http://localhost:4000`.

[cc-by]: http://creativecommons.org/licenses/by/4.0/
[cc-by-shield]: https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg