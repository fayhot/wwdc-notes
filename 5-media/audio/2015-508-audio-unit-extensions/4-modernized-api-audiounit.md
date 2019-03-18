Modernized API
AUAudioUnit



### Properties: v2

- Scope/element based properties, void * access methods
  - `AudioUnitGetProperty(audioUnit, propertyID, scope, element, data, dataSize)`
  - `AudioUnitSetProperty`
  - Awkward from Swift


### Properties: v3

Dot syntax in ObjC and Swift, KVC/KVO:

```swift
au.maximumFramesToRender = 4096
let maxFrames = au.valueForKey(“maximumFramesToRender”) as? Int
mixerAU.addObserver(self, forKeyPath: "inputBusses", options: nil,   context: nil)
mixerAU.inputBusses.addObserverToAllBusses(self,  forKeyPath: "format", options: nil, context: nil)
```



### Busses

- Objects
  - AUAudioUnitBusArray
  - AUAudioUnitBus

```swift
let fmt: AVAudioFormat = au.inputBusses[0].format
let sampleRate: Double = fmt.sampleRate
au.outputBusses[0].name = “Reverb send”
```


### Parameters: v2

- Scope/element/ID
- Unweildy tuple
- Not enough bits for complex AU’s

```
AudioUnitGetParameter(audioUnit, paramID, scope, element, value) AudioUnitSetParameter(audioUnit, paramID, scope, element, value) ```

Complex AUEventListener API




AUAudioUnit.parameterTree
Nodes
Groups Parameters
• Permanent,  wave
unique string ID’s
Key path (KVC)
  oscillator.wave
  filter.envelope.attack
Parameters also have numeric addresses (transient)


### Parameter Wiring


### Parameter Scheduling

### MIDI Events


```
scheduleMIDI = au.scheduleMIDIEventBlock



scheduleMIDI(when, cable,  numBytes, bytePtr)

```

```
internalRender = au.internalRenderBlock
  
internalRender(... AURenderEvent realtimeEventListHead ...)
```

### Rendering

- Pull model
- v2: AU has connection or input callback
- v3: Input always from callback
- Otherwise, functionally identical
  - Efficient bridging


### Calling the Render Block - For hosts

- Fetch the block when allocating render resources:
- `au.allocateRenderResources()`
- `renderBlock = au.renderBlock`

Call it to render:

- `renderBlock(...)`


### Render Block: Output Buffers

- Host provides AudioBufferList for the Audio Unit’s output
- `bufferList.mBuffers[i].mData` can be null
  - AU must replace this with an internally-owned buffer
  - Buffer must remain valid until next render cycle


### Render Block: Input Buffers

- Host provides AURenderPullInputBlock
- AU calls block for input
- AU must supply valid AudioBufferList (non-null mData pointers)
- Host may replace mData pointers
  - Must guarantee that memory remains valid until next render cycle
- Goal—Avoid copying



### Rendering

- Realtime thread context
  - Cannot allocate memory
  - Cannot make blocking calls
- Using/implementing render blocks
  - Never capture self: ObjC runtime unsafe
  - Swift unsafe too
  - To capture state: use pointer to C struct, C++ object