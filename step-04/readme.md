# Step 04 - Snippets

So far, we've seen how to create layout and template and we were able to render successfully our index page.

Now, it's time to create snippets. Snippets are elements that you want to reuse.

## Create a Header

Let's create a `header` snippet, in your snippets directory, create a `header.liquid` file and add this inside of it:

```
<header>
    <h1>{{ shop.name }}</h1>
</header>
```

Let's also update our index.liquid page:

```
<p>Welcome to {{ shop.name }}</p>
```

Now, we would like to render this Header so that it's present on each page, so we can directly inject it inside our `theme.liquid` file.

To render a snippet, simply use the `{% render %}` [doc](https://shopify.dev/docs/api/liquid/tags/render) tag like so:

```
{% render 'header' %}
```

## Add a navbar

Let's add a navigation now, so our user can move from one page to another. Navigation can be customised in Shopify in the dashboard, click on the online store > navigation, by default we have two navigation, one for the footer and one main navigation.

If you open it you can see the different items that composed the navigation.

To use this navigation inside your liquid file, we can use the [linklist](https://shopify.dev/docs/api/liquid/objects/linklist) object.

The linklist object contains all the links of a menu, we can loop through it in liquid using the `for...in` loop:

```
<nav>
  <ul>
    {% for link in linklists.main-menu.links -%}
      <li>{{ link.title | link_to: link.url }}</li>
    {%- endfor %}
  </ul>
</nav>
```

Let's add that to our Header! And voilà! The navigation should be now visible ! :)
