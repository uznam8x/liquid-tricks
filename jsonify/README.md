# JSONIFY

## CODE
```liquid copy
{% liquid
    assign rows = source | strip | newline_to_br | strip_newlines | replace: '<br /><br />', '<br />' | split: '<br />'
    assign headers = rows[0] | split: '|'
    echo "["
    for row in rows offset:1
        assign columns = row | split: '|'
        echo "{"
        for column in columns
            assign index = forloop.index0
            assign key = headers[index] | strip
            assign value = column | strip
            echo '"' | append: key | append: '":"' | append: value | append:'"'
            unless forloop.last
                echo ","
            endunless
        endfor
        echo "}"

        unless forloop.last
            echo ","
        endunless
    endfor
    echo "]"
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
{% render 'jsonify', source: ticker %}
```

## OUTPUT
```json
[
    { "key":"APPLE", "value":"AAPL"},
    { "key":"MICROSOFT", "value":"MSFT"},
    { "key":"GOOGLE", "value":"GOOG"}
]
```
