2-code-example.md


Code example

### Create Engine and Node


```
AVAudioEngine *engine = [[AVAudioEngine alloc] init];
AVAudioPlayerNode *player = [[AVAudioPlayerNode alloc] init];
[engine attachNode:player];
```


### Set up Player (File)

```
AVAudioFile *file = [[AVAudioFile alloc] initForReading:fileURL
error:&error];
AVAudioMixerNode *mainMixer = [engine mainMixerNode];
[engine connect:player to:mainMixer format:file.processingFormat];
[player scheduleFile:file atTime:nil completionHandler:nil];
```

### Set up Player (Buffer)

```
AVAudioPCMBuffer *buffer = ...

AVAudioMixerNode *mainMixer = [engine mainMixerNode];
[engine connect:player to:mainMixer format:buffer.format];

[player scheduleBuffer:buffer atTime:nil options:nil completionHandler:nil];
```


### Start Engine and Play

```
NSError *error;
[engine startAndReturnError:&error] !
[player play];
```


### Buffer Schedule Options

AVAudioPlayerNode class
1. Play buffer now

```
[player scheduleBuffer:buffer atTime:nil options:nil completionHandler:nil];
[player play];

// 2. Append new buffer
[player scheduleBuffer:buffer2 atTime:nil options:nil completionHandler:nil];



// 3. Interrupt with new buffer

[player scheduleBuffer:buffer2 atTime:nil
options:AVAudioPlayerNodeBufferInterrupts completionHandler:nil];

```

// 4. Loop single buffer


// 
5. Interrupt looping buffer

```
[player scheduleBuffer:buffer atTime:nil options:AVAudioPlayerNodeBufferLoops
completionHandler:nil];
[player play];
[player scheduleBuffer:buffer atTime:nil
options:AVAudioPlayerNodeBufferInterrupts completionHandler:nil];
```

6. Interrupt looping buffer after current loop finishes


### Buffer Looping Example

Attack, Sustain, Release

```
[player scheduleBuffer:attackBuffer atTime:nil options:nil
completionHandler:nil];
!
[player scheduleBuffer:sustainBuffer atTime:nil
options:AVAudioPlayerNodeBufferLoops completionHandler:nil];
!
[player play];
!
// after some time
[player scheduleBuffer:releaseBuffer atTime:nil
options:AVAudioPlayerNodeBufferInterruptsAtLoop completionHandler:nil];
```

Schedule to Play in the Future
AVAudioPlayerNode class
Buffers and files can be scheduled to play in the future

```
AVAudioTime *tenSecsInTheFuture = [AVAudioTime timeWithSampleTime:(10 *
buffer.format.sampleRate) atRate:buffer.format.sampleRate];
!
[player scheduleBuffer:buffer atTime: tenSecsInTheFuture options:nil
completionHandler:nil];
!
[player play];
```


### Node Tap - AVAudioNode class

- Node tap captures the output of a node
  - Record microphone data
  - Record a live performance in a music application
  - Capture the output mix of a game
- One tap per node’s output bus
- Captured data is returned in a callback block


```

[mixer installTapOnBus:0 bufferSize:4096 format:[mixer outputFormatForBus:0]
block:^(AVAudioPCMBuffer *buffer, AVAudioTime *when) {
            // perform operation using data
       }];
```

### Audio Data and the Render Thread

- Players push data onto the render thread
- Node taps pull data from the render thread


### Connect Input Node

Engine is running, input node is active Data is pulled from the input node


```
AVAudioInputNode *input = [engine inputNode];
[engine connect:input to:mixer format:[input inputFormatForBus:0]];
[engine startAndReturnError:&error];
```

### Disconnect Input Node

Engine is running but input node is inactive Data will not be pulled from the input node

[engine disconnectNodeOutput:input]


### Capturing Input - AVAudioInputNode class

Use a node tap directly with the   input node
Data is pulled when engine is running


### Effect Nodes

AVAudioUnitEffect, AVAudioUnitTimeEffect
Effects are nodes that process data
Two main categories
AVAudioUnitEffect AVAudioUnitTimeEffect




## Demo - Channel strip | | p88
Kapil Krishnamurthy
Core Audio Rock Star

