working-with-external-data.md



Working with external data



Combine Publisher


```swift



@State private var currentTime : TimeInterval = 0.0


VStack{}
.onReceive(PodcastPlayer.currentTimePubliser) {

}

```



