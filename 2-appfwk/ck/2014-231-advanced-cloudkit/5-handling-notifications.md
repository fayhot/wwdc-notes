5-handling-notifications.md

## Handling notifications | 3150 | p201


### Subscriptions and Notifications - Recap

- Subscriptions are persistent queries
- Server sends a push notification
- Pushes are sent via Apple Push Notification Service


### Push Notifications Are Lossy

- No guarantees on delivery
- Server stores pushes (if you offline)
- Server only stores the latest push


### Push Notifications 

- Store and Forward
- Only the last push is delivered


### Notification Collection

like delta download. change token

### Dropped Notifications - It’s not just for airplane mode!

- Always check the notification collection
- Rapid pushes can cause coalescing
- Bad network conditions are common

