# Project Name Documentation

This is a documentation site for [Project Name](). Copy or clone me and adapt for your project
that needs documentation guides similar to [clojureelasticsearch.info](http://clojureelasticsearch.info) and
other ClojureWerkz projects.


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

![alert example](/assets/images/warning_important_alerts.png)

To include new paragraphs, just add the <br/> tag within the content, like this:

{% include warning.html content="This is a warning. <br/> This is the second line of the warning." %}

{% include important.html content="This is for an important message." %}

![alert example2](/assets/images/note_tip_alerts.png)

