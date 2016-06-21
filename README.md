# PopupDialog

[![Version](https://img.shields.io/cocoapods/v/PopupDialog.svg?style=flat)](http://cocoapods.org/pods/PopupDialog)
[![License](https://img.shields.io/cocoapods/l/PopupDialog.svg?style=flat)](http://cocoapods.org/pods/PopupDialog)
[![Platform](https://img.shields.io/cocoapods/p/PopupDialog.svg?style=flat)](http://cocoapods.org/pods/PopupDialog)

## Introduction

Popup Dialog is a simple, customizable alert view that is close to UIAlertController, written in Swift (2.2). You can add an image on top, though ;)

![PopupDialog example one](http://www.mwfire.de/orderella/github/PopupDialog01.gif "PopupDialog example one")
![PopupDialog example two](http://www.mwfire.de/orderella/github/PopupDialog02.gif "PopupDialog example two")

##Usage

PopupDialog is a subclass of UIViewController and as such can be added to your view modally.
The full initializer looks as follows:

```swift
public init(title: String?, message: String?, image: UIImage? = nil, buttonAlignment: UILayoutConstraintAxis = .Vertical)
```

Bascially, all parameters are optional, although this makes no sense at all. You want to at least add a message and a single button, otherwise the dialog can't be dismissed. I am planning on implementing dismiss by background tap or swipe in the future.

If you provide an image it will be pinned to the top/left/right of the dialog. The ratio of the image will be used to set the height of the image view, so no distortion will occur.

Buttons can be aligned either `.Horizontal` or `.Vertical`, with the latter being the default. Please note distributing buttons horizontally might not be a good idea if you have more than two buttons.


## Example

You can find this example project in the repo. To run it, clone the repo, and run `pod install` from the Example directory first.

```swift
// Create the dialog
let alert = PopupDialog(title: title, message: message, image: image)

// Create a button with cancel style
let buttonOne = CancelButton(title: "CANCEL CAT") {
    self.kittenLabel.text = "You canceled the cat. Whatever that means..."
}

// Create a button with default style
let buttonTwo = DefaultButton(title: "PLAY WITH CAT") {
    self.kittenLabel.text = "Phew, that was exhausting!"
}

// Create a button with default style
let buttonThree = DefaultButton(title: "PET CAT") {
    self.kittenLabel.text = "The cat purrs happily :)"
}

// Add buttons to dialog
alert.addButtons([buttonOne, buttonTwo, buttonThree])

// Present dialog
self.presentViewController(alert, animated: true, completion: nil)

```

##Appearance
Many aspects of the popup dialog can be customized. Dialogs are supposed to have 
mostly the same layout throughout the app, therefore global appearance settings should make this easier. Find below the appearance settings and their default values.

```swift
// Popup Dialog View Appearance Settings
PopupDialogView.appearance().backgroundColor = UIColor.whiteColor()
PopupDialogView.appearance().titleFont       = UIFont.boldSystemFontOfSize(14)
PopupDialogView.appearance().titleColor      = UIColor(white: 0.4, alpha: 1)
PopupDialogView.appearance().messageFont     = UIFont.systemFontOfSize(14)
PopupDialogView.appearance().messageColor    = UIColor(white: 0.6, alpha: 1)
PopupDialogView.appearance().cornerRadius    = 4

// Popup Dialog Button Appearance Settings
// The standard button classes available are DefaultButton, CancelButton
// and DestructiveButton. On all buttons the same appearance can be set.
// Below, only the differences are highlighted
DefaultButton.appearance().titleFont         = UIFont.systemFontOfSize(14)
DefaultButton.appearance().titleColor        = UIColor(red: 0.25, green: 0.53, blue: 0.91, alpha: 1)
DefaultButton.appearance().buttonColor       = UIColor.clearColor()
DefaultButton.appearance().separatorColor    = UIColor(white: 0.9, alpha: 1)

CancelButton.appearance().titleColor         = UIColor.lightGrayColor()

DestructiveButton.appearance().titleColor    = UIColor.redColor()
```

Moreover, you can create a custom button by subclassing `PopupDialogButton`. The following example creates a solid blue button, featuring a bold white title font. Separators are invisble.

```swift
/// Represents a destructive button for the popup dialog
public final class SolidBlueButton: PopupDialogButton {

    override public func setupView() {
        defaultFont           = UIFont.boldSystemFontOfSize(16)
        defaultTitleColor     = UIColor.whiteColor()
        defaultButtonColor    = UIColor.blueColor()
        defaultSeparatorColor = UIColor.clearColor()
        super.setupView()
    }
}

```

These buttons can also be customized with the appearance settings given above as well.

## Requirements
As this dialog is based on UIStackViews, a minimum Version of iOS 9.0 is required.
This dialog was written with Swift 2.2, 3.X compatability will be published on a seperate branch soon.

## Installation

PopupDialog is available through [CocoaPods](http://cocoapods.org). To install
it, simply add the following line to your Podfile:

```ruby
pod 'PopupDialog', ~> '0.1.0'
```

## Author

Martin Wildfeuer, mwfire@mwfire.de
for Orderella Ltd., [orderella.co.uk](http://orderella.co.uk)

## Images in the sample project

The sample project features two images:<br>
Santa cat image courtesy of m_bartosch at FreeDigitalPhotos.net<br>
Cute kitten image courtesy of Tina Phillips at FreeDigitalPhotos.net<br>
Thanks a lot for providing these :)


## License

PopupDialog is available under the MIT license. See the LICENSE file for more info.
