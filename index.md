Example WonderPush webite SDK plugin.

## From the initialization options of the SDK

Change your call to `WonderPush.init()` to include the following, merging existing keys as necessary:

```javascript
WonderPush.init({
  plugins: {
    "example": {
      // Add any option to customize the plugin as desired
    },
  },
});
```

You can find the reference of the options in the {@link Example.Options} section of the reference.

# Reference

The available options are described in the {@link Example.Options} section of the reference.

The available API is described on the {@link Example} class.
