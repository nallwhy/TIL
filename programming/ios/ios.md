### 2017-03-24

#### Life without Interface Builder

https://blog.zeplin.io/life-without-interface-builder-adbb009d2068

```swift
// Defining the appearance while creating the property.
let editButton: NSButton = {
    let button = NSButton()
    button.bordered = false
    button.setButtonType(.MomentaryChange)
    button.image = NSImage(named: "icEdit")
    button.alternateImage = NSImage(named: "icEditSelected")

    return button
}()

// Declaring Auto Layout constraints with Cartography.
constrain(view, editButton, self) { view, editButton, superview in
    editButton.left == view.right
    editButton.right <= superview.right - View.margin
    editButton.centerY == view.centerY
}
```

https://github.com/robb/Cartography