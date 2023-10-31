采用json封装格式

1. join加入房间
2. resp-json，当join房间之后发现房间里面已经存在一个人时则返回另一个人的uid；如果只有自己则不返回
3. leave离开房间后，服务器收到leave信令则检查同一房间内是否还有其他人，如果有则通知其他人有人离开
4. new-peer 服务端通知客服端有新人加入，收到new-peer则发起连接请求
5. peer-leave 服务器通知客服端有人离开
6. offer 转发offer sdp
7. answer 转发answer sdp
8. candidate 转发candidate sdp
## join
```javascript
var jsonMsg={
  "cmd":"join",
  "roomId":roomId,
  "uid":localUserId
}
```
## resp-json
```javascript
var jsonMsg={
  "cmd":"resp join",
  "remoteUid":remoteduid
}
```
## leave
```javascript
var jsonMsg={
  "cmd":"leave",
  "roomId":roomId,
  "uid":localUserId
}
```
## new-peer
```javascript
var jsonMsg={
  "cmd":"new-peer",
  "remotedUid":uid
}
```
## peer-leave
```javascript
var jsonMsg={
  "cmd":"peer-leave",
  "remoteUid":uid,
}
```
## offer
```javascript
var jsonMsg={
  "cmd":"offer",
  "roomId":roomId,
  "uid":localUserid,
  "remoteUid":remoteUserId,
  "msg":JSON.stringfy(sessionDescription)
}
```
## answer
```javascript
var jsonMsg={
  "cmd":"offer",
  "roomId":roomId,
  "uid":localUserid,
  "remoteUid":remoteUserId,
  "msg":JSON.stringfy(sessionDescription)
}
```
## candidate
```javascript
var jsonMsg={
  "cmd":"candidate",
  "roomId":roomId,
  "uid":localUserId,
  "remoteUid":remoteUserId,
  "msg":JSON.stringify(candidateJson)
}
```
## offer、answer、candidate信令实现

1. 收到new-peer，作为发起者创建RTCPeerConnection，绑定事件响应函数，加入到本地流
2. 创建offer sdp,设置本地sdp,并将offer sdp发送到服务器
3. 服务器收到offer，也创建RTCPeerConnection，绑定事件响应函数，加入到本地流中。
4. 接受者收到offer，也创建RTCPeerConnection，绑定事件响应函数，加入到本地流中。
5. 接收者设置远程sdp,并创建answer sdp,然后设置本地sdp，并将answer sdp发送到服务器
6. 服务器收到answer sdp转发给指定的remouteClient
7. 发起者收到answer sdp,则设置远程sdp
8. 发起者和接受者都收到ontrack回调事件，获取到对方的对象句柄
9. 发起者和接收者都开始请求打洞，通过oniceCandidate获取到打洞信息(candidate)被发送给对方
10. 如果P2P能够成功则进行P2P通话，如果P2P不成功，则进行中继转发通话。
