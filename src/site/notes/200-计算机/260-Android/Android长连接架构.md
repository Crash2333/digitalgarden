---
dg-publish: true
date: 2023-10-08
tags:
  - WebSocket
---
```plantuml

interface SocketService {  
    fun observeWebSocketEvent(): Flowable<WebSocket.Event>  
    fun sendPing(ping: String)  
    fun sendMsg(msg: String)  
}

interface ISocketHelper {  
    fun resolveMsg(msg: String)  
    fun sendMsg(msg: String)  
}


class SocketHelper{
	
}

class SocketManager{
	var webSocketService: SocketService
	fun onHeartBeat()
}


ISocketHelper <|.. SocketHelper
SocketHelper <-- SocketManager

```