working-with-external-data.md


## [Working with external data](working-with-external-data.md)  (17:45-)



### Combine [`Publisher`](https://developer.apple.com/documentation/combine/publisher) (19:50-)

- Single abstraction
- Main thread: use .receive(on:)


### New requirement: Adding timestamp 


### External Changes

```swift

@State private var currentTime : TimeInterval = 0.0


VStack{
    Text("\(currentTime, formatter: currentTimeFormatter)")
}
.onReceive(PodcastPlayer.currentTimePubliser) { newCurrentTime in 
    self.currentTime = newCurrentTime
}

```

### External Data

protocol [`ObservableObject`](https://developer.apple.com/documentation/combine/observableobject) : AnyObject

~`BindableObject`~ is replaced by `ObservableObject`



```swift

class PodcastPlayerStore : ObservableObject {
    var didChange = PassthroughSubject<Void, Never>()

    func advance() {
        currentEpisode = nextEpisode
        currentTime = 0.0
        // Notify subscribers that the play changed
        didChange.send()
    }
}


```

### Creating Dependencies on  [`ObservableObject`](https://developer.apple.com/documentation/combine/observableobject) ~BindableObject~

Pass directly with `@ObservedObject` ~`@ObjectBinding`~



Automatic dependency tracking

```swift
@ObjectBinding var model: MyModel

```

### Creating Dependencies Indirectly

Environment


@EnvironmentObject

### Environment

- Data applicable to an entire hierarchy
- Convenience for indirection
- Content types: ...

## Comparison

tool|scope|type|managed by
--|--|--|--
@State|View-local|value|Framework
BindableObject|External|Reference|Developer 


@Binding

@State

Limit use if possible / Use derived `Binding`









BindableObject

### Creating Dependencies on BindableObject

`@ObservedObject` ~`@ObjectBinding`~

### Indirect Dependencies

@EnvironmentObject


### Environment

- Data applicable to an entire hierarchy
- Convenience for indirection
- Accent color, right-to-left, and more (dynamic type, dark mode)


#### Sources of Truth

[`ObservableObject`](https://developer.apple.com/documentation/combine/observableobject) ~`BindableObject`~

X|@State|`@ObservedObject` ~`@ObjectBinding`~ BindableObject
---|---|---
Scope|View-Model (in view only)|External (could be any object, such as from db)
data type|Value|Reference
x|Framework Managed|Developer Managed

#### Building Reuseable Components

- Read-only: Swift property, Environment
- Read-write : @Binding
- Prefer immutable access

? : @State - Use derived Binding or value

#### @Binding

- First class reference to data
- Great for reusability
- Use $ to derive from source


#### Using State Effectively

- Limit use if possible
- Use derived Binding or value
- Prefer BindableObject for persistence
- Example: Button highlighting


#### Next Steps

- Minimze Source of Truth
- Understand your data
- Build a great app!

