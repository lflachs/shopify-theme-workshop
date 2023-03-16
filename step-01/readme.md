# Step 01 - Getting started

## Setup your local environment

To start developping a theme for Shopify, we need to setup our local environment. We will create a Shopify Partner Account, a development store and install Shopify-cli.

### Create a Shopify Partner Account

The first step is to create a [Shopify Partner account](https://www.shopify.com/partners). A shopify Partner account is an account that can be created for people that are not working directly with shopify as a shop but rather on the configuratin and development side.

It can be used to develop, manage and sale themes or apps for Shopify or to experience, teach or test differents part of Shopify.

To create an Shopify Partner Account, follow [this link](https://accounts.shopify.com/signup?rid=dc920114-6359-4819-b070-daf32c521681).

Follow the onboarding step until your account is created. Choose "Building themes for the Shopify theme store".

### Create a Development store

Once your partner account is created, it's time to create a development store. Click on stores on your dashboard and "Create a development store".

Fill the information, use "Start with test data", and click on create store. Wait for your store to be created.

Now you should arrive on the administration of your development store! Take a moment to look at your store and explore a bit the dashboard.

### Install Shopify-cli

Follow the comand to install Shopify-cli:

#### macOS (Homebrew)

```
brew tap shopify/shopify
brew install shopify-cli
```

#### Windows and Linux (npm)

```
npm install -g @shopify/cli @shopify/theme
```

---

Now you can check your installation using `shopify version`, it should return to you the version.
