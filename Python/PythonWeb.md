#### Websocket

前端

```javascript
const ws = new WebSocket("ws://127.0.0.1:2333")
  ws.onopen = function () {
    console.log("Connection open ...");
    ws.send("admin:123456")
  }
  ws.onmessage = function (evt) {
    console.log("Received Message: " + evt.data);
    ws.close();
  }
  ws.onclose = function (evt) {
    console.log("Connection closed.");
  }
```

后端

```python
import asyncio # 是用来编写 并发 代码的库，使用 async/await 语法
import websockets # 处理websocket

# 接受请求
async def webRes(websocket):
    while True:
        recv_str = await websocket.recv()
        # 设置安全词（输入即退出）
        if recv_str == "Bazinga!":
            response_str = "This connection is end"
            await websocket.send(response_str)
            return True
        else:
            response_str = f"your submit context: {recv_str}"
            await websocket.send(response_str)

# 服务器端主逻辑
# websocket和path是该函数被回调时自动传过来的，不需要自己传
async def main_logic(websocket, path):
    await webRes(websocket)
    
# 把ip换成自己本地的ip
start_server = websockets.serve(main_logic, '127.0.0.1', 2333)
asyncio.get_event_loop().run_until_complete(start_server)
asyncio.get_event_loop().run_forever()

# 如果要给被回调的main_logic传递自定义参数，可使用以下形式
# 一、修改回调形式
# import functools
# start_server = websockets.serve(functools.partial(main_logic, other_param="test_value"), '10.10.6.91', 5678)
# 修改被回调函数定义，增加相应参数
# async def main_logic(websocket, path, other_param)
```



#### CORS

前端（我测试是用axios.get能成功）

```javascript
axios
    .get('http://127.0.0.1:2333/cros', { params: {a:1} })
    .then((res) => {
        console.log (res)
    })
    .catch((err) => {
        console.log (err)
    });
```

后端

```python
from flask import Flask, Response
app = Flask(__name__)

@app.route('/cors')
def cors():
    res = Response('It is ok by Access-Control-Allow')
    res.headers['Access-Control-Allow-Origin'] = 'http://127.0.0.1:3000'
    # res.headers['Access-Control-Allow-Origin'] = '*'
    res.headers['Access-Control-Allow-Methods'] =  'GET'
    # res.headers['Access-Control-Allow-Methods'] =  'GET, POST'
    return res


if __name__ == "__main__":
    app.run(port=2333)
```



另一种方法

```
pip install flask-cors
```

前端

```javascript
axios({
    url: 'http://127.0.0.1:2333/cros',
    method: 'POST',
    data: {a:1}
})
.then((res: any) => {
    console.log (res)
})
.catch((err) => {
    console.log (err)
});
```

后端

```python
@app.route('/cors', methods=['GET', 'POST'])
@cross_origin()
def cors():
    res = Response('It is ok by Access-Control-Allow')
    return Response
```



应对fetch

```javascript
fetch('http://127.0.0.1:2333/cors')
    .then(response => response.json())
    .then(json => console.log(json))
    .catch(err => console.log('Request Failed', err));
```



```
@app.route('/cors', methods=['GET', 'POST'])
@cross_origin()
def cors():
    return jsonify({'a': 1, 'b': 2})
```





#### Nignx配history

```
start nignx

nignx -s stop
```

