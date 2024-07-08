# Fuse

## CODE
```liquid copy
{% liquid
    assign rows = source | strip | newline_to_br | split: '<br />'
    assign offset = offset | default: 0
    for row in rows offset: offset
        assign res = template | strip
        assign columns = row | strip | split: '|'
        for column in columns
            assign key = "[%" | append: forloop.index0 | append: '%]'
            assign value = column | strip
            assign res = res | replace: key, value
        endfor
        echo res
    endfor
%}
```

## USAGE
```liquid copy
{%- capture ticker -%}
    key | value
    APPLE | AAPL
    MICROSOFT | MSFT
    GOOGLE | GOOG
{%- endcapture -%}
{%- capture template -%}
<dl>
    <dt>[%0%]</dt>
    <dd>[%1%]</dd>
</dl>
{%- endcapture -%}
{% render 'fuse', source: ticker, template: template %}
```

## OUTPUT
```html
<dl>
    <dt>APPLE</dt>
    <dd>AAPL</dd>
</dl>
<dl>
    <dt>MICROSOFT</dt>
    <dd>MSFT</dd>
</dl>
<dl>
    <dt>GOOGLE</dt>
    <dd>GOOG</dd>
</dl>
```