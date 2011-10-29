desc 'Generate tags page'
task :tags do
  puts "Generating tags..."
  require 'rubygems'
  require 'jekyll'
  include Jekyll::Filters

  options = Jekyll.configuration({})
  site = Jekyll::Site.new(options)
  site.read_posts('')
  site.categories.sort.each do |category, posts|
    html = ''
    html << <<-HTML
---
layout: default
title: Postings tagged "#{category}"
---
    <h1 id="#{category}">Postings tagged "#{category}"</h1>

    html << '<ul class="posts">'
    posts.each do |post|
      post_data = post.to_liquid
      html << <<-HTML
        <li>#{post_data['title']}</li>
      HTML
    end
    html << '</ul>'

    File.open("tags/#{category}.html", 'w+') do |file|
      file.puts html
    end
  end
  puts 'Done.'

desc 'Generate tag-cloud page'
task :cloud do
  puts 'Generating tag cloud...'
  require 'rubygems'
  require 'jekyll'
  include Jekyll::Filters

  options = Jekyll.configuration({})
  site = Jekyll::Site.new(options)
  site.read_posts('')

  html =<<-HTML
---
layout: default
title: Tag cloud
---

<h1>Tag cloud</h1>

    HTML

    site.categories.sort.each do |category, posts|
      html << <<-HTML
      HTML

      s = posts.count
      font_size = 12 + (s*1.5);
      html << "<a href=\"/tags/#{category}.html\" title=\"Postings tagged #{category}\" style=\"font-size: #{font_size}px; line-height:#{font_size}px\">#{category}</a> "
    end

    File.open('tags.html', 'w+') do |file|
      file.puts html
    end
  end
  puts 'Done.'
