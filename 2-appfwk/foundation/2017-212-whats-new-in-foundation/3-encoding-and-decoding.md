# [Encoding and Decoding - Tony Parker & Itai Ferber, Foundation](212-3-encoding-and-decoding.m) (23.5~)

```swift
let jsonData = """
{
  "name": "Monalisa Octocat",
  "email": "support@github.com",
  "date": "2011-04-14T16:00:49Z"
}
""".data(using: .utf8)!
struct Author : Codable {
    let name: String
    let email: String
    let date: Date
}
let decoder = JSONDecoder()
decoder.dateDecodingStrategy = .iso8601
let author = try decoder.decode(Author.self, from: jsonData)

author.name
author.date



```

???? Can use class instead of struct??

#### customize name

```swift
private enum CodingKeys : String, CodingKey {

  case commentCount = "comment_count"
}
```


## Demo - Itai Ferber, Foundation 30.5

GitHubCommit


#### `let sha: string`

add it in CodingKeys { case sha }

#### `let url : URL` ; `{case url = "XXXX"}` -

DecodingError

let url : URL? // if even wrong "XXXX" keyNotFound

#### valueNotFound / typeMismatch

## Slide , Tony 38:40

Codable Philosophy

* Error handling built-in
* Encapsulate encoding details
* Abstract format from types

### Error handling

* Encoding
  * Invalid Value
* Decoding
  * keyNotFound
  * valueNotFound
  * typeMismatch
  * dataCorrupted

#### Beyond Basic Error Handling

* Bytes
* Structured bytes
* Typed data
* Domain-specific validation
* Graph ?? validation

Writing `init(from decoder)...` - for example required url is https

### Encapsulate encoding details

Keyed Containers

Strongly-typed replacements for String keys

Unkeyed Container

Single Value Containers

#### `func encode(to encoder : Encoder) throws`

Nested Containers 49?

classes......

```swift
class Animal : Decodable {
  var legCount: Int
  private enum CodingKeys: String, CodingKey { case legCount }
  required init(from decoder: Decoder) throws {
    let container = try decoder.container(keyedBy: CodingKeys.self)
    legCount = try container.decode(Int.self, forKey: .legCount)
  }
}

class Dog : Animal {
  var bestFriend: Kid
  private enum CodingKeys : String, CodingKey { case bestFriend }
  required init(from decoder: Decoder) throws {
    let container = try decoder.container(keyedBy: CodingKeys.self)
    bestFriend = try container.decode(Kid.self, forKey: .bestFriend)
    let superDecoder = try container.superDecoder()
    try super.init(from : superDecoder)
  }
}

```

### Abstract format from types

Date -- see [`JSONEncoder.DateEncodingStrategy`](https://developer.apple.com/documentation/foundation/jsonencoder.dateencodingstrategy)

Data -- [`JSONEncoder.DataEncodingStrategy`](https://developer.apple.com/documentation/foundation/jsonencoder.dataencodingstrategy)

Property Lists


#### Codable Foundation Types

--- Ref
