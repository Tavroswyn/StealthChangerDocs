
<p class="guide-author">{{ assembly.author }}</p>

## Overview

=== ":material-clipboard-text:{ .lg .middle } Summary"
    {% filter indent(width=4) -%}
{{ assembly.summary }}
    {%- endfilter %}

=== ":material-printer-3d-nozzle:{ .lg .middle } Printed BOM"

{% for item, data in assembly.printed_bom.items() %}
    * {{ item }} x{{ data.qty }} {% if data.urls is defined %}{% for anchor, url in data.urls.items() %}[[{{ anchor }}]({{ url }}){:target="_blank"}] {% endfor %}{% endif %}
{% endfor %}

=== ":fontawesome-solid-screwdriver-wrench:{ .lg .middle } Hardware BOM"

{% for item, data in assembly.hardware_bom.items() %}
    * {{ item }} x{{ data.qty }} {% if data.urls is defined %}{% for anchor, url in data.urls.items() %}[[{{ anchor }}]({{ url }}){:target="_blank"}] {% endfor %}{% endif %}
{% endfor %}

{% if assembly.resources is defined %}
=== ":material-database-eye:{ .lg .middle } Resources"

{% for anchor, url in assembly.resources.items() %}
    * [{{ anchor }}]({{ url }}){:target="_blank"}
{% endfor %}
{% endif %}
