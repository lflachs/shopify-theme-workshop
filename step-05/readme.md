# Step 05 - Display some products

Let's display some of the products from our shop on our homepage. For that, we will first need to create a `product-card` snippet, and then loop through a collection of product available in shopify to display the products.

## Create the product-card snippet

Go on your theme and inside the snippet create a `product-card.liquid`. Inside this file, let's create a basic layout for the products:

```
<article>
    <h3>{{ product.title }}</h3>
</article>
```

Now in our homepage, let's render a collection. A collection in shopify is a collection of product that can be created with the UI and re-used.

If you look at your dashboard, you should see 3 collection of product already added for you.

Let's add more product to the `homepage` collection.

To access a collection in our liquid file we can use the [collections](https://shopify.dev/docs/api/liquid/objects/collections) object.

```
{% for product in collections['frontpage'].products %}
  {% render 'product-card' , product: product %}
{% endfor %}
```

We are passing to our template the product, you can see what the product object contains following the [documentation](https://shopify.dev/docs/api/liquid/objects/product)

Let's make it a bit nicer by adding the image of the product, and the price.

```
<img
    src="{{ product.featured_image | image_url: width: 300 }}"
    width="{{ image.width }}"
    height="{{ image.height }}"
    loading="lazy" />
<p>{{ product.price }}</p>
```

For the price, you might notice that the price is incorrectly displayed, to display the price correctly you can use the [money filter](https://shopify.dev/docs/api/liquid/filters/money-filters).

```
<p>{{ product.price | money }}</p>
```

Now, let's add the link so that when the user click, he is redirected to the product page:

```
<article>
    <a href={{ product.url }}>
        <h3>{{ product.title }}</h3>
        <img
            src="{{ product.featured_image | image_url: width: 300 }}"
            width="{{ image.width }}"
            height="{{ image.height }}"
            loading="lazy" />
        <p>{{ product.price | money }}</p>
    </a>
</article>
```

That's it, but now we need to create the product page.

## Product page

The product page is defined by creating a `product.liquid` page inside the templates folder.
Let's create a quick one with just a h1 to test

```
<h1>Welcome to the product Page<h1>
```

Now if you click on a product, you should be redirected to the product page.

As you might have guessed, inside the product page, you can access to variables related to the current product.

Let's use them to display informations about the product:

```
<article>
  <h1>{{ product.title }}</h1>
  <img src="{{ product.featured_image | image_url: width: 600 }}" alt="{{ product.title }}" loading="lazy" width="{{ product.width }}" height="{{ product.height }}">
  <p>{{ product.price | money }}</p>
  <p>{{ product.description }}</p>
</article>
```

### Product Variants

Product might have different variations, the variations can be defined inside the product itself in Shopify.

We can access the product variant using the `product.variants` object.

Let's create a select menu:

```
<select name="id">
    {% for variant in product.variants %}
        <option value="{{ variant.id }}">{{ variant.title }}</option>
    {% endfor %}
</select>
```

### Add to cart

It's possible to add a functionnality to add a product to the cart, for that we will need to use a form. The product form is defined in the [documentation](https://shopify.dev/docs/themes/architecture/templates/product) like so:

```
{% form 'product', product %}
  <!-- form content -->

  <input type="submit" value="Add to cart">
{% endform %}
```

Let's add this to our product page:

```
{% form 'product', product %}
  <select name="id">
      {% for variant in product.variants %}
          <option value="{{ variant.id }}">{{ variant.title }}</option>
      {% endfor %}
  </select>

  <button type="submit">Add to cart</button>
{% endform %}
```

Now if you click on the button, you shouldn't be able to see the cart page, by default, shopify redirects the user to the cart when a product is added and we don't have a cart page for now, you can view your cart by visiting `/cart.json` in your browser.

Let's now add also the same thing to the `product-card` so that user can add to the cart also from there.

And that's it! Our cart page is done! If you click the checkout button, you can see that shopify already has everything done for the checkout.
