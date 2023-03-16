# Step 02 - Theming

The theme in Shopify is the definition of the look, feel and functionnalties of your shop.

Shopify themes are built using Shopify templating language called Liquid. With HTML, CSS and JavaScript you can create any look and feel that you want.

You can find the liquid specs [here](https://shopify.github.io/liquid/).

## Let's explore shopify current theme

Go to online store > Themes.

Currently, our shop is using the default theme from shopify - Dawn. Let's see how the theme is structured, click on the `...` and then `edit code`, you should arrive in a code editor, here it is possible for us to view and see the code for each file that compose our theme and also to see the structure of the theme itself.

Any Shopify theme should follow a certain structure and must contain certain files in order to work.

## Markup and features (from the doc)

The organization of each page is determined by the following components.

![structure](https://shopify.dev/assets/themes/architecture/all-components.png)

1. The layout file
2. The template assigned to the resource being displayed
3. The sections added to the template
4. The blocks that each section contains

Each theme should include different types of templates to display different types of content, such as the home page and products. You can also create multiple templates for the same resource type to allow for variations within the online store.

Features can be introduced to themes in Liquid template files, sections, blocks, and snippets. You can implement theme features using Liquid, CSS, and JavaScript. The features included in the theme inform how customers can interact with the content on an online store. For example, your theme needs to allow customers to add products to a cart by providing a Liquid form tag with a product type.
