blubars.github.io
=================

Website/blog, via github pages with Jekyll.

## Setup

1. `cd blubars.github.io`
1. Install ruby, perhaps using [asdf](https://github.com/asdf-vm/asdf-ruby): `asdf install ruby 2.7.8`
    1. If using `asdf` to manage ruby versions, the `.tools-versions` file specifies the local version of ruby. Can set another like `asdf local ruby 2.7.8`.
    1. If using `direnv` to manage environment, the `.envrc` file specifies to use asdf.
1. Set up jekyll: https://jekyllrb.com/docs/
    1. `gem install jekyll bundler`
1. Run jekyll: `bundle exec jekyll serve --livereload`
1. Visit http://127.0.0.1:4000
