1-example-podcastplayer-on-watch.md



## [Example: PodcastPlayer on Watch](1-example-podcastplayer-on-watch.md) [4:32]





```swift
struct PlayerView : View {

    let episode : Episode
    @State private var isPlaying : Bool = false


}


```



Abstract a PlayButton out


```swift

struct PlayButton : View {

    @Binging var isPlaying : Bool = false // was @State private


}



```













@Binding Property Wrapper

- read and write without ownership
- Derivable from @State ? 

Really? You don't need ViewController any more?

Example of built-in Views to using Binding

- Toggle - Bool
- TextField - String
- Slider - BinaryFloatingPoint


```swift
Button(action: {
    withAnimation { self.isPlaying.toggle() }
}){

}

```

Use site


```swift


PlayButton(isPlaying: $isPlaying)


```