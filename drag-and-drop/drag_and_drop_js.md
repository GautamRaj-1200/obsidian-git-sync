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