# Social Share Button

This is a gem to help you quickly add social share buttons to your rails site.

[![Gem Version](https://badge.fury.io/rb/social-share-button.svg)](https://badge.fury.io/rb/social-share-button)

# Supported Sites

* Facebook
* Twitter
* Douban
* Weibo
* QZone
* Google Bookmark
* Delicious
* Pinterest
* Email
* LinkedIn
* WeChat (Weixin)
* Vkontakte
* Odnoklassniki
* Xing
* Reddit
* Hacker News
* Telegram

## Screenshot

<img width="473" alt="2016-10-05 8 51 07" src="https://cloud.githubusercontent.com/assets/5518/19097657/ea7c0a20-8ad8-11e6-953f-83354d9a6384.png">

## Install

In your `Gemfile`:

```ruby
gem 'social-share-button', github: 'daqing/social-share-button'
```

Old version for IE and lower browser support:

```ruby
gem 'social-share-button', '0.2.1'
```

And install it:

```bash
$ bundle install
$ rails generate social_share_button:install
```

## Configure

You can config `config/initializers/social_share_button.rb` to choose which site do you want to use:

```ruby
SocialShareButton.configure do |config|
  config.allow_sites = %w(twitter facebook weibo)
end
```

More site names you can visit https://github.com/huacnlee/social-share-button/blob/master/lib/social_share_button/config.rb#L33 to found it.

## Usage

For static assets(css, js), please refer to the npm package: [@v8os/social-share-button-js](https://www.npmjs.com/package/@v8os/social-share-button-js)

Then you can use `social_share_button_tag` helper in views, for example `app/views/posts/show.html.erb`

```erb
<%= social_share_button_tag(@post.title) %>
```

Apart from the default title, you can specify the title for the special social network:

```erb
<%= social_share_button_tag(@post.title, 'data-twitter-title' => 'TheTitleForTwitter') %>
```

To specify sites at runtime:

```erb
<%= social_share_button_tag(@post.title, :allow_sites => %w(twitter facebook)) %>
```

And you can custom rel attribute:

```erb
<%= social_share_button_tag(@post.title, :rel => "twipsy") %>
```

You can also specify the URL that it links to:

```erb
<%= social_share_button_tag(@post.title, :url => "http://myapp.com/foo/bar") %>
```

```erb
<%= social_share_button_tag(@post.title, :url => "http://myapp.com/foo/bar", :image => "http://foo.bar/images/a.jpg", desc: "The summary of page", via: "MyTwitterName") %>
```

Those two above calls are identical.
Here are the mapping of attributes depending on you data-type parameter

| data-type         | standard  | custom :"data-*" prefixed  |
| ----------------- | --------- | -------------------------- |
| link (default)    | title     | data-title                 |
|                   | url       | data-url                   |
| text              | title     | data-title                 |
| photo             | title     | data-caption               |
|                   | image     | data-source                |
| quote             | title     | data-quote                 |
|                   |           | data-source                |

## Facebook

A couple of gotchas for Facebook only:

### Facebook needs the description added

```
  <%= social_share_button_tag('Share to Facebook', :url => course_path(@course), desc: @course.name) %>
```
This will add the required ```data-desc``` element, and Facebook will then accept the request.

### Testing from localhost will not work

You will need to test from a live site or Facebook will reject it; localhost will not work.


## How to change icon size?

Yes, you can override social-share-button base css to change the icon size.

In you `app/javascript/stylesheets/application.scss`:

```scss
$size: 24px;

.social-share-button {
  .ssb-icon {
    background-size: $size $size;
    height: $size;
    width: $size;
  }
}
```

## Demo

[https://ruby-china.org/wiki/about](https://ruby-china.org/wiki/about)
