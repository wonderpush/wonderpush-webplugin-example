# What are plugins WonderPush website SDK?

They are javascript files that can be loaded by our website SDK to add functionnality and easy to use for our customers: all they have to do is slightly adapt their WonderPush javascript snippet like this:

```javascript
window.WonderPush = window.WonderPush || [];
WonderPush.push(["init", {
  webKey: "YOUR_WEB_KEY",
  plugins: {
    "example": {
      // Plugin options go here
    }
  },
}]);
```

# Developing a plugin

To get started with your own plugin, just use this repository as a template: fork and adapt.

## Prerequisites
While developing, you'll need:
1. an https-enabled test website where you can install WonderPush and test your plugin
2. https-enabled hosting of your plugin (it can be that same test website)

## Plugin structure

Choose a slug for your plugin and change this plugin slug from `example` to something more appropriate.

The main javascript file should be in the `src` directory, and named after that slug.
For example:

`src/myplugin.js`

Next to that plugin file, you can create SASS (SCSS) and CSS files:

`src/style.scss` or `src/style.css`

You can import these files with `WonderPushSDK.loadStylesheet`, as shown in this plugin file `src/example.js`.

## Plugin options

Plugins can accept options. They should be documented in JSDoc directly in your plugin source javascript file,
just like in this plugin:

```javascript
/**
 * Example WonderPush website SDK plugin.
 * @class Example
 * @param {external:WonderPushPluginSDK} WonderPushSDK - The WonderPush SDK instance provided automatically on intantiati
 * @param {Example.Options} options - The plugin options.
 */
/**
 * @typedef {Object} Example.Options
 * @property {String} [hello] - The contents of the hello message. Defaults to "Hello, world!"
 */

```

The options are passed directly from the WonderPush javascript snippet.
For example:


```javascript
    // (...)
    plugins: {
      "https://url/to/your/plugin/directory/dist/yourplugin.js": {
        exampleOption: 'exampleValue',
        // (...)
      }
    },
```

## Anatomy of the plugin file

### Registering the plugin

A WonderPush plugin is declared by calling `WonderPush.registerPlugin`
with 2 arguments:
1. the plugin slug
2. a set of plugin constructors.

You can provide up to two constructors: one for the `window` context,
and one for the `serviceWorker` context.

```javascript
(function () {
  WonderPush.registerPlugin("example", { // "example" is the plugin slug, you should adapt it.
    window: function (WonderPushSDK, options) {
    },
    serviceWorker: function (WonderPushSDK, options) {
    },
  });
})();
```
### Adding methods

Inside a constructor, you can add methods that will be publically accessible throught the WonderPush SDK:

```javascript
    // ...
    window: function (WonderPushSDK, options) {
      this.someMethod = function() {
      };
    }
    // ...
```

Methods can be called like this: `WonderPush.Plugins.get('example').someMethod()` where 'example' is the slug passed to `WonderPush.registerPlugin`

## Testing your plugin

### Step 1. Install WonderPush

Follow the [web push notifications quickstart guide](https://docs.wonderpush.com/docs/web-push-notifications-quickstart) to install WonderPush on that website.

You then need to modify your Javascript snippet to use your plugin.
This is done as described below.
Adapt `https://url/to/your/plugin/directory/dist/yourplugin.js` to point to the generated plugin file in the `dist` directory.

```javascript
window.WonderPush = window.WonderPush || [];
WonderPush.push(["init", {
    webKey: "YOUR_WEB_KEY",
    plugins: {
      "https://url/to/your/plugin/directory/dist/yourplugin.js": {
        // Plugin options go here
      }
    },
}]);
```

### Step 2. Build and deploy your plugin

Go to your plugin directory and run:

```shell
yarn install
gulp
```

This will install dependencies and run the build, generating a `dist` folder that contains your plugin file, minified,
along with any css files.

You then need to upload your plugin to an https-enabled hosting
so that the url you adapted in step 1 resolves to the plugin file in the `dist` directory just built.

You can then hit your test website, you should see in your inspector that the WonderPush SDK successfully loads your plugin javascript file.

### Step 3. Load the test website and make changes

As a convenience, there is a `gulp watch` target that will look for changes in JS, CSS and SASS source files and automatically update the contents of the `dist` directory.

About WonderPush
----------------

[WonderPush](https://www.wonderpush.com/) is a push notifications
service that allows your users to opt-in to timely updates from your
website and allow you to effectively re-engage them with customized,
engaging content, even when they are not currently browsing your
website.

Find out how to integrate web push notifications to your website
easily at: https://www.wonderpush.com/docs/web/getting-started.


Plugin documentation
--------------------

The documentation in JSDoc format available in the `gh-pages` branch,
and is served at:
https://wonderpush.github.io/wonderpush-webplugin-example/.


Plugin reference
----------------

API and options reference for the plugin are available here:
https://wonderpush.github.io/wonderpush-webplugin-example/latest/api.html.


Need some help?
---------------

Ask us by chat at: https://www.wonderpush.com/.
