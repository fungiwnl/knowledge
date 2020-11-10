# Testing



## UI Testing 

XCUITest is a native test framework introduced in iOS 9. It works by running your app in a seperate process from the test, with the test communicating to the app via a form of IPC. Tests are driven by interacting the iOS DOM with elements that can be be identified by IDs and values. 



## Element identifiers 

Other than accessing the storyboards, these are the methods to search for labels/accessibility identifiers of an iOS app to use to write UI tests.  

- Xcodes accessibility identifier dev tool (**Xcode -> Open Developer tool**)
- Setting a breakpoint in a test and inputting `po print(XCUIApplication().debugDescription)` in the debug console to print the apps object hierachy tree
- Adding `print(XCUIApplication.debugDescription)` statements in a test to print the apps object hierachy tree
