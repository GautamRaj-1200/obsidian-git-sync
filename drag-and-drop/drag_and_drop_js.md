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
