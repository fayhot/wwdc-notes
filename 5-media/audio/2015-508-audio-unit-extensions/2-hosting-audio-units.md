
## [Hosting Audio Units](2-hosting-audio-units.md)

Hosting Audio Units

Using v3 API’s
Sample Code:AudioUnitV3Example

AUHost shows
- Finding
- Opening
- Connecting
- Presets
- Opening AU’s custom view



Audio Components
struct AudioComponentDescription {
  var componentType: OSType
  var componentSubType: OSType
  var componentManufacturer: OSType
  var componentFlags: UInt32
  var componentFlagsMask: UInt32
}



Finding Audio Unit Components
let anyEffect = AudioComponentDescription(componentType:
kAudioUnitType_Effect, componentSubType: 0, componentManufacturer:
0, componentFlags: 0, componentFlagsMask: 0)
let availableEffects: [AVAudioUnitComponent] = AVAudioUnitComponentManager.sharedAudioUnitComponentManager().  componentsMatchingDescription(anyEffect)


Selecting an Audio Unit
func selectEffectComponent(comp: AVAudioUnitComponent?,
completionHandler: () -> Void) {
selectEffectWithComponentDescription  (comp?.audioComponentDescription,
    completionHandler: completionHandler)
}




## Demo - AUHost |Michael Hopkins, Purveyor of Pixels|1200-1600|p40



Using an AudioUnit Directly, v3 (Swift):


```swift
AUAudioUnit.instantiateWithComponentDescription(desc, options: [])
{ audioUnit, err in
    ... 
}
```
Directly, v2 (C):

```c
AudioComponentInstantiate(desc, options, ^(AudioComponentInstance au, OSStatus err) {
    ... 
})
```

Hosting: In Versus Out of Process

v2 AU’s: Always in Host’s Process


v3 AU’s: Default to Separate Process

v3 AU’s: Optionally In-Process

party|value
---|---
Host options|kAudioComponentInstantiation_LoadInProcess
AU extension plist entry|AudioComponentBundle

### In-Process: Safety Versus Performance

- Safety
  - Security risk
  - Misbehaving AU can crash the host
- Performance
  - IPC overhead ~40 μs per render cycle
  - Significance depends on number of AU’s and render interval 
  - 0.1% at 1024 frames / 44.1 kHz
  - 5.5% at 32 frames / 44.1 kHz

### Updating a v2 Host

If kAudioComponentFlag_RequiresAsyncInstantiation is set, use:
extern void AudioComponentInstantiate(  
AudioComponent inComponent, 
AudioComponentInstantiationOptions inOptions, 
void (^inCompletionHandler)(  AudioComponentInstance __nullable, OSStatus));

Instead of:

extern OSStatus AudioComponentInstanceNew(AudioComponent
inComponent, AudioComponentInstance *outInstance);



If kAudioComponentFlag_IsV3AudioUnit is set, use: 

kAudioUnitProperty_RequestViewController
(also asynchronous) 

Instead of:

kAudioUnitProperty_CocoaUI

### Asynchronous Operations

- Can use new methods with v2 units
- Must use new methods with v3 units
- Helps responsiveness - Unblocks main thread
- Don’t wait on the main thread! - Deadlock

