# Dynamic event listener

A quick pure JavaScript implementation that allows to add an event listener that also works on elements dynamically created. The functionality is similar to `jQuery.on()`.

The minified library has only **806 Bytes**.

# Limitations
You should use `focusout` event instead of `blur`, as the `blur` event does not bubble.

# Usage
Include the library and call `addDynamicEventListener` to create a new event listener.
```HTML
<script src="dynamicListener.min.js"></script>
<script>
// Any `li` or element with class `.myClass` will trigger the callback, 
// even elements created dynamically after the event listener was created.
addDynamicEventListener(document.body, 'click', '.myClass, li', function (e) {
    console.log('Clicked', e.target.innerText);
});
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

- `Void`

# Browser support
Same as `addEventListener` (consider it  to be IE9+).

# How it works
The script uses the [Element.matches()](https://developer.mozilla.org/en/docs/Web/API/Element/matches) method to test the target element against the given selector. When an event is triggered the callback is only called if the target element matches the selector given.

# License
No restrictions. Feel free to use it in any project you want.


# Check out my analytics script
[![userTrack](https://www.usertrack.net/img/usertrack_logo.png)](https://www.usertrack.net)  
Self-hosted analytics plaform with heatmaps and full session recordings.
