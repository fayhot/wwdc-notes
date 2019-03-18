## [Creating an Audio Unit Extension](3-creating-an-audio-unit-extension.md)



About App Extensions
.appex
App’s PlugIns directory
Runs in XPC service process
See App Extension Programming Guide



Creating an Audio Unit
Using v3 API’s
New Sample Code:AudioUnitV3Example FilterDemo


FilterDemo Anatomy
Containing app Extension (.appex) Both link framework

Easy development within app (no XPC) Code size/duplication
On OS X, framework can be   loaded into host process

### Extension’s Info.plist
Comments in <AudioUnit/AUAudioUnitImplementation.h>
 
Key|Value
---|---
NSExtensionPointIdentifier | com.apple.AudioUnit-UI
NSExtensionMainStoryboard | MainInterface
AudioComponents | AudioComponentDescription (type/subtype/manufacturer), name, version, tags


### Extension’s MainInterface.storyboard


Entry point is a View Controller, set its Custom Class:


### Extension Code

```swift
import FilterDemoFramework
/*
The app extension has to contain *some* code
  linking against the framework.
*/
let dummy = FilterDemoViewController.self
```

### Framework: FilterDemoViewController

- View controller is extension’s “principal class”
- Creates AUAudioUnit subclass
- Creates and manages custom view

### FilterDemoViewController

```swift
public class FilterDemoViewController : AUViewController,
    AUAudioUnitFactory, 
    ControllerDelegate {
  
    public var audioUnit: AUv3FilterDemo? { ... }
  
    public func createAudioUnitWithComponentDescription(desc:
AudioComponentDescription) throws -> AUAudioUnit {
        audioUnit = try AUv3FilterDemo(componentDescription: desc,
options: [])
        return audioUnit!
    }
}
```


### Framework: AUv3FilterDemo
AUAudioUnit subclass

```cpp
@interface AUv3FilterDemo () {
   FilterDSPKernel kernel;
   BufferedInputBus inputBus;
   AUAudioUnitBus *outputBus;
   AUAudioUnitBusArray *inputBusArray;
   AUAudioUnitBusArray *outputBusArray;
   AUParameterTree *parameterTree;
}
```


AUv3FilterDemo

Creating bus arrays

```
inputBus.init(defaultFormat, 8);
outputBus = [[AUAudioUnitBus alloc] initWithFormat:defaultFormat
error:nil];
inputBusArray  = [[AUAudioUnitBusArray alloc]
initWithAudioUnit:self busType:AUAudioUnitBusTypeInput  busses:
@[inputBus.bus]];
outputBusArray = [[AUAudioUnitBusArray alloc]
initWithAudioUnit:self busType:AUAudioUnitBusTypeOutput busses:
@[outputBus]];
```


Creating bus arrays

```
inputBus.init(defaultFormat, 8);
outputBus = [[AUAudioUnitBus alloc] initWithFormat:defaultFormat
error:nil];
inputBusArray  = [[AUAudioUnitBusArray alloc]
initWithAudioUnit:self busType:AUAudioUnitBusTypeInput  busses:
@[inputBus.bus]];
outputBusArray = [[AUAudioUnitBusArray alloc]
initWithAudioUnit:self busType:AUAudioUnitBusTypeOutput busses:
@[outputBus]];
```

Creating parameters

```
AUParameter *cutoffParam = 
[AUParameterTree createParameterWithIdentifier:@"cutoff" 
name:@“Cutoff" address:FilterParamCutoff 
min:12.0 max:20000.0  unit:kAudioUnitParameterUnit_Hertz unitName:nil  flags:0 valueStrings:nil dependentParameters:nil];
AUParameter *resonanceParam = 
[AUParameterTree createParameterWithIdentifier:@"resonance"  
name:@“Resonance" address:FilterParamResonance  ...
```

Creating the parameter tree
```
parameterTree = [AUParameterTree createTreeWithChildren:  @[cutoffParam, resonanceParam]];
parameterTree.implementorValueObserver =  ^(AUParameter *param, AUValue value) { 
filterDSPKernel->setParameter(param.address, value);  };
parameterTree.implementorValueProvider =  ^(AUParameter *param) { 
return filterDSPKernel->getParameter(param.address);  };
```


Preparing to render

```
- (BOOL)allocateRenderResourcesAndReturnError:(NSError **)outError
{
if (![super allocateRenderResourcesAndReturnError: outError]) {  return NO; }
  inputBus.allocateRenderResources(self.maximumFramesToRender);
kernel.init(outputBus.format.channelCount,  outputBus.format.sampleRate);
  kernel.reset();
```




Cleaning up
```
- (void)deallocateRenderResources
{
  [super deallocateRenderResources];
  inputBus.deallocateRenderResources();
  ...
```

Rendering

```
- (AUInternalRenderBlock)internalRenderBlock
{
  // Capture properties into locals.
  __block FilterDSPKernel *state = &kernel;
  __block BufferedInputBus *input = &inputBus;

return ^AUAudioUnitStatus(  AudioUnitRenderActionFlags *actionFlags, 
  const AudioTimeStamp
  AVAudioFrameCount
  NSInteger
  AudioBufferList
  const AURenderEvent
  AURenderPullInputBlock
{
...
```




Rendering
input->pullInput(&pullFlags, timestamp, frameCount, 0,  pullInputBlock);
AudioBufferList *inAudioBufferList =  input->mutableAudioBufferList;
state->setBuffers(inAudioBufferList, outAudioBufferList);
state->processWithEvents(timestamp, frameCount,   realtimeEventListHead);


Demo - AUv3FilterDemo | Michael Hopkins , Purveyor of Pixels | |p114

