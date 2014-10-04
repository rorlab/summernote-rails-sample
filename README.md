# Sample Rails 4 Project for Summernote-rails v0.5.10

## Development Environment

* Mac OSX 10.9.5
* Ruby 2.1.3
* Rails 4.1.6

## Installation

Add the following gems to your application's Gemfile:

```ruby
gem 'simple_form'

# You'll need to include the following dependencies of Summernote
gem 'bootstrap-sass'
gem "font-awesome-rails"

# This is the right gem to use summernote editor in Rails projects.
gem 'summernote-rails'
gem 'codemirror-rails'

# To solve the problems on the turbolinks
gem 'jquery-turbolinks'
```

And then execute:

```
$ bundle install
```

## Usage

First of all, the summernote editor works on Bootstrap and so it is assumed that you have already set it up.


In app/assets/stylesheets/application.css.scss,

```
// Bootstrap 3
@import "bootstrap";
@import "font-awesome";
@import "summernote";
@import "codemirror";
@import "codemirror/themes/solarized";
@import "posts";
body {padding-top:3em;}
```

In app/assets/javascripts/application.js, you should add the following:

```
//= require jquery
//= require jquery.turbolinks
//= require jquery_ujs
//= require bootstrap
//= require codemirror
//= require codemirror/modes/ruby
//= require codemirror/modes/sass
//= require codemirror/modes/shell
//= require codemirror/modes/sql
//= require codemirror/modes/slim
//= require codemirror/modes/nginx
//= require codemirror/modes/markdown
//= require codemirror/modes/javascript
//= require codemirror/modes/http
//= require codemirror/modes/htmlmixed
//= require codemirror/modes/haml
//= require codemirror/modes/xml
//= require codemirror/modes/css
//= require codemirror/modes/yaml
//= require codemirror/modes/slim
//= require codemirror/modes/php
//= require summernote
//= require lang/summernote-ko-KR
//= require_tree .
//= require turbolinks
```

For example, if you made a `Post` model using `scaffold generator` of Rails, you would see the `post` form view template in app/views/posts/_form.html.erb.

In that template file, you should add `summernote` class to the textarea input as the following:

```
<%= simple_form_for(@post) do |f| %>
  <%= f.error_notification %>

  <div class="form-group">
    <%= f.input :title, input_html:{class:'form-control'} %>
  </div>
  <div class="form-group">
    <%= f.input :content, class:'summernote' %>
  </div>

  <div class="form-group">
    <%= f.button :submit, class:'btn btn-default' %>
  </div>
<% end %>
```

And then, in `post`-dedicated coffeescript file, app/assets/javascripts/posts.js.coffee, you should add the following:

```
$ ->

  # to set summernote object
  # You should change '#post_content' to your textarea input id
  summer_note = $('#post_content')

  # to call summernote editor
  summer_note.summernote
    # to set options
    height:500
    lang: 'ko-KR'
    codemirror:
      lineNumbers: true
      tabSize: 2
      theme: "solarized light"

  # to set code for summernote
  summer_note.code summer_note.val()

  # to get code for summernote
  summer_note.closest('form').submit ->
    # alert $('#post_content').code()
    summer_note.val summer_note.code()
    true
```

That's it.