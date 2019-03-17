1-manual-rendering.md



## Manual Rendering

- Engine is not connected to any audio device
- Renders in response to requests from the client
- Modes
  - Offline
  - Realtime

### Offline Manual Rendering

- Engine and nodes operate under no deadlines or realtime constraints
- A node may choose to:
  - Use a more expensive signal processing algorithm
  - Block on render thread for more data if needed
    - For example, player node may wait until its worker thread reads the data from disk


### Applications

- Post-processing of audio files, for example, apply reverb, effects etc.
- Mixing of audio files
- Offline audio processing using CPU intensive (higher quality) algorithms
- Tuning, debugging or testing the engine setup

## Demo - AVAudioEngine - Offline Manual Rendering

### //Realtime Manual Rendering, code example
```swift

do {

    let engine = AVAudioEngine() // by default engine will render to/from the audio device
    // make connections, e.g. inputNode -> effectNode -> outputNode

    // switch to manual rendering mode

    engine. stop()
    try engine.enableManualRenderingMode(
        .realtime format: outputPCMFormat,
        maximumFrameCount: frameCount)

    let renderBlock = engine.manualRenderingBlock // cache the render block


    // set the block to provide input data to engine
    engine.inputNode.setManualRenderingInputPCMFormat(inputPCMFormat) { 
        (inputFrameCount) -> UnsafePointer<AudioBufferList>? in
        guard haveData else { return nil}

        // fill and return the input audio buffer list
        return inputBufferList
    })

    // create output buffer, cache the buffer list
    let buffer = AVAudioPCMBuffer(
        pcmFormat: outputPCMFormat,
        frameCapacity: engine.manualRenderingMaximumFrameCount)!
 
    buffer.frameLength = buffer.frameCapacity
    let outputBufferList = buffer.mutableAudioBufferList 
    try engine.start()

}catch { 
    // handle error

}
```

### // to render from realtime context

```swift
OSStatus outputError = noErr;
const auto status = renderBlock(framesToRender, outputBufferList, &outputError);
switch (status) {
    case AVAudioEngineManualRenderingStatusSuccess:
    handleProcessedOutput(outputBufferList); // data rendered successfully
    break;
    case AVAudioEngineManualRenderingStatusInsufficientDataFromInputNode:
    handleProcessedOutput(outputBufferList); // input node did not provide data,
    break;
    // but other sources may have rendered
    ..
    default:
        break;
}
```

### Render calls Offline

Can use either ObjC/Swift render method or the block based render call
Realtime
Must use the block based render call
