# react-native-socketio

## React native

``` Javascript
const ws = useRef(null);

const connectWebSocket = () => {
  ws.current = webSocket('ws://192.168.1.104:3000', { jsonp: false })
  
  ws.current.on('connect', () => {
    console.log('client connect success');
  });
  
  ws.current.on('message', msg => {
    console.log('get message from server: ', msg)
  })
}

const sendMessage = () => {
  ws.current.emit('message', 'send message to server')
}
```

- HOST URL 目前測試無法用 '0.0.0.0' 跟 '127.0.0.1'

## Python

Client 連接上時，會有 sid，可當作 client 的 ID
``` Python
@socketio.on('connect')
def connect():
    print("client connected with sid = ", request.sid)
```

指定 sid 去傳送訊息
``` Python
def send():
  socketio.emit('client_event', {'message': "to sid"}, to=request.sid)
```

接收 client 來的訊息
``` Python
@socketio.on('message')
def receive_message(msg):
    print('from: ', request.sid, 'msg: ', msg)
```
