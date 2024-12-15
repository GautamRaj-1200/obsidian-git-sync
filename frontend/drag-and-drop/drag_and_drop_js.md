## Introduction
- The user may select  ***DRAGGABLE*** elements with a mouse,
- DRAG those elements to a ***DROPPABLE*** element,
- DROP them by releasing the button.
- A translucent representation of the _draggable_ elements follows the pointer during the drag operation.
- We can customize
	- which elements are **draggable**
	- the type of feedback the **draggable** elements produce
	- and the **droppable** elements

## Drag Events
- HTML drag-and-drop uses the [DOM event model](https://developer.mozilla.org/en-US/docs/Web/API/Event) and _[drag events](https://developer.mozilla.org/en-US/docs/Web/API/DragEvent)_ inherited from [mouse events](https://developer.mozilla.org/en-US/docs/Web/API/MouseEvent).
- A typical _drag operation_ begins when a user selects a _draggable_ element,
- continues when the user drags the element to a _droppable_ element, 
- and then ends when the user releases the dragged element.

| Event                                                                                                   | Fires when...                                                                                                                                                                                                         |
| ------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [`drag`](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/drag_event "drag")                | ...a _dragged item_ (element or text selection) is dragged.                                                                                                                                                           |
| [`dragend`](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/dragend_event "dragend")       | ...a drag operation ends (such as releasing a mouse button or hitting the Esc key; see [Finishing a Drag](https://developer.mozilla.org/en-US/docs/Web/API/HTML_Drag_and_Drop_API/Drag_operations#finishing_a_drag).) |
| [`dragenter`](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/dragenter_event "dragenter") | ...a dragged item enters a valid drop target. (See [Specifying Drop Targets](https://developer.mozilla.org/en-US/docs/Web/API/HTML_Drag_and_Drop_API/Drag_operations#specifying_drop_targets).)                       |
| [`dragleave`](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/dragleave_event "dragleave") | ...a dragged item leaves a valid drop target.                                                                                                                                                                         |
| [`dragover`](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/dragover_event "dragover")    | ...a dragged item is being dragged over a valid drop target, every few hundred milliseconds.                                                                                                                          |
| [`dragstart`](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/dragstart_event "dragstart") | ...the user starts dragging an item. (See [Starting a Drag Operation](https://developer.mozilla.org/en-US/docs/Web/API/HTML_Drag_and_Drop_API/Drag_operations#starting_a_drag_operation).)                            |
| [`drop`](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/drop_event "drop")                | ...an item is dropped on a valid drop target. (See [Performing a Drop](https://developer.mozilla.org/en-US/docs/Web/API/HTML_Drag_and_Drop_API/Drag_operations#performing_a_drop).)                                   |
## Q. How to implement drag-and-drop file upload in HTML?

### A. Use HTML5 Drag-and-Drop API

- Drag-and-drop functionality allows users to drag files from their file explorer and drop them directly into a specific area on a web page.

---

## Q. What are the components of drag-and-drop?

### A. Four main components:

1. **Draggable Area:**
    - A specific HTML element that acts as the target area for file drops.
    - Example        
```html
<div id="dropZone">Drop files here</div>
```
        
2. **Drag Events:**
    - **`dragenter`**: Fires when a file is dragged into the target area.
    - **`dragover`**: Fires continuously as the file is dragged over the target. Used to visually indicate the drop zone.
    - **`dragleave`**: Fires when the file is dragged out of the target area.
    - **`drop`**: Fires when the file is dropped into the target area.
3. **JavaScript Handlers:**
    - Event listeners are added to handle each drag event.
    - Example:
```js
const dropZone = document.getElementById('dropZone');
dropZone.addEventListener('dragover', (e) => {
    e.preventDefault(); // Prevent default behavior to allow drops
    dropZone.style.backgroundColor = 'lightblue'; // Visual cue
});

dropZone.addEventListener('drop', (e) => {
    e.preventDefault();
    const files = e.dataTransfer.files; // Access the dropped files
    console.log(files);
});
```
        
4. **File Handling:**
    - Use the **File API** to process dropped files.
    - Example:
```js
Array.from(files).forEach(file => {
    console.log(`Name: ${file.name}, Size: ${file.size}`);
});
```

---

## Q. How to style the drop zone?

### A. Use CSS for a better user experience    
- **Dynamic Styling**: Add/remove the `dragging` class during `dragenter` and `dragleave` events.

---

## Q. How to read files dropped into the area?

### A. Use the FileReader API:
- Example:
```js
dropZone.addEventListener('drop', (e) => {
    e.preventDefault();
    const files = e.dataTransfer.files;
    Array.from(files).forEach(file => {
        const reader = new FileReader();
        reader.onload = (event) => {
            console.log(`File content: ${event.target.result}`);
        };
        reader.readAsText(file); // Read as text; can also use readAsDataURL for images
    });
});
```

---

## Q. How to restrict file types?

### A. Check the file type in the `drop` event:
- Example:
```js
dropZone.addEventListener('drop', (e) => {
    e.preventDefault();
    const files = e.dataTransfer.files;
    Array.from(files).forEach(file => {
        if (file.type === 'image/png' || file.type === 'image/jpeg') {
            console.log(`Accepted file: ${file.name}`);
        } else {
            console.error(`Rejected file: ${file.name}`);
        }
    });
});
```
---

## Q. How to enable multiple file uploads using drag-and-drop?
### A. Drag-and-Drop inherently supports multiple files:

- Access all dropped files using `e.dataTransfer.files`.

---

## Q. What security concerns exist in drag-and-drop?

### A. Similar to `<input type="file">`:
- Files are not uploaded automatically, and the user must explicitly confirm actions.
- The **real file path** is never exposed—only the file name and metadata are accessible.
---
