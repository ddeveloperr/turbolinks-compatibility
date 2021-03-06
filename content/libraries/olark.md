---
title: Olark
contributors:
  - user:     Empact
    name:     Ben Woosley
issues:
  - repo:     rails/turbolinks
    number:   166
---

# Olark Chat Widget 

> **[olark.com](http://olark.com)**

### Overview

The supplied javascript will look something like this:

```html
<script>
  window.olark || (function(c){
    // initialization code
  })({ 
    loader: "static.olark.com/jsclient/loader0.js", 
    name: "olark", 
    methods: ["configure", "extend", "declare", "identify"]
  });
  olark.identify('<your identity string>');
</script>
```

### Solution

To get it working with Turbolinks:

1. Move the script inside the head tags.
2. Convert the anonymous initialization function into a named function.
3. Bind this new function to the `page:load` event.

An example solution, in jQuery:

```javascript
function initOlark(){
  c = {
    loader: "static.olark.com/jsclient/loader0.js", 
    name: "olark", 
    methods: ["configure", "extend", "declare", "identify"]
  };
  //initialization code
}

window.olark || initOlark();

$(document).bind('page:load', function(){
  initOlark();
  olark.identify('<your identity string>');
});
```
