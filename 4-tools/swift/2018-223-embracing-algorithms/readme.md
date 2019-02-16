


2018-223-embracing-algorithms/readme.md


# [2018 223 Embracing Algorithms](https://developer.apple.com/videos/play/wwdc2018/223)




Dave Abrahams

Meet Crusty

Mind your own business


```swift
extension Canvas {
    mutating func deleteSelection() {
        for i in 0..<shapes.count {
            if shapes[i].isSelected {
                shapes.remove(at: i)
            }
        }
    }
}
```


 Linear vs Quadratic



•Get to know your standard library

Readability and Maintainability


“No Raw Loops” - Sean Parent (a.k.a. “Crusty's cousin”), C++ Seasoning




// Layering Operations

// bringToFront()


https://github.com/apple/swift/blob/master/test/Prototypes/Algorithms.swift




Discover Algorithms

```swift
extension MutableCollection {
    mutating func bringForward(elementsSatisfying predicate: (Element) -> Bool) {
        if let predecessor = indexBeforeFirst(where: predicate) {
            self[predecessor...].stablePartition(isSuffixElement: { !predicate($0) })
        }
    }
}

extension Collection {
    func indexBeforeFirst(where predicate: (Element) -> Bool) -> Index? {
        return indices.first {
            let successor = index(after: $0)
            return successor != endIndex && predicate(self[successor])
        }
    }   
}
```


Building Towers Of Abstraction


Discover Generic Algorithms


“If you want to improve the code quality in   your organization, replace all of your coding guidelines with one goal:
No Raw Loops” - Sean Parent, C++ Seasoning

