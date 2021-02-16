# UI Testing

XCUITest is a native test framework introduced in iOS 9. It works by running your app in a seperate process from the test, with the test communicating to the app via a form of IPC. Tests are driven by interacting the iOS DOM with elements that can be be identified by IDs and values. 



## Element identifiers 

Other than accessing the storyboards, these are the methods to search for labels/accessibility identifiers of an iOS app to use to write UI tests.  

- Xcodes accessibility identifier dev tool (**Xcode -> Open Developer tool**)
- Setting a breakpoint in a test and inputting `po print(XCUIApplication().debugDescription)` in the debug console to print the apps object hierachy tree
- Adding `print(XCUIApplication.debugDescription)` statements in a test to print the apps object hierachy tree



## Disabling animations

Idling background animations in an app can cause issues with XCUITests where XCUITest wants to wait for all the UIView animations to end before it considers the app idle to continues with interacting with elements, etc. 

To fix this, we can set a `launchArgument` or `launchEnvironment` to disable animations in your app for tests, which should make tests implementable in areas of your app with persistent animations, while also making tests more stable and performant. 

```swift
override func setUp() {
  super.setUp()
  continueAfterFailure = false
  app.launchArguments.append("--UITests")
  app.launch()
  
}
```

And then in your AppDelegate:

```swift
if CommandLine.arguments.contains("--UITests") {
       UIView.setAnimationsEnabled(false)
     }
```



## References

[Stackoverflow - Disabling animations](https://stackoverflow.com/questions/41277026/disabling-waiting-for-idle-state-in-ui-testing-of-ios-apps)





