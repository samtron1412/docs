# Overview

- A fast, expressive, extensible templating engine.

# Template Designer Documentation

- https://jinja.palletsprojects.com/en/3.1.x/templates/

## Synopsis

- A Jinja template is simply a text file.
- A template contains `variables` and/or `expressions`, which get
  replaced with values when a template is **rendered**; and `tags`,
  which control the logic of the template.
- The default Jinja `delimiters` are:
    + `{% ... %}` for Statements.
    + `{{ ... }}` for Expressions to print to the template output.
    + `{# ... #}` for Comments not included in the template output.
        * Cannot add comments inside Expressions.
        * Or you can use comments way of the target language outside of
          Jinja statements and expressions, for example, YAML is `#`.

```
{# note: commented-out template because we no longer use this
    {% for user in users %}
        ...
    {% endfor %}
#}
```

## Variables

```
{{ foo.bar }}
{{ foo['bar'] }}
```

- More implementation details here:
    + https://jinja.palletsprojects.com/en/3.1.x/templates/#variables

## Filters

- Variables can be modified by `filters`.
- Filters are separated from the variable by a pipe symbol (`|`) and may
  have optional arguments in parentheses.
- Multiple filters can be chained.

```
{{ name|striptags|title }}
{{ listx|join(', ') }}
```

- List of builtin filters
    + https://jinja.palletsprojects.com/en/3.1.x/templates/#builtin-filters

## Tests

- Beside filters, there are also so-called `tests` variables.
- Tests can be used to test a variable against a common expression.
    + `name is defined`
- Tests can accept arguments, too.
    + `{% if loop.index is divisibleby(3) %}`
- List of builtin tests:
    + https://jinja.palletsprojects.com/en/3.1.x/templates/#builtin-tests

## Whitespace Control

- In the default configuration:
    + A single trailing newline is stripped if present.
    + other whitespace (spaces, tabs, newlines etc.) is returned
      unchanged.
- Add `+` or `-` to the beginning or end of a block to add or remove
  whitespaces before or after that block.

```
<div>
    {% if something +%}
        yay
    {% endif %}
</div>

{% for item in seq -%}
    {{ item }}
{%- endfor %}
```

## Esacping

```
{{ '{{' }}

{% raw %}
    <ul>
    {% for item in seq %}
        <li>{{ item }}</li>
    {% endfor %}
    </ul>
{% endraw %}
```

## extends, include, import

- `extends` template inheritance
    + Base template can defined `blocks` that child templates can
      override.
- `include`: renders another template and outputs the result into the
  current template.
- `import`: evaluate the imported template and make all variable,
  expressions available to use in the current template.

## Control structures

### For

```
<h1>Members</h1>
<ul>
{% for user in users %}
  <li>{{ user.username|e }}</li>
{% endfor %}
</ul>

---

<dl>
{% for key, value in my_dict.items() %}
    <dt>{{ key|e }}</dt>
    <dd>{{ value|e }}</dd>
{% endfor %}
</dl>

---

<dl>
{% for key, value in my_dict | dictsort %}
    <dt>{{ key|e }}</dt>
    <dd>{{ value|e }}</dd>
{% endfor %}
</dl>
```

### If

```
{% if users %}
<ul>
{% for user in users %}
    <li>{{ user.username|e }}</li>
{% endfor %}
</ul>
{% endif %}

---

{% if kenny.sick %}
    Kenny is sick.
{% elif kenny.dead %}
    You killed Kenny!  You bastard!!!
{% else %}
    Kenny looks okay --- so far
{% endif %}
```


### Macros

- Macros are comparable with functions in regular programming languages.

```
{% macro input(name, value='', type='text', size=20) -%}
    <input type="{{ type }}" name="{{ name }}" value="{{
        value|e }}" size="{{ size }}">
{%- endmacro %}
```

- Three special variables that you can access inside macros
    + `varargs`
        * If more positional arguments are passed to the macro than
          accepted by the macro, they end up in the special varargs
          variable as a list of values.
    + `kwargs`
        * Like varargs but for keyword arguments. All unconsumed keyword
          arguments are stored in this special variable.
    + `caller`
        * If the macro was called from a call tag, the caller is stored
          in this variable as a callable macro.
- The following attributes are available on a macro object:
    + `name`: name of the macro: `{{ input.name }}` will print *input*
    + `arguments`: a tuple of the names of arguments the macro accepts.
    + `catch_kwargs`:
        * This is true if the macro accepts extra keyword arguments.
    + `catch_varargs`
        * This is true if the macro accepts extra positional arguments.
    + `caller`
        * This is true if the macro accesses the special caller variable
          and may be called from a call tag.
- If a macro name starts with an underscore, it’s not exported and can’t
  be imported.

## Call (anonymous macro)

- Pass a macro to another macro.

```
{% macro render_dialog(title, class='dialog') -%}
    <div class="{{ class }}">
        <h2>{{ title }}</h2>
        <div class="contents">
            {{ caller() }}
        </div>
    </div>
{%- endmacro %}

{% call render_dialog('Hello World') %}
    This is a simple dialog rendered by using a macro and
    a call block.
{% endcall %}

---

{% macro dump_users(users) -%}
    <ul>
    {%- for user in users %}
        <li><p>{{ user.username|e }}</p>{{ caller(user) }}</li>
    {%- endfor %}
    </ul>
{%- endmacro %}

{% call(user) dump_users(list_of_user) %}
    <dl>
        <dt>Realname</dt>
        <dd>{{ user.realname|e }}</dd>
        <dt>Description</dt>
        <dd>{{ user.description }}</dd>
    </dl>
{% endcall %}
```
