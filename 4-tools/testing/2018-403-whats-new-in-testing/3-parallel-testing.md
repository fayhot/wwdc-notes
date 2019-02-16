
## [Parallel testing](3-parallel-testing.md) | Ethan Vaughan | 1500 | p76



Development Cycle


Write Debug Test Push


Parallel Destination Testing (iOS 9.0)

Ability to run all of your tests on multiple destinations simultaneously

```bash 
xcodebuild test
    -destination ‘platform=iOS,name=iPhone X’ 
    -destination ‘platform=iOS,name=iPad’
```

Parallel Destination Testing - Limitations

- Only beneficial if testing on multiple destinations
- Only available from xcodebuild


### Testing Architecture  | 1810 | p88

Unit tests


UI tests

> See 2016 Advanced Testing and Continuous Integration


### Classes Execute in Parallel - Motivation

- Hidden dependencies between tests in a class
- Avoid unnecessary `+setUp` and `+tearDown` computation

### Parallel Testing on Simulator


### Demo | 2245


### Demo Recap | 2655

- Enabling parallelization
- Viewing results in the test log and test report
- Multiple instances of a Mac app running unit tests 
- Multiple simulator clones running UI tests


### `xcodebuild`

- Override the number of workers
  - `-parallel-testing-worker-count n`
- Force parallel testing on or off
  - `-parallel-testing-enabled YES | NO`


### Tips and Tricks

- Consider splitting a long running class into two classes
- Put performance tests into their own bundle, with parallelization disabled
- Understand which tests are not safe for parallelization

