
## [New protocol support in NSURLSession](2-new-protocol-support-in-nsurlsession.md) | Andreas Garkuscha | 1310 | p33


HTTP/2 RFC 7540


- Why a new protocol?
- HTTP/2 in depth
- Adoption using NSURLSession


### Why a new protocol?

### HTTP/1.1 - Common issues

- One outstanding request
- HTTP pipelining
- Multiple connections
- Textual protocol overhead
- Header compression

### The Path to HTTP/2

- Experimental protocols
- Specification for HTTP/2
- IETF standardization, RFC

HTTP/1.1|HTTP/2
---|---
Multiple TCP connections to a host |Only one TCP connection
Head-of-line blocking|Fully multiplexed
FIFO restrictions|Requests have priorities
Textual protocol overhead|Binary
No header compression|Header compression (HPACK)


### HTTP/2 Header Compression



### HTTP/2 - Adoption on the client

- NSURLSession supports HTTP/2 protocol automatically
- No source code changes needed

### You Only Need an HTTP/2 Server


### HTTP/2 in NSURLSession - Compatibility

- Backward compatible with HTTP/1.1 servers
- Encrypted connection only
- HTTP/2 server requires ALPN or NPN support

### HTTP/2 Today - Current adoption

- HomeKit Remote Access via iCloud
- Services provided by Google and Twitter
- Open source web servers
- Content Delivery Network providers

### HTTP/2 -At a glance

- HTTP/2 is available in WWDC seed today
- Available in NSURLSession
- Enabled in Safari on OS X 10.11 and iOS 9

