# frozen_string_literal: true

source "https://rubygems.org"
gem "github-pages", group: :jekyll_plugins

gem "tzinfo-data"
gem "wdm", "~> 0.1.0" if Gem.win_platform?
gem 'rack'
gem 'rackup' 

group :jekyll_plugins do
    gem "jekyll", ENV["JEKYLL_VERSION"] if ENV["JEKYLL_VERSION"]
    gem "kramdown-parser-gfm" if ENV["JEKYLL_VERSION"] == "~> 3.9"
    gem 'jekyll-feed', "~> 0.9"
    gem 'jekyll-sitemap', "~> 1.1"
    gem 'jekyll-admin'
end
gem "webrick", "~> 1.7"