---
layout: bulma
theme: jekyll-theme-cayman
title: APIs.guru awesome-openapi3
site:
  show_downloads: false
---

{% include header.md %}

## Tools by language

{% assign tmp = site.data.tools | where:"v3",true | sort: 'stars' | reverse %}
{% assign items_grouped = tmp | group_by: 'language' %}
{% assign items_sorted = items_grouped | sort: 'name' %}

{% for group in items_sorted %}
* [{{group.name}}](#{{group.name | slugify }}){% endfor %}

{% for group in items_grouped %}
### {{group.name}}

| Project | Stars | Category | Description |
|---|---|---|---|
{% for tool in group.items %}| <a href="{{ tool.github }}" data-json="{{ tool | jsonify | url_encode }}"> {% if tool.archived %}~~{% endif %}{{ tool.name }}{% if tool.archived %}~~{% endif %} </a> | {{ tool.stars }} | {{tool.category}} | {{ tool.description }} |
{% endfor %}
{% endfor %}

<script src="https://unpkg.com/tippy.js@3/dist/tippy.all.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/zepto/1.2.0/zepto.min.js"></script>

<script type="text/javascript">
  function plural(value,word){
    if (!value) value = 0;
    return value+' '+word+(value === 1 ? '' : 's');
  }
  $(document).ready(function(){
    $('table').addClass('table');
    $('ul').css('column-count',4);
    $('a').each(function(i,e){
        if ($(e).data('json')) {
            var d = JSON.parse(decodeURIComponent($(e).data('json')));
            tippy(e,{ content: plural(d.watch,'watcher')+', '+plural(d.forks,'fork')+' and '+plural(d.issues,'issue')+'. '+(d.license ? 'License:&nbsp;'+d.license : '')+(d.downloadStr ? ' Downloads: '+d.downloadStr : '')});
        }
    });
  });
</script>
