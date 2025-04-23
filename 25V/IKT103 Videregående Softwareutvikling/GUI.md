Qt

## Concepts
**Widget** - A GUI component, eg. a button, menu or text field
- Widget can contain other widgets
- A window is a wiedget, but it also contains widgets

**Signal** - Something that hapened in a widget
- Mouse click, a checkbox was checked, text wars typed.
- Widget generate signals from UI.

**Slots** - functions that can receive signals
- A function is connected to a signal so it can later receive it.
- A function is called when a connected signal is sent
- Widget sends signal -> your function is called. 
### GUI libraries
ABOUT
- gtkmm, builds on C GTK, similar to Qt, but smaller and a bit simpler. easier to use from CLion.
- Qt, large application framwerok, usually used through Qt creator, their own IDE.