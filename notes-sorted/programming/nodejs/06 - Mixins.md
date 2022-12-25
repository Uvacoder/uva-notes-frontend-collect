https://pugjs.org/language/mixins.html

_ before mixin name is optional, comes from sass syntax (?)

create mixin (this is for a reusable form):
```pug
mixin storeForm(store = {})
```
the store argument defaults to an empty object

include mixin in `.pug` file:
```pug
include mixins/_storeForm
```

use mixin in another `.pug` file:
```pug
+storeForm()
```
we can pass arguments into mixins when using them

[[07 - Using Async Await]]