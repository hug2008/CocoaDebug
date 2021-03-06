<p align="center">
  <img src ="https://raw.githubusercontent.com/CocoaDebug/CocoaDebug/master/pic/logo.png"/>
</p>

# CocoaDebug

### [中文介绍](https://github.com/CocoaDebug/CocoaDebug/wiki/%E4%B8%AD%E6%96%87%E4%BB%8B%E7%BB%8D)

[![Build Status](https://travis-ci.org/CocoaDebug/CocoaDebug.svg?branch=master)](https://travis-ci.org/CocoaDebug/CocoaDebug)
[![Codacy Badge](https://api.codacy.com/project/badge/Grade/6aac8606d10f403a811cafdf870bb552)](https://www.codacy.com/app/CocoaDebug/CocoaDebug?utm_source=github.com&amp;utm_medium=referral&amp;utm_content=CocoaDebug/CocoaDebug&amp;utm_campaign=Badge_Grade)
[![CocoaPods Compatible](https://img.shields.io/cocoapods/v/CocoaDebug.svg)](https://img.shields.io/cocoapods/v/CocoaDebug.svg)
[![Carthage Compatible](https://img.shields.io/badge/Carthage-compatible-4BC51D.svg?style=flat)](https://github.com/Carthage/Carthage)
![Platform](https://img.shields.io/badge/platforms-iOS%208.0+-blue.svg)
![Languages](https://img.shields.io/badge/languages-Swift%20%7C%20ObjC-orange.svg)
[![codecov](https://codecov.io/gh/CocoaDebug/CocoaDebug/branch/master/graph/badge.svg)](https://codecov.io/gh/CocoaDebug/CocoaDebug)
<img src="https://img.shields.io/badge/license-MIT-blue.svg?style=flat" alt="License MIT"/>

iOS Debugging Tool

## Introduction

![example](https://raw.githubusercontent.com/CocoaDebug/CocoaDebug/master/pic/example.gif)

- Shake to hide/show the black bubble. (support both device/simulator)

- Long press the black bubble to show UIDebuggingInformationOverlay. (Apple's Private API, support iOS 10/11)

- You can copy app logs and network logs as you like. (long press the text, then select all or select copy)

---

![](https://raw.githubusercontent.com/CocoaDebug/CocoaDebug/master/pic/6.png)

- When you are in the `Network Details` page, you can shake device or simulator to share network details via email or copy to clipboard.

## Installation

### CocoaPods

```ruby
platform :ios, '8.0'
use_frameworks!

target 'YourTargetName' do
    pod 'CocoaDebug', :configurations => ['Debug']
end
```

### Carthage

```ogdl
github "CocoaDebug/CocoaDebug"
```

> WARNING: Don't submit `.ipa` to AppStore which has been linked with the `CocoaDebug.framework`. This [Integration Guide](https://github.com/CocoaDebug/CocoaDebug/wiki/Integration-Guide) outline a way to use build configurations to isolate linking the framework to `Debug` builds only.

## Usage

### Swift
	
    //Step 1.
    #if DEBUG
        import CocoaDebug
    #endif
	
    //Step 2.
    #if DEBUG
        CocoaDebug.enable()
    #endif

    //Step 3.
    public func print<T>(file: String = #file, function: String = #function, line: Int = #line, _ message: T, color: UIColor = .white) {
        #if DEBUG
            swiftLog(file, function, line, message, color)
        #endif
    }
	

### Objective-C
	
    //Step 1.
    #ifdef DEBUG
        @import CocoaDebug;
    #endif
	
    //Step 2.
    #ifdef DEBUG
        [CocoaDebug enable];
    #endif
	
    //Step 3.
    #ifdef DEBUG
        #define NSLog(fmt, ...) [CocoaDebug objcLog:[[NSString stringWithUTF8String:__FILE__] lastPathComponent] :NSStringFromSelector(_cmd) :__LINE__ :(fmt, ##__VA_ARGS__) :[UIColor whiteColor]]
    #else
        #define NSLog(fmt, ...) nil
    #endif

> Please check `Example_Swift.xcodeproj` and `Example_Objc.xcodeproj` for more advanced usage.

> NOTE: Be careful with `Other Swift Flags` & `Preprocessor Macros` when using Swift & Objective-C in one project. You can refer to [here](https://stackoverflow.com/questions/24111854/in-absence-of-preprocessor-macros-is-there-a-way-to-define-practical-scheme-spe).   

## TODO

- [Unit Testing](https://codecov.io/gh/CocoaDebug/CocoaDebug)

## Thanks

Special thanks to [remirobert](https://github.com/remirobert).

## License

CocoaDebug is released under the [MIT license](https://github.com/CocoaDebug/CocoaDebug/blob/master/LICENSE).