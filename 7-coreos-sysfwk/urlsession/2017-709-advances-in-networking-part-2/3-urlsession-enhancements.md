## [URLSession enhancements](3-urlsession-enhancements.md) | Stuart Cheshire | 2430 | p30



- ProgressReporting
- Brotli compression
- Public Suffix List updates
- URLSessionStreamTask and authenticating proxies


### URLSessionTask Progress Tracking

Old API for progress calculation

- Extra work for URLSession API clients
- Need Key-value Observing setup for
  - countOfBytesExpectedToReceive, countOfBytesReceived countOfBytesExpectedToSend, countOfBytesSent
- Not always available
  - countOfBytesExpectedToReceive countOfBytesExpectedToSend


Improved API for progress calculation (NEW)

- Implements ProgressReporting protocol
  - class URLSessionTask : NSObject, NSCopying, ProgressReporting
class URLSessionTask : NSObject, NSCopying, ProgressReporting
public var progress: Progress { get }


- URLSessionTask overall work completed
  - var fractionCompleted: Double [0.0, 1.0]
- General and more specific progress description
- Can attach Progress object to a UIProgressView or NSProgressIndicator
- Progress of multiple tasks by using a parent progress object
- Key-value observing and Cocoa bindings


### URLSession Brotli Support  (NEW)

- RFC 7932 “Brotli Compressed Data Format”
- `Content-Encoding: br`
- Faster URL loads
  - Median 15% improvement in compressed sizes versus gzip for text-based assets (HTML, JS, CSS, ...)
- Requires HTTPS (TLS)


### URLSession Public Suffix List

Effective top level domain list

- Public Suffix List
  - https://publicsuffix.org
- Heuristic to determine administrative boundaries
  - “apple.com” is one organization
  - “com.au” is many organizations

### URLSession Public Suffix List Updates (NEW)

Effective top level domain list

- URLSession can now receive updates over the air
- Update can be pushed biweekly (or even more frequently)  depending on the number of TLDs added to the list
- Better security for users against cookie attacks
  - URLSession APIs
  - HTTPCookieStorage


### URLSessionStreamTask

- Allows for direct TCP/IP connection to a host and port
- Optional secure handshaking (STARTTLS)
- Ability to convert to legacy NSInputStream/NSOutputStream
- For new code we recommend using native URLSessionStreamTask APIs
- Navigation of authenticating HTTPS proxies (NEW)

See 2015 Networking with NSURLSession

