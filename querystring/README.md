# Query string

## CODE
```liquid copy
{% liquid
assign qs = content_for_header | split: '"pageurl":"' | last | split: '"' | first | split: '.myshopify.com' | last | split: '?' | last | replace: '\/', '/' | replace: '%20', ' ' | replace: '\u0026', '&'
echo qs
%}
```

## USAGE
```liquid copy
{% render 'querystring' %}
```

> Lightly disregard the message "Do not rely on the content of 'content_for_header'" 😁