# pip_view_custom_size

This is a fork from ![pip_view](https://github.com/lslv1243/pip_view) which enables the custom sizes for floating widget. 


# pip_view

Widget to allow the presentation of a widget below a floating one. It supports moving the floating widget around which sticks to the corners.

![Example GIF](https://github.com/lslv1243/pip_view/raw/master/doc/example.gif)

## Usage

Create a `PIPView` widget, the prop `builder` will be the view rendered floating when requested. To present a view below the floating view use `PIPView.of(context).presentBelow(MyWidget(), initialWidgetSize: Size(280, 320))`. `initialWidgetSize` is optional. By adding that you'll set the starting size of the floating view/widget. if `initialWidgetSize` not set, the floating view/widget will take the full screen size.

### Props:

- `avoidKeyboard`: whether the floating view should avoid the keyboard;
- `builder`: a builder for the widget to float, the second parameter indicates if the view is floating;
- `floatingWidget`: a specific widget to be float, this is optional. when this is set the widget(parent) within the builder will be ignored when floating.
- `initialCorner`: the corner in which the floating view will be sticked initially
  - Possible values are: `PIPViewCorner.topLeft`, `PIPViewCorner.topRight`, `PIPViewCorner.bottomLeft`, `PIPViewCorner.bottomRight`;
- `floatingHeight`: the height of the foreground view when floating. If not set is calculated from the `floatingWidth` to keep aspect ratio of the screen;
- `floatingWidth`: the width of the foreground view when floating. If not set and `floatingHeight` is set, it is calculated from the `floatingHeight` value to keep aspect ratio of the screen. If not set and `floatingHeight` is not set, defaults to `100.0`;

### Example:

``` dart
class MyScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return PIPView(
      builder: (context, isFloating) {
        return Scaffold(
          body: Column(
            children: [
              Text('This is the screen that will float!');
              MaterialButton(
                child: Text('Start floating');
                onPressed: () {
                  PIPView.of(context).presentBelow(MyBackgroundScreen(), initialWidgetSize: Size(320, 280));
                },
              ),
            ],
          );
        );
      },
    );
  }
}

class MyBackgroundScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: Text('This is my background screen!');
    );
  }
}
```

NOTE: If you want a more declarative way of using the `PIPView`, you can use `RawPIPView` instead.
