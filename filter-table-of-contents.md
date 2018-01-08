---
layout: snippet
title:  "toc Filter - (Auto-)generate a table of contents"
---

## {{ page.title }}


Add a filter that (auto-)generates a table of contents
using all heading 2 (h2) tags on your page:


``` ruby
module TocFilter
  def toc(input)
    output = "<ul class=\"toc\">"
    input.scan(/<(h2)(?:>|\s+(.*?)>)([^<]*)<\/\1\s*>/mi).each do |entry|
      id = (entry[1][/^id=(['"])(.*)\1$/, 2] rescue nil)
      title = entry[2].gsub(/<(\w*).*?>(.*?)<\/\1\s*>/m, '\2').strip
      if id
        output << %{<li><a href="##{id}">#{title}</a></li>}
      else
        output << %{<li>#{title}</li>}
      end
    end
    output << '</ul>'
    output
  end
end
Liquid::Template.register_filter(TocFilter)
```

Use it in your templates / layouts like:


```
{% raw %}
{{ content | toc }}
{% endraw %}
```


## Sources

- [Jekyll table of contents per page](https://fettblog.eu/snippets/jekyll/table-of-contents/) by Stefan Baumgartner
