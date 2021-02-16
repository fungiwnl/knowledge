# Snapshot Testing
 
Snapshot testing is a form of testing that renders a UI, takes a snapshot of it, and compares it to a reference image. The idea behind snapshot testing is that it can catch visual defects such as layout, spacing, font, colour that normal unit or functional UI tests test for.

Inititally popularised by Facebooks snapshot testing library, which later got maintained by [Uber](https://github.com/uber/ios-snapshot-test-case), which now is deprecated. [Pointsfrees swift-snapshot-testing library](https://github.com/pointfreeco/swift-snapshot-testing) is now the library to use for all swift snapshotting needs. There are other forms of snapshot testing strategies that don't involve UI components, which is on the list of things to explore.


## Basic snapshot test 

```swift
import SnapshotTesting
import XCTest

class MyViewControllerTests: XCTestCase {
  func testMyViewController() { 
    var sut: OnboardingViewController!
   
    // Create an instance of UIStoryboard 
    let storyboard = UIStoryboard(name: "Onboarding", bundle: nil)

    // Instantiate UIViewController with Storyboard ID
    sut = storyboard.instantiateViewController(withIdentifier: "OnboardingViewController") as?
    OnboardingViewControler
   
    // Make the viewDidLoad() execute
    sut.loadViewIfNeeded()
    
    //Assert the rendered view against source image
    assertSnapshot(matching: sut, as: .image)
  }
}
```

## Re-recording snapshots
```swift
...
   assertSnapshot(matching: sut, as: .image, record: true)
```


## Asserting against multiple devices 

```swift
  private func verifyViewController(_ viewController: UIViewController, named: String) {
        let devices: [String: ViewImageConfig] = ["iPhoneX": .iPhoneX,
                                                  "iPhone8": .iPhone8, 
                                                  "iPhoneSe": .iPhoneSe]
        
        let results = devices.map { device in
            verifySnapshot(matching: viewController,
                           as: .image(on: device.value),
                           named: "\(named)-\(device.key)",
                           testName: "LoginViewController")
        }
        
        results.forEach { XCTAssertNil($0) }
    }
```


## References

https://medium.com/dev-jam/snapshot-testing-in-swift-9d52cbec075c

https://www.appsdeveloperblog.com/ways-to-load-uiviewcontroller-in-a-unit-test/
