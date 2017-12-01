---
id: version-0.28-appstate
title: AppState
original_id: appstate
---

`AppState` can tell you if the app is in the foreground or background,
and notify you when the state changes.

AppState is frequently used to determine the intent and proper behavior when
handling push notifications.

### App States

 - `active` - The app is running in the foreground
 - `background` - The app is running in the background. The user is either
    in another app or on the home screen
 - `inactive` - This is a state that occurs when transitioning between
 	 foreground & background, and during periods of inactivity such as
 	 entering the Multitasking view or in the event of an incoming call

For more information, see
[Apple's documentation](https://developer.apple.com/library/ios/documentation/iPhone/Conceptual/iPhoneOSProgrammingGuide/TheAppLifeCycle/TheAppLifeCycle.html)

### Basic Usage

To see the current state, you can check `AppState.currentState`, which
will be kept up-to-date. However, `currentState` will be null at launch
while `AppState` retrieves it over the bridge.

```
getInitialState: function() {
  return {
    currentAppState: AppState.currentState,
  };
},
componentDidMount: function() {
  AppState.addEventListener('change', this._handleAppStateChange);
},
componentWillUnmount: function() {
  AppState.removeEventListener('change', this._handleAppStateChange);
},
_handleAppStateChange: function(currentAppState) {
  this.setState({ currentAppState, });
},
render: function() {
  return (
    <Text>Current state is: {this.state.currentAppState}</Text>
  );
},
```

This example will only ever appear to say "Current state is: active" because
the app is only visible to the user when in the `active` state, and the null
state will happen only momentarily.


### Methods

- [`constructor`](appstate.md#constructor)
- [`addEventListener`](appstate.md#addeventlistener)
- [`removeEventListener`](appstate.md#removeeventlistener)




---

# Reference

## Methods

### `constructor()`

```javascript
constructor()
```



---

### `addEventListener()`

```javascript
addEventListener(type, handler)
```


Add a handler to AppState changes by listening to the `change` event type
and providing the handler

TODO: now that AppState is a subclass of NativeEventEmitter, we could deprecate
`addEventListener` and `removeEventListener` and just use `addListener` and
`listener.remove()` directly. That will be a breaking change though, as both
the method and event names are different (addListener events are currently
required to be globally unique).




---

### `removeEventListener()`

```javascript
removeEventListener(type, handler)
```


Remove a handler by passing the `change` event type and the handler



