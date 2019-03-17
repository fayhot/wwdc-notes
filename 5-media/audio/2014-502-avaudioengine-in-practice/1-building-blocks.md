1-building-blocks.md

## Building Blocks

- Engine (AVAudioEngine)
- Node (AVAudioNode)
  - Output node (AVAudioOutputNode)
  - Mixer node (AVAudioMixerNode)
  - Player node (AVAudioPlayerNode)


### [`AVAudioEngine`](https://developer.apple.com/documentation/avfoundation/avaudioengine) class

- Engine manages graph of audio nodes
- Use the engine to set up connections between nodes
- Start/stop the engine
- Allows dynamic node configuration

### Engine Workflow

- Create an engine
- Create nodes
- Attach nodes to the engine
- Connect the nodes together
- Start the engine


### Node - AVAudioNode class

- Nodes are audio blocks
  - Source—Player, microphone
  - Process—Mixer, effect
  - Destination—Speaker
- N inputs/M outputs, specified as busses
- Every bus has an audio data format

### Active Chain

- Node connections
- Active chain => Source node to destination node



### Inactive Chain

- Node connections
- Disconnected nodes are in an inactive state

### Output Node - AVAudioOutputNode class

- Engine has an implicit destination node called output node 
- Output node provides audio data to the output hardware 
- Standalone instance cannot be created

### Mixer Node AVAudioMixerNode class

- Processing node that mixes N inputs to a single output
- Volume control over each input bus
- Volume control of output bus


Sub-Mixing

AVAudioMixerNode class


- Engine has an implicit mixer node
- Additional mixer nodes can be created and attached to the engine
- Mixer inputs can have different audio formats


### AVAudioEngine Architecture


### Pushing Data on the Render Thread

- Running engine = active render thread
- Use player nodes to push data


### Player Node - AVAudioPlayerNode class

- Player nodes play data from files and buffers
- Schedule events—Play data at a specified time
- Schedule buffers
  - Multiple buffers with individual callbacks
  - Single buffer that loops
- Schedule files and file segments


### Player Node—Single Buffer


### Player Node—File


