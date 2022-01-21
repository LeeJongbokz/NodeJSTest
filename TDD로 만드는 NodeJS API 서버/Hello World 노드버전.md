

- 여기까지 Node에 대해서 간단히 살펴봤고,  
  본격적으로 Hello World 코드를 보면서 노드에 대해서 알아봄  
  

- Hello World 코드는 노드 문서에 보시면 자세히 나와있음  
  그것을 복사해서 그대로 가져옴.  
  
```
const http = require('http');

const hostname = '127.0.0.1';
const port = 3000;

const server = http.createServer((req, res) => {
  res.statusCode = 200;
  res.setHeader('Content-Type', 'text/plain');
  res.end('Hello, World!\n');
});

server.listen(port, hostname, () => {
  console.log(`Server running at http://${hostname}:${port}/`);
});
```

- 붙여넣고 저장한 다음에 바로 실행해 봄.  
  Hello World 코드를 저장했고, 다시 node index.js라고 치면,  
  이렇게 메시지가 출력이 됨  
  
- 실제 이 코드를 테스트해보려면,  
  터미널을 하나 더 띄워서, 위에 터미널, 아래 터미널 나눠서 함.  
  
```
curl -x GET 'localhost:3000'
```
  
