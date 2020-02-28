
### Language Identification

```swift
import NaturalLanguage
let recognizer = NLLanguageRecognizer()
recognizer.processString(“困死啦睡觉去了了”)
let lang = recognizer.dominantLanguage
let hypotheses = recognizer.languageHypotheses(withMaximum:2)
```

[`NLLanguageRecognizer`](https://developer.apple.com/documentation/naturallanguage/nllanguagerecognizer)

[`NLLanguage`](https://developer.apple.com/documentation/naturallanguage/nllanguage)

### Tokenization

```swift
import NaturalLanguage
let tokenizer = NLTokenizer(unit: .word)
let str = “困死啦睡觉去了了”
let strRange = str.startIndex ..< str.endIndex tokenizer.string = str
let tokenArray = tokenizer.tokens(for: strRange)
```

[`NLTokenizer`](https://developer.apple.com/documentation/naturallanguage/nltokenizer)


enum [`NLTokenUnit`](https://developer.apple.com/documentation/naturallanguage/nltokenunit) : Int / case word, sentence, paragraph, document



### Named Entity Recognition

```swift
import NaturalLanguage
let tagger = NLTagger(tagSchemes: [.nameType])
let str = “Prince Harry and Meghan Markle had their wedding ceremony in Windsor” let strRange = str.startIndex ..< str.endIndex
tagger.string = str
tagger.setLanguage(.english, range: strRange)
let tags = tagger.tags(in: strRange, unit: .word,
scheme: .nameType, options: .omitWhitespace)
```


[`NLTagger`](https://developer.apple.com/documentation/naturallanguage/nltagger)


struct [`NLTagScheme`](https://developer.apple.com/documentation/naturallanguage/nltagscheme)


struct [`NLTagger.Options`](https://developer.apple.com/documentation/naturallanguage/nltagger/options)


struct [`NLTag`](https://developer.apple.com/documentation/naturallanguage/nltag)