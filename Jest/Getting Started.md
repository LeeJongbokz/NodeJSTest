

- Jest는 자바스크립트 테스팅 프레임웍으로, 간결함에 초점을 맞춤  


## 시작하기 

- yarn을 사용해서 설치할 수 있음 

```
yarn add --dev jest
```

- 혹은 npm을 사용해서 설치할 수 있음

```
npm install --save-dev jest
```

- 임의의 함수를 만들어서, 테스트 작성을 시작해보자.  
  먼저 sum.js를 만들어봄  
 
``` 
function sum(a, b){ 
   return a+b;
}
module.exports = sum;
``` 
 
- 그리고 sum.test.js라는 파일을 만듦.  
  이것은 실제 test를 포함하고 있음.  

```
const sum = require('./sum');

test('adds 1+2 to equal 3', () => {
  expect(sum(1,2)).toBe(3);
});
```

- package.json에 아래의 섹션을 추가함  

```
{
  "scripts": {
    "test": "jest"
   }
}
```

- 마지막으로 yarn test나 npm run test를 실행하면,  
  Jest가 아래 메시지를 출력함  

```
PASS ./sum.test.js
v adds 1 + 2 to equal 3 (5ms)
```

- 이제 Jest를 사용해 첫 번째 테스트를 성공적으로 마쳤습니다!  
- 이 테스트는 expect와 toBe를 사용했고, 그 두 값이 정확히 같았음  
  Jest가 테스트할 수 있는 다른 것들을 보려면,  
  https://jestjs.io/docs/using-matchers  
  이것을 보세요
  
  
## Command 라인에서 실행하기 

- Jest는 CLI에서 바로 실행할 수 있음  
  (만약 당신의 PATH에 globally available 하다면, 
   ex) yarn global add jest 
       npm install jest --global  
       
- 이것은 어떻게 my-test에 일치하는 파일들을 config.json을 설정 파일로 해서 실행하고  
  실행 후 native OS 노티를 보여줄 것인지에 관한 것임  

```  
  jest my-test --notify --config=config.json  
```  

- CLI에서 jest를 어떻게 실행할지에 대해서 더 알고 싶다면,  
  Jest CLI options를 보면 됨  
  

## 추가 설정

### 기본 설정 파일 생성하기 

- 프로젝트에 기초해, Jest는 몇 개의 질문을 묻고, 기본적인 설정 파일을 만들 것임  

```
jest --init  
```

### 바벨 사용하기  

- 바벨을 사용하기 위해서는, yarn을 사용해서 dependencies를 설치해야 함  

```
yarn add --dev babel-jest @babel/core @babel/preset-env  
```

- 프로젝트의 root에 babel.config.js를 만들고, 현재 버전의 Node를 타겟하기 위해,  
  바벨을 설정할 수 있음  


babel.config.js

```
module.exports = {
  presets: [['@babel/preset-env', {targets: {node: 'current'}}]], 
};
```

- 이상적인 바벨의 설정은 프로젝트에 따라 다를 수 있음  
  https://babeljs.io/docs/en/ 을 참고해봄  
  

### 웹팩 사용하기 

- Jest는 웹팩을 사용하는 프로젝트에 사용할 수 있음  
  웹팩은 assets, styles, compilation을 관리함  
  웹팩은 다른 툴들과는 달리 유니크한 도전을 제공함  
  https://jestjs.io/docs/webpack 을 참고해봄  
  
### Parcel 사용하기

- Jest는 parcel-bundler를 사용하는 프로젝트에 사용할 수 있음  
  Parcel은 설정이 필요 없음.  
  https://parceljs.org/docs/ 을 참고해봄  
  

### 타입스크립트 사용하기 

- Jest는 TypeScript를 바벨을 통해서 지원함  
  먼저 위의 바벨과 관련된 설명을 따라야 함.  
  그리고 나서, yarn을 이용해서 @babel/preset-typescript를 설치함  

```
yarn add --dev @babel/preset-typescript
```

- 그리고 나서 babel.config.js의 presets에 @babel/preset-typescript를 추가함 

babel.config.js

```
module.exports = {
presets: [
  ['@babel/preset-env', {targets: {node: 'current'}}],
  '@babel/preset-typescirpt',
  ],
};
```

- 그러나, Typescript를 바벨과 사용할 때 주의할 점이 있음  
  바벨에서 지원하는 Typescript는 순수히 transpilation만 지원하기 때문에
  Jest는 실행 시 테스트에 대한 type-check를 하지 않음  
  
- 만약 그것을 원한다면, ts-jest를 대신 사용하던가,  
  아니면 Typescript 컴파일러인 tsc를 독립적으로 사용해야 함  
  
- 만약 @types/jest 모듈을 사용하고 있는 Jest의 버전에 맞게 설치하고 싶을 수 있음  
  이것은 Typescript로 테스트를 작성할 때, full typing을 제공함  

```
yarn add --dev @types/jest
```













 
