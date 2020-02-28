# [2019 232 Advances in Natural Language Framework](https://developer.apple.com/videos/play/wwdc2019/232/)



Sentiment Analysis

```swift
import NaturalLanguage
let tagger = NLTagger(tagSchemes: [.sentimentScore])
tagger.string = string
let (sentiment, _) = tagger.tag(at: string.startIndex, unit: .paragraph, scheme: .sentimentScore)

```

Language Assets
 
```swift
import NaturalLanguage
NLTagger.requestAssets(for: .french, tagScheme: .sentimentScore) { (result, error) in // handle result
}
```

Text Catalog
Creation

```swift
import CreateML
let entities = [
    "Italian Cheese": ["Parmigiano-Reggiano", "Pecorino Romano", "Montasio", ...], 
    "Mexican Cheese": ["Cotija", "Añejo", "Chihuahua", "Queso de cuajo", ...],
    "American Cheese": ["Monterey Jack", "Colby cheese", "Colorado Blackie", ...], 
    "Greek Cheese": ["Feta", "Kasseri", "Manouri", "Kefalotyri", ...], 
    ...
]
let gazetteer = try MLGazetteer(dictionary: entities) 
try gazetteer.write(to: url)
```

[NLGazetteer](https://developer.apple.com/documentation/naturallanguage/nlgazetteer)

### Under the Hood


Text Catalog
Usage with a tagger

```swift
import NaturalLanguage
let gazetteer = try! NLGazetteer(contentsOf: url)
let tagger = NLTagger(tagSchemes: [.nameTypeOrLexicalClass]) 
tagger.setGazetteers([gazetteer], for: .nameTypeOrLexicalClass)
```
