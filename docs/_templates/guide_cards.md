<div class="grid cards" style="text-align: center;" markdown>
{% for title, guide in guides.items() %}
- ## {{ title }} { .guide-toc-heading }
    [![{{ title }}]({{ guide.folder|urlencode }}/image.png){ .guide-card-image }]({{ guide.folder|urlencode }}/)

    ---

    [**{{ title }}**]({{ guide.folder|urlencode }}/){ .guide-card-title }  
    [*{{ guide.author }}*]({{ guide.folder|urlencode }}/){ .guide-card-author }
{% endfor %}
</div>


