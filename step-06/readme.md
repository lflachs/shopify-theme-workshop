# Step 06 - Cart page

So far, we have a homepage, with some products, we can navigate to the product page and add product to the cart.

Let's now create the cart page.

## Create the cart page

In the templates folder, create a `cart.liquid` file. As usual let's use a <h1> to check that everything works.

Navigate to `/cart` you should see your h1.

In the `cart` file, we can access all variables related to the cart as defined in the [documentation](https://shopify.dev/docs/api/liquid/objects/cart).

Let's display some information about the cart:

```
{% for item in cart.items %}
    <article>
        <img src="{{ item.product.featured_image | img_url: 'small' }}" alt="{{ item.product.name }}">
            <h2>{{ item.product.title }}</h2>
            <p>{{ item.product.description }}</p>
            <p>Price: {{ item.final_line_price | money }}</p>
    </article>
{% endfor %}
```

Now, it would be nice to give the option for our users to remove our update the items in our cart.

As you can see in the [documentation](https://shopify.dev/docs/themes/architecture/templates/cart) we need to wrap our cart item into a cart form and add that:

```
{% form 'cart', cart %}
    <a href="{{ item.url_to_remove }}">Remove</a>
    <input type="text" name="updates[]" value="{{ item.quantity }}">
    <input type="submit" value="Update">
{% endfor %}
```

Now, we can also display the total for the cart at the bottom:

```
<hr />

<h2>Total: {{ cart.total_price | money }}</h2>
<button type="submit" name="checkout"> Checkout </button>
```

Last, if you remove all items from the cart, you might see the total still displayed, we can use a condition to prevent that to be seen:

```
{% if cart.empty? %}
{% else %}
```

And that's it! Our cart page is done! If you click the checkout button, you can see that shopify already has everything done for the checkout.

It's possible to create a `checkout.liquid` page, but it's being deprecated by shopify probably for security reason. Shopify users with a plus plan can use the [checkout extensibility](https://shopify.dev/docs/apps/checkout/build-options) to customize the checkout on Shopify.
