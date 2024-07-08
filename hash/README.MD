Hash

## CODE
```liquid copy
{% liquid
echo 'now' | date: '%N' | modulo: 1000000 | md5 | prepend: '_'
%}
```

## USAGE
```liquid copy
{% render 'hash' %}
``
