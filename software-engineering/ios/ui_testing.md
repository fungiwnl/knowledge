# UI Testing

XCUITest is a native test framework introduced in iOS 9. It works by running your app in a seperate process from the test, with the test communicating to the app via a form of IPC. Tests are driven by interacting the iOS DOM with elements that can be be identified by IDs and values. 



## Element identifiers 

Other than accessing the storyboards, these are the methods to search for labels/accessibility identifiers of an iOS app to use to write UI tests.  

- Xcodes accessibility identifier dev tool (**Xcode -> Open Developer tool**)
- Setting a breakpoint in a test and inputting `po print(XCUIApplication().debugDescription)` in the debug console to print the apps object hierachy tree
- Adding `print(XCUIApplication.debugDescription)` statements in a test to print the apps object hierachy tree


## Increase core animation for tests to speed things up

```swift
if CommandLine.argumennts.contains("uitests"){
   window?.layer.speed = 100
}
```

## Disabling animations altogether


```swift
override func setup() {
  super.setup()
  continueafterfailure = false
  app.launcharguments.append("--uitests")
  app.launch()
  
}
```

And then in your AppDelegate:

```swift
if CommandLine.arguments.contains("--uitests") {
       UIView.setAnimationsEnabled(false)
     }
```



## References

[Stackoverflow - Disabling animations](https://stackoverflow.com/questions/41277026/disabling-waiting-for-idle-state-in-ui-testing-of-ios-apps)





