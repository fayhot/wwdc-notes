## [xcodebuild](4-xcodebuild.md) | | | p161

4-xcodebuild.md


xcodebuild
Building block for Continuous Integration Systems


Test action


```bash
xcodebuild test -workspace <path>
                -scheme <name>
                -destination <specifier>
```

- Builds sources
- Installs app on destination if needed
- Runs tests
- Reports results in console


Test Options
Customizing tests
NEW

```bash 
xcodebuild test -workspace <path>
                -scheme <name>
                -destination <specifier>
                -only-testing:TestBundleA/TestSuiteA/TestCaseA
-only-testing:TestBundleB/TestSuiteB
-only-testing:TestBundleC
  
xcodebuild  test    -scheme <name>
                    -skip-testing:TestBundleD/TestSuiteD/TestCaseD
```


### Building for Testing


Only building

NEW

```bash  
xcodebuild build-for-testing -workspace <path>
                             -scheme <name>
                             -destination <specifier>
```

- Builds sources for testing
- Outputs products in Derived Data
- Generates an xctestrun file

### Test Without Building

Only testing

```bash
xcodebuild test-without-building -workspace <path>
                                 -scheme <name>
                                 -destination <specifier>
```

- Finds binary products in Derived Data
- Installs if necessary
- Runs tests and report results as before


```bash
xcodebuild test-without-building -xctestrun <path>
                                 -destination <specifier>
```

- Ingests the xctestrun file
- Finds binary products relative to xctestrun file
- Runs tests, reports results as before

### Distributed testing


### xctestrun - Test manifest

- Tests to run or skip
- Environment variables
- Command-line arguments
- Documentation in man pages
- `man xcodebuild.xctestrun`

