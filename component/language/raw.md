# @raw

Adding the `@raw()` tag around templte content will stop Element properties from being processed, this is useful when using the [Elements CMS](https://app.gitbook.com/o/qIywZyO82bvjWx2b4aH7/s/Tf3DR4s6R7zTFZDxsRx4/) in your templates.

```html
@raw()
    <div class="text-sm text-black-600">{{item.title}}</div>
@endraw
```
