# rw.theme

```javascript
const transformHook = (rw) => {
    const { names, breakpoints } = rw.theme;
    
    // names if an order array, smallest to largest,
    // of the enabled screen names in the theme studio
    // names = [ "sm", "md", "lg" ]
    
    // breakpoints is an object of key value pairs for
    // the enabled screens in the theme studio
    // breakpoints = { lg: 1024, md: 768, sm: 640 }
};

exports.transformHook = transformHook;

```
