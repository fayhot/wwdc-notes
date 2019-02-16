
## [Scalable Test Code](2-scalable-test-code.md) | Greg Tracy, Xcode Engineer | | p119


- Balance between UI and unit tests
- Code to help UI tests scale
- Quality of test code


### Striking the right balance  between UI and unit tests


### Testing Pyramid

UI - Unit ; Higher Maintenance - Lower Maintenance 

- Unit tests great for testing small, hard-to-reach code paths
- UI tests are better at testing integration of larger pieces


Writing code to help UI tests scale

Code to Help UI Tests Scale

- Abstracting UI element queries
- Creating objects and utility functions
- Utilizing keyboard shortcuts

### Abstracting UI Element Queries

- Store parts of queries in a variable
- Wrap complex queries in utility methods
- Reduces noise and clutter in UI test


Creating objects and utility functions

```swift
 
 func testGameWithDifficultyBeginnerAndSoundOff() {
     
app.navigationBars["Game.GameView"].buttons["Settings"].tap()
app.buttons["Difficulty"].tap()
app.buttons["beginner"].tap()
app.navigationBars.buttons["Back"].tap()
app.buttons["Sound"].tap()
app.buttons["off"].tap()
app.navigationBars.buttons["Back"].tap() app.navigationBars.buttons["Back"].tap()
// test code
}
```

After Code Refactoring

```swift
func setDifficulty(_ difficulty: String) {
app.buttons["Difficulty"].tap()
app.buttons[difficulty].tap()
app.navigationBars.buttons["Back"].tap()
}
func setSound(_ sound: String) {
app.buttons["Sound"].tap()
app.buttons[sound].tap()
app.navigationBars.buttons["Back"].tap()
}

enum Difficulty { 
    case beginner
    case intermediate
    case veteran
}
enum Sound {
    case on
    case off 
}


func setDifficulty(_ difficulty: Difficulty) {
 // code
}
func setSound(_ sound: Sound) {
 // code
} 

```


```swift 
class GameApp: XCUIApplication {
    enum Difficulty {/* cases */ }
    enum Sound { /* cases */}

    func setDifficulty(_ difficulty: Difficulty) { /* code */ }
    func setSound(_ sound: Sound) { /* code */ }
    func configureSettings(difficulty: Difficulty, sound: Sound) {
        app.navigationBars["Game.GameView"].buttons["Settings"].tap()
        setDifficulty(difficulty)
        setSound(sound)
        app.navigationBars.buttons["Back"].tap()
    }
}

func testGameWithDifficultyBeginnerAndSoundOff() { 
    GameApp().configureSettings(difficulty: .beginner, sound: .off) 
    // test code
}
```


