working-with-external-data.md


## [Working with external data](working-with-external-data.md) 



### Combine [`Publisher`](https://developer.apple.com/documentation/combine/publisher)

- Single abstraction
- Main thread: use .receive(on:)


### New requirement: Adding timestamp 


### External Changes

```swift



@State private var currentTime : TimeInterval = 0.0


VStack{}
.onReceive(PodcastPlayer.currentTimePubliser) { newCurrentTime in 
    self.currentTime = newCurrentTime
}

```

### External Data


```swift

class PodcastPlayerStore : BindableObject {
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

Pass directly with `@ObjectBinding`
Automatic dependency tracking

```swift
@ObjectBinding var model: 

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

@ObjectBinding

### Indirect Dependencies

@EnvironmentObject


### Environment

- Data applicable to an entire hierarchy
- Convenience for indirection
- Accent color, right-to-left, and more


Sources of Truth

X|@State|BindableObject
---|---|---
x|View-Model|Extneral
x|Value|Reference
x|Framework Managed|Developer Managed

### Building Reuseable Components

Read-only: Swift property, Environment
: @Binding
: @State - Use derived Binding or value


Next Steps

- Minimze Source of Truth
- Understand your data
- Build a great app!

