
# [2017 208 Natural Language Processing and your Apps](https://developer.apple.com/videos/play/wwdc2017/208/)

Speakers

* Vivek Kumar Rangarajan Sridhar, Software Engineering Manager
* Doug Davidson, Senior Engineer

Also see [2018 713 Introducing Natural Language Framework](https://developer.apple.com/videos/play/wwdc2018/713/)

TOC

* Language identification
* tokenization
* part of speech
* lemmatization
* named entity recognition

[`NSLinguisticTagger`](https://developer.apple.com/documentation/foundation/nslinguistictagger)


## App : Winnow

### Language identification

```swift
import Foundation
let tagger = NSLinguisticTagger(tagSchemes: [.language], options: 0) tagger.string = "Die Kleinen haben friedlich zusammen gespielt."
let language = tagger.dominantLanguage
```

### tokenization

```swift
import Foundation
let tagger = NSLinguisticTagger(tagSchemes: [.tokenType], options: 0)
let text = "NSLinguisticTagger provides text processing APIs.\n NSLinguisticTagger 是苹果的文字处理平台。"
tagger.string = text
let range = NSRange(location: 0, length: text.utf16.count)
let options: NSLinguisticTagger.Options = [.omitPunctuation, .omitWhitespace]
tagger.enumerateTags(in: range, unit: .word, scheme: .tokenType, options: options) { tag, tokenRange, stop in
let token = (text as NSString).substring(with: tokenRange)
  // Do something with each token
}
```

## part of speech



### lemmatization
```swift
import Foundation
let tagger = NSLinguisticTagger(tagSchemes:[.lemma], options: 0)
let text = "Great hikes make great pics! Wonderful afternoon in Marin County."
tagger.string = text
let range = NSRange(location:0, length: text.utf16.count)
let options: NSLinguisticTagger.Options = [.omitPunctuation, .omitWhitespace]
tagger.enumerateTags(in: range, unit: .word, scheme: .lemma, options: options) { tag, tokenRange, stop in
  if let lemma = tag?.rawValue {
      // Do something with each lemma
    }
}
```

## Demo by Doug

## Whisk - collate soical media feeds.

### named entity recognition

```swift
import Foundation
let tagger = NSLinguisticTagger(tagSchemes: [.nameType], options: 0)
let text = "Tim Cook is the CEO of Apple Inc. which is located in Cupertino, California" tagger.string = text
let range = NSRange(location:0, length: text.utf16.count)
let options: NSLinguisticTagger.Options = [.omitPunctuation, .omitWhitespace, .joinNames]
let tags: [NSLinguisticTag] = [.personalName, .placeName, .organizationName]
tagger.enumerateTags(in: range, unit: .word, scheme: .nameType, options: options) { tag, tokenRange, stop in
    if let tag = tag, tags.contains(tag) {
      let name = (text as NSString).substring(with: tokenRange)
    }
}
```

## Demo by Doug

## Homogeneous Text Processing

## Privacy

* On-device machine learning
* User data stays on-device

## Performance
* Highly optimized on-device
* Multi-threaded
* Existing clients—significant speedup
* Chinese tokenization is 30% faster on iOS
* Named Entity Recognition 80% faster on iOS


## Language Support

* Language identification - 29 scripts, 52 languages
* Tokenization - All iOS/macOS system languages
* Lemmatization, Part of speech, Named entity recognition

English French Italian German Spanish Portuguese Russian Turkish


## Accuracy


## Debugging Hints

- Tags are NSLinguisticTagOtherWord
- Model not downloaded
- Explicitly set language if known
