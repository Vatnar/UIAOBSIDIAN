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
- gtkmm, builds on C GTK, similar to Qt, but smaller and a bit simpler. easier to use from CLion. Modern C++
- Qt, large application framwerok, usually used through Qt creator, their own IDE.feature rich but complex. Recommended to learn more about GUI programming.
- FLTK:, smaller in complexity and scope, older design, not using modern c++.
# Window class and startup
*About*
- The window is implemented by creating a class.
- Inherit from Gtk::Window
- main() must then create the application and run it.
```cpp
#include <gtkmm.h>
class MyWindow : public Gtk::Window
{
public:
	MyWindow()
	{
		set_title("My window title");
		set_default_size(400, 300);
		
	}
};

int main(int argc, char *argv[])
{
auto app = Gtk::Application::create();

return app->make_window_and_run<MyWindow>(argc, argv);
}
```

**Biblioiteker trengs i vcpkg**
**pkgconf**
**gtkmm**


vcpkg install failed. See logs for more information: C:\Users\peter\Courses\ikt103g25v\examples\21_gtk\cmake-build-debug\vcpkg-manifest-install.log
Libraries. 