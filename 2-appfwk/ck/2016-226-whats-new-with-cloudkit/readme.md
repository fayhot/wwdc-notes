
# [2016 226 What's New with CloudKit](https://developer.apple.com/videos/play/wwdc2016/226/)

* Paul Seligman, CloudKit Engineer
* Jacob Farkas, CloudKit Engineer
* Vanessa Hong, CloudKit Engineer

TOC

Topic|Speaker|Time|Page
---|---|---|---
CloudKit Overview|Paul Seligman
Telemetry|Paul Seligman
API Improvements|
Sharing|
[Sharing UI](4-sharing-ui.md) | Jacob Farkas | 1955 | p114 
[Sharing In Depth](5-sharing-in-depth.md) |  Vanessa Hong | 2900 | p177

## CloudKit Overview

### Record Zone

zone | Public database | private database | shared database
--|--|--|--
default zone | Y | Y
custom zone |  | Y
shared zone | | | Y

### CloudKit Is Now Available Everywhere

* New in watchOS
* macOS
  * No Mac App Store requirement
    * Add iCloud Capabilities via your provisioning profile
* Web
  * Server to server
    * Acts as admin user
    * Uses public/private key pair registered on CloudKit Dashboard
    * Access to public database
* watchOS 3
  * Alternative to watch connectivity code
  * Standalone functionality
  * Can work without phone present (via wifi)
    * (Almost) Full CloudKit API - offer does not include CKSubscription
  * Similar code on all Apple platforms
  * Limited resources

## Telemetry
Visualize your app's behavior on the CloudKit Dashboard

## [API Improvements](3-api-improvements.md)

* Long Lived Operations
* CKOperation Timeouts
* Handling Many Record Zones
* Fetching Multiple Change Sets



## [Sharing UI](4-sharing-ui.md) | Jacob Farkas | 1955 | p114



## [Sharing In Depth](https://developer.apple.com/videos/play/wwdc2016/226/?time=1731) |  Vanessa Hong

5-sharing-in-depth.md

* Sharing multiple records
* Zones in shared database
* CKShare internals
* Sharing APIs
* Special notes


## Summary

* CloudKit is available on all platforms
* Telemetry available on CloudKit Dashboard
* API Improvements
* New Feature—Sharing
  * Sharing System UI
  * Sharing APIs, Objects and Lifecycle
  * Configure your fallback URL!
