# System Design Interview -- An Insider's Guide / Alex Xu / 2020

### Key Points:

#### Chapter 1: Scale
- **Vertical scaling**: Scale up. Add more power(CPU, RAM, etc.) to your servers. 
- **Horizontal scaling**: Scale-out. Add more servers into your pool of service.

#### Chapter 2 Estimation: 
- **Latency numbers**: *
- **Availability numbers**: *.
  
- #### Chapter 4 Rate limiter: 
- **API gateway**: middleware. Service tthat suppors rate limiting, SSL termination,authentication, IP whitelisting, servive static content.. 
- **Algs**:
    1. token bucket: a container that has pre-defined capacity. Each request consumes one token. Drop request if no token left. # Refill rate.
    2. leaking bucket: requests are processed at a fixed rate. Implemented with a FIFO que. # bucket size / queue size # outflow rate
    3. fixed window counter: devide timeline into fix-sized time window and assign a counter for each window. Drop request on reaching threshold. # Spike in traffic at the edge of a window could cause more requests than the allowed quota to go through.
    4. sliding window log: remove outdated timestamps, keep log size same the lower than the allowed count. 
    5. sliding window counter: mix 3 & 4.# Rolling minute.
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
- [**Exactly Once Delivery**:](https://bravenewgeek.com/you-cannot-have-exactly-once-delivery/) reduce duplication by adding dedupe logic after rety mechanism (for reliability)
- **Tracking and monitoring**: https://www.datadoghq.com/blog/rabbitmq-monitoring/

#### Chapter 11: News Feed System
- **Load balancer**: distribute feed rettrieval API traffic to web servers. 
- **Fanout service**: get friend IDs from graph db --> deliver news feeds to friends.
  
#### Chapter 12 Chat System: 
- **Connection**: HTTP keep-alive, polling(periodically ask, close connection each time), long polling(hold connection open util message available or timeout), websocket(upgraded to bidirectional and persistent)
- **Stateful service**: the chat service.
- **Service discovery (Apache Zookeeper)**: service whose primary job is to give the client a list of chat servers that the client could connect to. Provide new server for clients to establish connection with in case of a server goes offline.
- **KVStore**:
  1. user's online / offline status
  2. chat history data: for horizontal scaling, low access latency, long tail of data
  3. relational db got generic user data
- **Status fanout**:
  1. for small user group(<500):Presence server maintain channels(WebSocket, publish-subscribe) for each friend pair
  2. for larger groups:fetch online status only on refresh / new user enter
- **Wrap up**:
  1. chat server, presence server, KVstore, API store
  2. compression(text: gzip/bzip2), cloud storage, thumbnail
  3. end-to-end encryption: only sender and recipent can read messages
  4. cache: https://slack.engineering/flannel-an-application-level-edge-cache-to-make-slack-scale/
  
#### Chapter 13 Search AutoComplete System: 
- Re**trie**val and opt: limit max length of prefix / cache top search queries at each node 
- **Optimization**: AJAX request, browser caching(cache suggestions), data sampling(log 1 out of N requests)
- **Multiple language support**: unicode character. store tries in CDNs to build different tries for different contries to diffrentiate top search queries.
- TODO: Elastic search

#### Chapter 14 Youtube: 
- **DAG**: tasks defined in stages to be executed sequentially or parallely. DAG schedular, resource manager, task worker.

#### Chapter 15 Google Drive: 
- **Estimation**:
  1. 50 million signed up users, 10 million DAU.
  2. 10 GB free space / user. Total space allocated:  50 million * 10 GB = 500 Petabyte.
  3. 2 500 KB file uploaded.
  4. 1:1 read to write ratio.
  5. QPS for upload API: 10 million * 2 uploads / 24 hours/ 3600 seconds = ~ 240
  6. Peak QPS = QPS * 2 = 480
- **Storage**: AWS S3.
- **high-level design**: Block servers (split files to 4MB per block), cloud storage, cold storage, load balancer(evenly distribute request between API servers), API servers (everything other than the upload. i.e. authentication, managing user profile, upload file metadata) , metadata db & cache, notification service, offline backup queue.
  
### Vocabulary:
1. Bloom Filter
2. Timestamp
3. URL Frontier

### Reference
### further reading
