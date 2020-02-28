
## Word Embeddings



Concept


Mapping symbols (label, string, image), to Vector Representation


Embedding



- Get vector for word
- Compute distance between two words
- Get nearest neighbors for word
- Get nearest neighbors for vector


[`NLEmbedding`](https://developer.apple.com/documentation/naturallanguage/nlembedding)


Obtain Embedding


```swift
import NaturalLanguage
guard let embedding = NLEmbedding.wordEmbedding(for: .english) else { return } 
guard let vector = embedding.vector(for: string) else { return }
let distance = embedding.distance(between: word1, and: word2)
embedding.enumerateNeighbors(for: string, maximumCount: 5) { (string, distance) —> Bool in // make use of string and distance
return true
}
```


Custom Word Embeddings

```swift
import CreateML
let vectors = ["Camembert": [0.118, 0.013, -0.063, -0.020, -0.100, 0.088, ...], "Brie": [0.038, 0.008, -0.051, 0.065, -0.198, 0.024, ...],
"Cirrus": [0.128, 0.127, 0.021, -0.042, -0.057, 0.055, ...], "Neufchâtel": [0.308, 0.094, -0.011, 0.155, -0.005, 0.021...], ...]
let embedding = try MLWordEmbedding(dictionary: vectors) try embedding.write(to: url)
```


Under the Hood

- Automatic compression
- Efficient representation for fast k-NN






## Transfer Learning

Text Classification


```swift
import CreateML
let modelParameters =
MLTextClassifier.ModelParameters(algorithm: .transferLearning(version: 1))
 
```



Guidelines
Algorithms

- Start with maxEnt classifier - Compare with transfer learning