# valma-docs
Documentation for VALMA model system

The documentation is written for **model users** – people who prepare input data, run scenarios and
interpret results – not for developers of the model code.

The pages are in the [docs](docs) folder and are built as a GitHub Pages site with the
[just-the-docs](https://github.com/just-the-docs/just-the-docs) theme.

## Building the site locally

The repository has no `Gemfile`, so create one before building (it only needs to exist locally):

```
source "https://rubygems.org"
gem "github-pages", group: :jekyll_plugins
gem "jekyll-remote-theme"
```

Then run:

```
bundle install
bundle exec jekyll serve --source docs
```

Alternatively, enable GitHub Pages for the repository and select the `docs` folder as the source.
