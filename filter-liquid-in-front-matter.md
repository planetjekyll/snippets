---
layout: snippet
title:  "liquify Filter - Use Liquid Placeholders in Front Matter Values"
---


## {{ page.title }}

Add a new filter that lets you use liquid in your front matter block. Example:

```
---
title: How to install {% raw %}{{ site.data.placeholder.product-name }}{% endraw %}
---
```

And the filter:

``` ruby
module LiquidFilter
  def liquify(input)
    Liquid::Template.parse(input).render(@context)
  end
end
Liquid::Template.register_filter(LiquidFilter)
```

Use it in your templates / layouts like:

```
{% raw %}
{{ page.title | liquify }}
{% endraw %}
```



## Sources

- [Jekyll filter: Use Liquid in front-matter](https://fettblog.eu/snippets/jekyll/liquid-in-frontmatter/) by Stefan Baumgartner
