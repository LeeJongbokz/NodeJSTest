
- 자바스크립트는 비동기 코드가 참 많음  
  노드도 마찬가지임  
  파일을 읽을 때도 비동기로 읽어야 하고,  
  네트워크 통신을 할 때도 다 비동기로 처리가 됨  
  

- 이것은 Java나 PHP처럼 동기적으로 수행하는 코드와는 크게 다른점임  
  그래서 Node로 코딩을 할 때는, 비동기 처리에 대해서 익숙해져야 함  
  우선, 어떻게 차이가 있는가 보여드림  
  
- Node에 보면 파일 시스템이라는 모듈이 있음  
  예제를 위해서 파일 시스템을 써 봄  
  노드 사이트에 가서 문서 메뉴로 가서
  우리가 사용하고 있는 6.10.0 API를 살펴봄  
  여기 보면 파일 시스템이라는 메뉴가 있음  
  

- 파일 시스템 메뉴 중에 readFile이라는 메뉴가 있음  
  readFile이 있고, readFileSync라는 것이 있음  
  똑같은 역할을 하는 함수인데,  
  위에 있는 것은, 비동기로 동작하고,  
  아래에 있는 것은, 동기로 동작함.  
  그러면 readFileSync라는 메소드를 통해서 파일을 한 번 읽어봄  
  
- 이번에는 텍스트 파일을 하나 만들어봄  
  data.txt라는 파일을 만듦  
  
- 다시 index.js로 가서 파일 시스템이라는 변수에 fs 모듈을 불러옴  
  fs에서 readFileSync를 한 다음에 읽을 파일 경로명을 적어줌  
  data.txt를 가져와서 data라는 변수에 할당함 
  그리고 실제 데이터가 로딩이 되었는가 출력을 해봄  
```
const fs = require('fs');
const data = fs.readFileSync('./data.txt');
console.log(data);
```

- 두 번째 파라미터에 객체가 아니라, utf8을 줌  
  그러면 This is data file이라는 문자열이 출력이 됨  
  
```
const fs = require('fs');
const data = fs.readFileSync('./data.txt', 'utf8');
console.log(data);
```
  
  
  
