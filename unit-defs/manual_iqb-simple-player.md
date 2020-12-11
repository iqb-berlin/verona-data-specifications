# Unit-Definition "iqb-simple" Version 1.0.0
Any HTML-content can be used as unit. Examples can be found in this repository in the folder `sample-data`.

The Unit can contain any HTML-content (inner Part of `<body>`), even `<script>`- and `<style>`-tags!
* Don't use the `<form>`-element, since the whole unit will put into one.
* Use the `<fieldset>`-element to define a page if you want to have a 
  multi-page unit. In this case on the root-level there should only be 
  `<fieldset>`-elements or absolute/static positioned elements, 
  otherwise it could confuse the page detection.
* Any `<input>`-, `<textarea>`- and `<select>`-element will be tracked and content stored as well as any element
  containing the `contenteditable`-attribute. In both cases use the name element to set up variable names.
* The player contains some JS-Classes which can be used in unit-code to extend functionality.
* Whenever a Verona-message is received an event with the same name is thrown, whenever a message is sent,
  an event called `sent:{MessageName}` gets thrown afterwards. Use these events to hook into the player's
  functionality if you want to.
* That's it.

## Naming
* Name the units with extension `htm` instead of `html`, otherwise the 
  iqb-testcenter gets confused with players wich have the same extension.

## Example units
* https://github.com/iqb-berlin/verona-player-simple/tree/main/sample-data
