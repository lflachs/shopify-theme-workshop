# Step 03 - Let's start our theme!

We could start by using a pre-existing theme and edit it to go faster and not start from scratch, but in order to gain a deep understanding we will start our theme from scratch for this workshop.

## Liquid extension

Feel free to install a extension for vs-code to handle liquid files Shopify created an official extension that you can find in the [extension store](https://marketplace.visualstudio.com/items?itemName=Shopify.theme-check-vscode).

## Create the folder structure

Let's create the folder structure, start by creating a new folder on your machine where you want your theme to be located.

Then we need to recreate the folder structure of a Shopify theme:

```
.
├── layout/
├── templates/
├── sections/
├── snippets/
├── config/
├── assets/
└── locales/
```

` mkdir layout templates sections snippets config assets locales`

And voilà! Our theme structure is ready to go!

## Create our first (and main) Layout

The layouts are the base of any Shopify theme, this is where our template are rendered.

From the [doc](https://shopify.dev/docs/themes/architecture/layouts):

```
Layouts are Liquid files that allow you to include content, that should be repeated on multiple page types, in a single location. For example, layouts are a good place to include any content you might want in your <head> element, as well as headers and footers.
```

![layout](https://shopify.dev/assets/themes/architecture/layout.png)

So that's also the place where we are going to create the main layout. The main layout file is called `theme.liquid`, but you can create different layout for your need.

Let's create a `theme.liquid` file in the Layout folder.

Here is the schema of a Layout file (again you can find that in the [documentation](https://shopify.dev/docs/themes/architecture/layouts)):

```
<!DOCTYPE html>
<html>
  <head>
    {{ content_for_header }}
  </head>

  <body>
    {{ content_for_layout }}
  </body>
 </html>
```

As you can see, the layout template is a html template, where some content will be injected by Shopify.

The [content_for_header](https://shopify.dev/docs/themes/architecture/layouts#content_for_header), will be where Shopify will inject all the scripts related to make your shop working.

The [content_for_layouut](https://shopify.dev/docs/themes/architecture/layouts#content_for_header) is where Shopify will inject the templates (so what the user will see).

## Create our first Template

Now that we have the Layout ready, we need a template, otherwise nothing will be displayed on the page.

From the [doc](https://shopify.dev/docs/themes/architecture/templates):

```
The template controls what's rendered on each type of page in a theme.

Each page type in an online store has an associated template type. You can use the template to add functionality that makes sense for the page type. For example, you can add additional product recommendations to a product template, or add a comment form to an article template.

You can create multiple versions of the same template type to create custom templates for different use cases. For example, you can create a separate product template for outerwear products, or a separate page template for pages with video content.
```

---

## Template types

From the doc:

```
Each available template type represents a type of content in a merchant's online store.

No template types are required. However, you must have a matching template for any page type that you want to render. For example, to render a product page, you need at least one template of type product.

You can have a maximum of 1000 JSON templates in your theme, across all template types. For example, if you have 20 JSON product templates, 10 JSON page templates, and 5 JSON collection templates, then you can add up to 965 additional templates to the theme.

You can use the following template types in your theme. To learn more about each template type, click on the template name.
```

| Type                       | Description                                                                                                                                                                                                                                   |
| -------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 404                        | Renders page content that is shown to customers if they enter an invalid URL for the store.                                                                                                                                                   |
| article                    | Renders the article page, which contains the full content of the article, as well as an optional comments section for customers. This template is used for items like individual posts in a blog.                                             |
| blog                       | Renders the blog page, which lists all articles within a blog.                                                                                                                                                                                |
| cart                       | Renders the /cart page, which provides an overview of the contents of a customer’s cart.                                                                                                                                                      |
| collection                 | Renders the collection page, which lists all products within a collection.                                                                                                                                                                    |
| customers/account          | Renders the customer account page, which provides an overview of the customer’s account.                                                                                                                                                      |
| customers/activate_account | Renders the customer account activation page, which hosts the form for activating a customer account.                                                                                                                                         |
| customers/addresses        | Renders the customer addresses page, which allows customers to view and manage their current addresses, as well as add new ones.                                                                                                              |
| customers/login            | Renders the customer login page, which hosts the form for logging into a customer account.                                                                                                                                                    |
| customers/order            | Renders the customer order page, which displays the details of a customer’s past orders.                                                                                                                                                      |
| customers/register         | Renders the customer register page, which hosts the form for customer account creation.                                                                                                                                                       |
| customers/reset_password   | Renders the password reset page, which hosts the form to reset the password for a customer account.                                                                                                                                           |
| gift_card.liquid           | Renders the gift card page, which displays the gift card issued to a customer upon purchase.                                                                                                                                                  |
| index                      | Renders the home page of the store, located at the root URL (/).                                                                                                                                                                              |
| list-collections           | Renders the collection list page, which lists all the store's collections. This page is located at the /collections URL of the store.                                                                                                         |
| page                       | Renders the shop’s pages, such as About us and Contact us.                                                                                                                                                                                    |
| password                   | Renders the /password page, which is a landing page shown when you add password protection to your online store. This page includes a message that is editable by merchants, and the password form for customers to gain access to the store. |
| product                    | Renders the product page, which contains a product's media and content, as well as a form for customers to select a variant and add it to the cart.                                                                                           |
| robots.txt.liquid          | Renders the robots.txt file, which is hosted at the /robots.txt URL. This file                                                                                                                                                                |
| search                     | Renders the /search page, which displays the results of a storefront search.                                                                                                                                                                  |

It's a lot of templates to create, isn't it?

Maybe let's start by the first one, our `index.liquid` page.

Go to the templates folder and create a `index.liquid` page.

Inside this page, let's add a `<h1>Hello world</h1>` to see our first page!

## Setup the shopify-cli to view our theme

To connect to a store, run the command `shopify theme dev --store {my-store}` where `{my-store}` should be the name of your store.

The cli will ask you to connect to your shopify partners account. Once it's done, you should see the theme up and running and you can open the URL to view your theme.

Let's take some time to inspect the page and understand what's going on.

## Add assets to our page

It's possible to add assets to our page, like images for example, for that, we can place the assets inside your theme `assets` folder.

To use it inside a `liquid` page, you can use the `{{ 'asset_name.extension' | asset_url  }}`.

In liquid, the `|` symbol indicate that we want to use a filter on a specific variable or text. So here, we will apply the asset_url filter to the file name and extension, and it will retrieve the asset URL from the server for us.

There is plenty of filter that we can use with liquid, you can find the list in their [documentation](https://shopify.dev/docs/api/liquid/filters).

Let's add the asset and an example of filter in our index to better understand:

```
<h1>{{ "Hello Template" | upcase }}</h1>
{{ 'puppy.jpg' | asset_url  }}
```

As you can see, it generates a cdn url for our asset in the shopify cdn. If you copy this url you should see the image.

Using the `asset_url` is a good practice when you work with Shopify, it will deliver the content through shopify cdn and will gives good performances, you can learn more about that in the [documentation](https://shopify.dev/docs/themes/best-practices/performance#host-assets-on-shopify-servers).

Let's make it nicer and wrap the image in an image tag:

```
<h1>{{ "Hello Template" | upcase }}</h1>
<img src={{ 'red-panda.jpg' | asset_url  }} alt="Puppy running on the grass" class="red-panda-img" />
```

We can also use the same approach for style and script files. Let's give it a try !

In the asset folder, add a style.css and a script.js file. In the style.css, let's resize our image:

```
.red-panda-img{
    width: 200px;
}
```

Now, let's go to our theme.liquid and let's add the css to the theme. In the `<head>` add the following code:

```
{{ 'style.css' | asset_url | stylesheet_tag }}
```

As you can see, we need to use another filter to add the url to a stylesheet tag, if you refresh, you should see the image resized.

Now let's add a `console.log` in the Js file, and let's do the same but this time place it at the end of the `<body>` tag.

We could use this code and it would work perfectly:

```
{{ 'script.js' | asset_url | script_tag }}
```

However, Shopify guidelines suggest that to get good performances, we should either use a script with `defer` or with `async` to prevent parser-blocking script tag ([see](https://shopify.dev/docs/themes/tools/theme-check/checks/parser-blocking-script-tag)), therefore, here is what we should use:

```
<script src="{{ 'script.js' | asset_url }}" async></script>
```

Now if you reload the page and go to the console, you should see that our script is loaded.

## Liquid object

Each page that you create inside your theme has access at a certain number of variables. You can find the list of the variable in the [documentation](https://shopify.dev/docs/api/liquid/objects).

If we look at the [shop](https://shopify.dev/docs/api/liquid/objects/shop) section, we can see that we can easily access the shop's name information using `shop.name`.

Let's try to use it inside our template to see how it look like:

```
<h1>{{ shop.name | upcase }}</h1>
```

You can see how we can easily access properties from our shop inside our liquid file!
