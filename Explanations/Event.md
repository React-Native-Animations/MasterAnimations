The Animated.event is a utility method to automatically set a value on an Animated.Value given an array/keys to traverse. Typically this would be used with the `onScroll` or `onPanResponderMove`. It receives an array of instructions. Animated.event returns a function, when the function is called the arguments it is called with are applied to the instructions in the array you provided. Once those instructions are traversed when ever the function is called it just does a `setValue` with the provided value on to the Animated.Value.

The typical callback signature of React is event first, then additional properties like `gestureState` for `PanResponders`. On the event `nativeEvent` contains all the content you need.

Because a function would be called with (event, gestureState) => {}, the instructions to get data from event would need to be placed into the first array spot in Animated.event

In the case of an onScroll from a ScrollView you need to provide a few levels of instructions.

<code class="js language-js">
Animated.event([
{
  nativeEvent: {
    contentOffset: {
      y: this._animation
    }
  }
}
])
</code>
If you don't need to reference anything off an event simply pass in null so that the argument call signature matches the array of instructions.

In the case of a `PanResponder` you would skip the event piece with null and only provide instructions to automatically set animated values from gestureState

<code class="js language-js">
Animated.event([
  null,
  {
    dx: this._animation.x,
    dy: this._animation.y
  }
])
</code>