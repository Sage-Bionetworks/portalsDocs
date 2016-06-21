# Synapse Documentation

This is a documentation site for [Synapse](https://www.synapse.org). 

## Install Dependencies

With Bundler:

    bundle install 
    npm install

### How to run a development server

    bundle exec jekyll serve

then navigate to [localhost:4000](http://localhost:4000)

### How to regenerate the site

    ./bin/jekyll build

## License & Copyright

Copyright (C) 2014-2016 Alexander Petrov, Michael S. Klishin, Zack Maril, and the ClojureWerkz team.

Distributed under the Eclipse Public License, the same as Clojure.

### Using alert tags

There are four types of alert highlighting to inform users: note, tip, warning, and important. You can insert an alert by using any of the following code in a markdown file. 

{% include note.html content="This is a note." %}

{% include tip.html content="This is a tip." %}

To include new paragraphs, just add the `<br/>` tag within the content, like this:

{% include warning.html content="This is a warning. `<br/>` This is the second line of the warning." %}

{% include important.html content="This is for an important message." %}

### To commit changes 

To avoid a lint error when committing, use:

    git commit --no-verify -m "some message here"