# System Design Interview -- An Insider's Guide / Alex Xu / 2020

### Key Points:

#### Chapter 1: Scale
- ****: . 
- ****: .
- ****: .

#### Chapter 2: 
- ****: . 
- ****: .
- ****: .
  
- #### Chapter 3: 
- ****: . 
- ****: .
- ****: .
  
- #### Chapter 4: 
- ****: . 
- ****: .
- ****: .

#### Chapter 5: Consistent Hashing
- Virtual nodes

#### Chapter 6: Key-Value Store
- **CAP Theorem**
- **Failure Detection**: Nodes send heartbeats to random nodes.
- **Failure Handling**:
  1. **Temporary**: Sloppy quorum – use available servers for reads and writes, push data when failed server recovers.
  2. **Permanent**: [Add details]

#### Chapter 7: UID Generator
- **Clock Synchronization**: NTP – Adjust clock based on network delay between client and server.

#### Chapter 8: URL Shortener
- **Design**: API for shortening and redirecting URLs (301/302 status codes).
- **Hash Functions**: CRC32, MD5, SHA-1 vs. Base 62 conversion.

#### Chapter 9: Web Crawler
- **Politeness & Priority**: URL frontier, queues.
- **Performance**: Cache DNS resolver (DNS is synchronous).
- **Data Validation**: Filter noise and redundancy.

#### Chapter 10: Notification System
- **Payload**: a JSON dictionary.
- **3rd party services**: APNs, FCM, SMS Services to push notifications
- [**Exactly Once Delivery**:](https://bravenewgeek.com/you-cannot-have-exactly-once-delivery/) reduce duplication by adding dedupe logic after rety mechanism( for reliability)
- **Tracking and monitoring**: https://www.datadoghq.com/blog/rabbitmq-monitoring/

#### Chapter 11: News Feed System
- **Load balancer**: distribute feed rettrieval API traffic to web servers. 
- **Fanout service**: get friend IDs from graph db --> deliver news feeds to friends.
  
#### Chapter 12 Chat System: 
- **connection**: HTTP keep-alive, polling(periodically ask, close connection each time), long polling(hold connection open util message available or timeout), websocket(upgraded to bidirectional and persistent)
- **stateless**: .
- **service discovery**: .
  
#### Chapter 13 Search AutoComplete System: 
- ****: . 
- ****: .
- ****: .
- elastic search

#### Chapter 14 Youtube: 
- ****: . 
- ****: .
- ****: .

#### Chapter 15 Google Drive: 
- ****: . 
- ****: .
- ****: .
  
### Vocabulary:
1. Bloom Filter
2. Timestamp
3. URL Frontier
