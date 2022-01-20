
- 동기적인 코드를 작성하면 이렇게 작성할 수 있음  

```
const fs = require('fs');
const data = fs.readFileSync('./data.txt', 'utf8');
console.log(data);
```

- readFile이라는 비동기 함수를 쓸 때는 다름  
  첫 번째 parameter로 읽을 파일 경로를 주고,  
  그 다음에 마지막 parameter로는 콜백함수를 주게 되어 있음  

```
const fs = require('fs');
// const data = fs.readFileSync('./data.txt', 'utf8');
const data = fs.readFile('./data.txt', 'utf8', function(err,data){
    console.log(data);
});
console.log(data);
```

- 이렇게 비동기 함수를 실행하게 되면, 이 함수는 그냥 parameter를 넣은 다음 실행이 됨    
  파일을 읽을 때 까지 기다리지 않고, 노드는 다음 명령줄을 쭉 해석함  
  그리고 나서 파일을 다 읽었다고 이벤트가 발생하면,  
  그제서야 이 콜백함수가 동작함.  
  파일을 제대로 못 읽었으면, 에러라는 곳에 값이 할당되어 들어옴.  
  파일을 제대로 읽었으면, data라는 두 번째 parameter에 값이 들어옴.  
  
- Node에서는 데이터를 읽을 때, 동기화 코드보다는 비동기 코드를 많이 씀.  
  비동기를 쓸 때 조심해야 할 것이, 콜백 함수 스타일을 많이 쓴다는 것.  
  
  
  
  
