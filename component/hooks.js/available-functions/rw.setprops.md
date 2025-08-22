# rw.setProps

The `rw.setProps()` accepts an object that is passed to your templates

```javascript
const transformHook = (rw) => {
  rw.setProps({
    message: 'Hello, World!',
    team: ["Ben", "Dan", "Tom"],
    apps: {
      elements: {
        slogan: "Build beautiful websites. No code required.",
        isAmamzing: true
      },
      squash: {
        slogan: "Batch Photo Editor",
        isAmamzing: true
      },
    }
  });
};

exports.transformHook = transformHook;
```
