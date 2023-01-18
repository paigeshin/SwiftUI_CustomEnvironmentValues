# SwiftUI_CustomEnvironmentValues


```swift
import SwiftUI

/// STEP 1
/// Create a EnvironmentKey and define its type.
fileprivate struct SafeAreaValue: EnvironmentKey {
    
    static var defaultValue: EdgeInsets = .init(top: 0, leading: 0, bottom: 0, trailing: 0)
    
}

/// STEP 2
/// Then, create an environment value for the key that you created earlier.
extension EnvironmentValues {
    var safeArea: EdgeInsets {
        get {
            self[SafeAreaValue.self]
        }
        set {
            self[SafeAreaValue.self] = newValue
        }
    }
}

@main
struct CustomPropertyApp: App {
    @Environment(\.safeArea) private var safeArea
    
    var body: some Scene {
        WindowGroup {
            GeometryReader {
                let safeArea = $0.safeAreaInsets
                ZStack {
                    Color.red
                        .overlay(
                            Text("\(safeArea.top)")
                        )
                }
                /// Final Step
                /// Set up your environment value as per your wish, and it will be accessible through its subview via @Environment
                .environment(\.safeArea, safeArea)
                .ignoresSafeArea()
            }
        }
    }
}


```
