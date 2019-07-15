```
sequenceDiagram
participant Host1 Fans
participant Host1
participant Server
participant agora Server
participant Host2
participant Host2 Fans
Host1->>Server:API:arena/apply
Server->>Host1:return success
Server->>Host2:StarPkArenaLinkApply = 87
Host2->>Host2:接受
Host2->>Server:API:arena/confirm
Server->>Host2:return success
Note over Server:下面的逻辑 邀请、随机一样
Server->>Host1:StarPkArenaLinkSuccess = 90
Server->>Host2:StarPkArenaLinkSuccess = 90
Host1->>Host1:倒计时
Host2->>Host2:倒计时
Host1->>Host1:开启30s超时定时器
Host1->>Server:API:room/p/querypub
Server->>Host1:return success
Host1->>agora Server:ijk→agora
Host1->>agora Server:joinChannel (加入自己的房间)
Host1->>agora Server:Host1 media data (Host1 sei)
Host2->>Host2:开启30s超时定时器
Host2->>Server:API:room/p/querypub
Server->>Host2:return success
Host2->>agora Server:ijk→agora
Host2->>agora Server:joinChannel (加入Host1的房间)
Host2->>agora Server:Host2 media data (Host2 sei)
agora Server->>Host1:Host2 media data
Host1->>Host1:移除30s超时定时器
agora Server->>Host2:Host1 media data
Host2->>Host2:移除30s超时定时器
Host1->>Server:API:arena/connSuccess
Host2->>Server:API:arena/connSuccess
Server-->>Host1 Fans:更新拉流地址(或者服务器流替换)
Server-->>Host2 Fans:更新拉流地址(或者服务器流替换)
Host1 Fans->>Host1 Fans:拉到的流有Host1 sei
Host1 Fans->>Host1 Fans:拉到的流有Host2 sei
Note over agora Server:Host1 Host2在同一房间 相同roomID
Note over Server:Host1 Host2分别在各自房间 不同roomID
```
