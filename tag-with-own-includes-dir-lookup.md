---
layout: snippet
title:  "Use Your Own Includes Directory Lookup in Your Liquid Tags"
---


## {{ page.title }}

Add your own `_includes` directory lookup to your liquid tags
by adding `resolved_includes_dir`:

```ruby
module Jekyll
  module Tags
    class SnippetTag < IncludeTag
      def resolved_includes_dir(context)
        context.registers[:site].in_source_dir('_snippets')
      end
    end
  end
end

Liquid::Template.register_tag('snippet', Jekyll::Tags::SnippetTag)
```


## Sources

- [Custom Jekyll Includes Directory](https://fettblog.eu/snippets/jekyll/custom-jekyll-includes-directory/) by Stefan Baumgartner
