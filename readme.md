# Sanity Resize Custom Overlay

A simple Custom Overlay that allows editors to set an element's width using a simple drag handle.

## Usage

First, define a max width property in your schema. You can name this anything you like:

```js
const myItem = defineType({
  ...,
  fields: [
    defineField({
      type: 'number',
      name: 'imageMaxWidth',
      title: 'Image Max Width',
    }),
  ]
});
```

Then, ensure the element you would like to apply the resize handle to has an Overlay created for it:

```jsx
<img
  data-sanity={createDataAttribute({
    id,
    type,
    path: "item.imageMaxWidth",
  }).toString()}
/>
```

Then, register `ResizeCustomOverlay` as a Custom Overlay for `<VisualEditing />`

```jsx
import { ResizeCustomOverlay } from "./ResizeCustomOverlay.tsx";

const components: OverlayComponentResolver = (props) => {
  const { type, node } = props;

  if (node.path === "imageMaxWidth") {
    return defineOverlayComponent(ResizeCustomOverlay, {
      direction: element.getAttribute("data-resize-dir"),
    });
  }
};

// ...

<VisualEditing components={components} />;
```

Finally, use the max width value however you wish:

```jsx
<img
  data-sanity={createDataAttribute({
    id,
    type,
    path: "item.imageMaxWidth",
  }).toString()}
  style={{ maxWidth: item.imageMaxWidth + "px" }}
/>
```
