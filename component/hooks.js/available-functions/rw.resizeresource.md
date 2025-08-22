# rw.resizeResource

```javascript
const transformHook = (rw) => {
  const { resourceId } = rw.props;

  // resizeResource accepts a resource, and a number in pixes
  const defaultSrc = rw.resizeResource(resourceId, 1200);
  
  rw.setProps({
    defaultSrc // a resized image at 1200px wide.
  });
};

exports.transformHook = transformHook;

```
