<ul>
{%- for sub_page in site.pages -%}
  {%- if sub_page.url contains page.url and sub_page.url != page.url -%}
    <li><a class="page-link" href="{{ sub_page.url | relative_url }}">{{ sub_page.title | escape }}</a></li>
  {%- endif -%}
{%- endfor -%}
</ul>