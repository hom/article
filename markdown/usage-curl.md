# curl

## 参数

### Usage

```bash
curl [options...] <url>
```

## 实例

### 获取页面

```bash
curl www.sina.com
```

保存页面  

```bash
curl -o [file name] www.sina.com
```

### 自动跳转

```bash
curl -L www.sina.com
```

### 显示头信息

#### 显示`response`头部信息和页面

```bash
curl -i www.sina.com
```

#### 仅显示`response`头部信息

```bash
curl -I www.sina.com
```

### 显示通信过程

#### 显示整个通信过程

```bash
curl -v www.sina.com
```

#### 现实更详细的通信过程

```bash
curl --trace output.txt www.sina.com
```

或者  

```bash
curl --trace-ascii output.txt www.sina.com
```

### 发送表单数据

#### `GET`

```bash
curl example.com/form.cgi?data=xxx
```

#### `POST`

```curl
curl -X POST --data "data=xxx" example.com/form.cgi
```

添加表单编码

```bash
curl -X POST--data-urlencode "date=April 1" example.com/form.cgi
```

### `HTTP`动词

> `-X`参数表示请求的方式

```bash
curl -X POST www.example.com
```

### 表单上传

```bash
curl --form upload=@localfilename --form press=OK [URL]
```

### `Referer`字段

```bash
curl --referer http://www.example.com http://www.example.com
```

### `User Agent`字段

```bash
curl --user-agent "[User Agent]" [URL]
```

### `cookie`

#### 发送`cookie`

```bash
curl --cookie "name=xxx" www.example.com
```

#### 保存服务器返回的`cookie`到文件

```bash
curl -c cookies http://example.com
```

#### 从文件中读入`cookie`

```bash
curl -b cookies http://example.com
```

### 增加头部信息

```bash
curl --header "Content-Type:application/json" http://example.com
```

### `HTTP`认证

```bash
url --user name:password example.com
```