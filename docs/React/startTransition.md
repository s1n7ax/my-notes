# React `startTransition`

In React, state updates are asynchronous. However, once a state update triggers a re-render, the rendering process occurs synchronously and cannot be interrupted. This can make the UI unresponsive during rendering. For example, if a user clicks a button twice, the second state change must wait for the first render to complete.

Using `startTransition` makes rendering interruptible. In a scenario where a user clicks a button twice, the first render will be discarded in favor of the second state change.

> [!WARNING]  
> `startTransition` does not help in situations where a component performs heavy calculations during rendering. In such cases, the UI may still become unresponsive. Consider optimizing the component or offloading heavy calculations to a Web Worker.

> [!NOTE]  
> You can wrap an update into a Transition only if you have access to the set function of that state.

> [!IMPORTANT]  
> You must wrap any state updates after any async requests in another `startTransition` to mark them as Transitions.
>
> Example:
>
> ```javascript
> startTransition(async function () {
>   const savedQuantity = await updateQuantity(newQuantity);
>   startTransition(() => {
>     setQuantity(savedQuantity);
>   });
> });
> ```
