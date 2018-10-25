# BLResultsController [![Version](https://img.shields.io/badge/Version-1.0-black.svg?style=flat)](#installation) [![License](https://img.shields.io/cocoapods/l/BLResultsController.svg?style=flat)](#license)

[![Platforms](https://img.shields.io/badge/Platforms-iOS|tvOS|macOS-brightgreen.svg?style=flat)](#installation)
[![Swift support](https://img.shields.io/badge/Swift-4.0%20%7C%204.1%20%7C%204.2-red.svg?style=flat)](#swift-versions-support)
[![CocoaPods Compatible](https://img.shields.io/cocoapods/v/BLResultsController.svg?style=flat&label=CocoaPods)](https://cocoapods.org/pods/BLResultsController)
[![Carthage compatible](https://img.shields.io/badge/Carthage-compatible-4BC51D.svg?style=flat)](https://github.com/Carthage/Carthage)
[![Twitter](https://img.shields.io/badge/Twitter-@BellAppLab-blue.svg?style=flat)](http://twitter.com/BellAppLab)

![BLResultsController](./Images/BLResultsController.png)

Background Realm is a collection of handy classes and extensions that make it easier to work with `RealmSwift` in the background.

It's main focus is to enhance existing `Realm`s and Realm-based code bases with very little overhead and refactoring. 

**Note**: Although this module makes it more convenient to work with a `Realm` in the background, it does **not** make  `Realm`s nor its objects thread-safe. They should still be accessed only from within their appropriate thread.

## Specs

* RealmSwift 3.0.0+
* iOS 9+
* tvOS 10+
* macOS 10.10+
* Swift 4.0+

## Writing to a Realm in the background

Commiting write transactions in the background becomes as easy as:

```swift
Realm.writeInBackground(configuration: <#T##Realm.Configuration?#>) { (realm, error) in
    <#code#>
}
```

Optionally, you can set a default `backgroundConfiguration` that will be used in all write transactions in the background:

```swift
Realm.Configuration.backgroundConfiguration = <#T##Realm.Configuration?#>

Realm.writeInBackground { (realm, error) in
    <#code#>
}
```

Finally, you can easily move from any `Realm` instance to its background counterpart:

```swift
let realm = try Realm()

realm.writeInBackground { (backgroundRealm, error) in 
<#code#>
}
```

## The `BackgroundRealm`

Background Realm exposes a `BackgroundRealm`  class, which basically:

1. creates a private `Thread` and `RunLoop` where a new background `Realm` will be opened
2. opens a `Realm` in the private thread
3. runs work in the background thread

This is particularly useful if you'd like to:

- make computationally expensive changes to the `Realm`
- register for change notifications in the background, without necessarily triggering a UI update right away

### Usage

- Creating a `BackgroundRealm` using `Realm.Configuration.backgroundConfiguration`:

```swift
let backgroundRealm = BackgroundRealm { (realm, error) in
    <#code#>
}
```

- Creating a `BackgroundRealm` using a custom configuration:

```swift
let backgroundRealm = BackgroundRealm(configuration: <#T##Realm.Configuration?#>) { (realm, error) in
    <#code#>
}
```

- Creating a `BackgroundRealm` using a file `URL`:

```swift
let backgroundRealm = BackgroundRealm(fileURL: <#T##URL#>) { (realm, error) in
    <#code#>
}
```

## Installation

### Cocoapods

```ruby
pod 'BLResultsController', '~> 1.0'
```

Then `import BLResultsController` where needed.

### Carthage

```swift
github "BellAppLab/BLResultsController" ~> 1.0
```

Then `import BLResultsController` where needed.

### Git Submodules

```shell
cd toYourProjectsFolder
git submodule add -b submodule --name BLResultsController https://github.com/BellAppLab/BLResultsController.git
```

Then drag the `BLResultsController` folder into your Xcode project.

## Author

Bell App Lab, apps@bellapplab.com

### Contributing

Check [this out](./CONTRIBUTING.md).

### Credits

[Logo image](https://thenounproject.com/search/?q=controller&i=316262#) by [Andres Flores](https://thenounproject.com/aflores158) from [The Noun Project](https://thenounproject.com/)

## License

BLResultsController is available under the MIT license. See the LICENSE file for more info.
