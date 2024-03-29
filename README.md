# Dynamic event listener

A pure JavaScript implementation to enable adding event listeners that work on **dynamically created** elements.  
The functionality is similar to `jQuery.on()`.

The minified library has only **643 Bytes**.

# Limitations
You should use `focusout` event instead of `blur`, as the `blur` event does not bubble.

# Usage
Include the library and call `addDynamicEventListener` to create a new event listener.
```HTML
<script src="dynamicListener.min.js"></script>
<script>
// Any `li` or element with class `.myClass` will trigger the callback, 
// even elements created dynamically after the event listener was created.
var removeListener = addDynamicEventListener(document.body, 'click', '.myClass, li', function (e) {
    console.log('Clicked', e.target.innerText);
});

// Later
removeListener();
</script>
```

**Note:** You will have to use `event.delegatedTarget` in your callbacks to get the element that matches the selector (as `event.target` could be a child of this element and `event.currentTarget` is the root on which the listener was attached to).

### API
##### addDynamicEventListener(rootElement, eventType, selector, callback, options) 
###### Parameters  
| Name | Type | Description |
| ---- | ---- | ----------- |
| rootElement | `Element`  | The root element to add the listener to. |
| eventType | `string`  | The event type to listen for. |
| selector | `string`  | The selector that should match the dynamic elements. |
| callback | `function`  | The function to call when an event occurs on the given selector. |
| options | `boolean` `object`  | Passed as the regular `options` parameter to the addEventListener function                                 Set to `true` to use capture.<br>                                Usually used as an object to add the listener as `passive` |

##### Returns

- `Function` - removeListener - Callback that removes the previously attached listener.

# Browser support
Same as `addEventListener` (consider it  to be IE9+).

# How it works
The script uses the [Element.matches()](https://developer.mozilla.org/en/docs/Web/API/Element/matches) method to test the target element against the given selector. When an event is triggered the callback is only called if the target element matches the selector given.

# Updates

* **7 December 2023** -  Return a remove listener callback.

# License
No restrictions. Feel free to use it in any project you want.


# Check out my analytics script
[![Self-hosted analytics UXWizz](https://www.uxwizz.com/img/uxwizz_logo.png)](https://www.uxwizz.com/)  
Self-hosted analytics plaform with heatmaps and full session recordings.
