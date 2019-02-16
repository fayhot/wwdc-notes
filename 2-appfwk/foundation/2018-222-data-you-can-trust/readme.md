

# [2018 222 Data You Can Trust](https://developer.apple.com/videos/play/wwdc2018/222)


- Itai Ferber, Foundation



## Trusting Data

Goal—ensure it

- Hasn't been modified
- Doesn't contain anything unexpected
- Follows the format/model/structure you need


```
• Validating Raw Data
• Validating Primitive Data
• Validating Structured Data
• NSSecureCoding |  | p131
• Codable | 3311 | p203
```

## Validating Raw Data

- Length
- Checksum


### Type Validation

Validate First, Execute Later

Nullability Validation

Range Validation

Length Validation

### Domain-Specific Validation

Inter-Value Validation


```swift
// Validating a Listing
func validate(_ listing: [String : Any]) throws {
    // Type, nullability, range checking
    guard let id = listing["id"] as? Int,
        id > 0, id <= Int32.max else { throw ... }

    // Type, nullability, length checking, and domain validation (via URL)
    guard let urlString = listing["url"] as? String,
        urlString.count <= 50,
        let url = URL(string: urlString) else { throw ... }
 
    // Further domain validation
    guard url.host == "example.com" else { throw ... }

    // ...
}

try listings.forEach(validate)
```



```swift
// Structured Model Types
class Purchase : NSCoding {
    let listing: Listing
    let purchaseDate: Date
    let receipt: Receipt

    func encode(with coder: NSCoder) { ... }
    required init?(coder: NSCoder) { 
        guard let listing = coder.decodeObject(forKey: "listing") as? Listing else {
            return nil
        }

        self.listing = listing


        guard let date = coder.decodeObject(forKey: "purchaseDate") as? Date else {
            return nil
        }
        self.purchaseDate = date
 
    }

}
```


## Next Steps

- Validate data at every stage
- Check types, ranges, lengths, and domain
- Audit NSCoding types and earn your NSSecureCoding badge
- Adopt Codable for new data

