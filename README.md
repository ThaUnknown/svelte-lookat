# LookAt

Creates a div which makes all it's children follow the mouse cursor or the user's face when using a mobile phone. Passes all props into the created div. Change  follow intensity with `intensity` prop.

Usage:
```jsx
import LookAt from 'svelte-lookat'

<LookAt class="w-full d-flex justify-content-center align-items-center" on:mousemove={handleMove} intensity={0.5}>
  <div class="w-full d-flex">
    text!
  </div>
</LookAt>
``` 