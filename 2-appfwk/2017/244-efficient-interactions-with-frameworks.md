
# [2017 244 Efficient Interactions with Frameworks](https://developer.apple.com/videos/play/wwdc2017/244/)

## Intro.

x | Small Size | Large Size
--|--|--
Frequently Occurring |
Infrequently Occurring

## TOC

* Improvements in Foundation
* Bridges and how they affect your apps
* Strings, ranges, and text


## Improvements in Foundation

### Copy-on-Write

```swift
var bytes = Data(bytes: [0xcf, 0xfa, 0xed, 0xfe])
var buffer = malloc(250).assumingMemoryBound(to: UInt8.self)  defer { free(buffer) }
```

## Bridges and how they affect your apps

Toll-free bridging
* From a CF type to a NS type
* From a NS type to a CF type
* Zero cost at cast
* Extra cost at usage


## Strings, ranges, and text (by Danna?)


### String Bridging

#### Example 2: NSTextStorage

### Ranges  

#### Example 1: Working with NSAttributedString

```swift
let string = "What a 🎉💩!"
var attributedString = NSMutableAttributedString(string: string)   
let backgroundRange = string.range(of: “ attributedString.addAttribute(.backgroundColor,  
value: color,  
range: NSRange(backgroundRange, in: string))
```


#### Example 2: Working with NSRegularExpression

```swift

func findTags(in string: String) -> [Range<String.Index>] {
  var found = [Range<String.Index>]()
  let re = try! NSRegularExpression(pattern: "<([a-z][a-z0-9]*)/?>")
  let ns_range =  (string.startIndex..<string.endIndex, in: string)
  for match in re.matches(in: string, range: ns_range  ) {
    found.append (Range(match.rangeAt(1), in: string)!)
  }

  return found
}
```

### Text layout and rendering

#### Higher-level Strategies

Use modern layout practise

#### Lower-level tips

Set rendering attributes ..

specify alignment and writing direction if known

balance between performance and correctness
