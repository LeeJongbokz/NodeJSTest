
- Javascript 코드가 비동기적으로 동작하는 경우는 흔합니다.  
  Jest는 테스트하는 코드가 끝나는 때를 알아야 하며,  
  그 이후에 다른 테스트로 넘어가야 합니다.  
  Jest에서는 이것을 다루기 위한 여러 가지 방법이 있습니다.  
  
  
### Callbacks

- 가장 일반적인 비동기 패턴은 콜백입니다. 
  예를 들어, 데이터를 fetch하는 fetchData(callback) 함수가 있고  
  그것이 끝났을 때, callback(data)를 호출한다고 합시다.  
  이 때, 이 리턴된 데이터가 문자열 'peanut butter'인지 알고 싶습니다.

- 기본적으로, Jest test는 실행의 끝에 도달하면 한 번 끝납니다. 
  그 의미는 테스트가 의도된 대로 실행되지 않는다는 것을 의미합니다. 

```
// Don't do this!
test('the data is peanut butter', () => {
  function callback(data){
    expect(data).toBe('peanut butter');
  }
  fetchData(callback);
});
```

- 문제는 테스트가 fetchData가 완료되자마자 callback이 실행되기도 전에 끝난다는 것임  
  
- 이것이 그것을 수정한 test의 다른 형식임. 
  테스트를 빈 argument로 함수에 넣는대신, done이라는 단일한 argument를 넣음.  
  Jest는 done 콜백이 호출될때까지 기다림. 
  
```
test('the data is peanut butter', done => {
  function callback(data) {
    try{
      expect(data).toBe('peanut butter');
      done();
    } catch (error) {
      done(error);
    }
    
    fetchData(callback);
});
```

- done()이 호출되지 않는다면, 테스트는 실패할 것임  
  
- 만약 expect statement가 실패하면, 잉것은 에럴르 던지고 done()이 호출되지 않음  
  우리가 테스트 로그에서 이것이 왜 실패했는지 보고 싶다면,  
  우리는 expect를 try 블록으로 감싸고, catch 블록의 done에 에러를 보내야 함  
  
- 그렇지 않다면, 우리는 불분명한 timeout error와 함께 끝이 나며, 
  expect(data)가 어떤 데이터를 받았는지 알 수 없게 됨  
  





