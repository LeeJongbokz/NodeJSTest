

## Matchers 사용하기 

- Jest는 matchers를 사용해서 값을 여러 방식으로 테스트 함  
  이 문서는 일반적으로 사용되는 몇 가지 matchers를 소개함  
  

### 일반적인 Matchers

- 값을 테스트하는 가장 간단한 방법은 정확한 동등함을 보는 것임  
  
``` 
test('two plus two is four', () => {
 expect(2 + 2).toBe(4);
});
```

- 이 코드에서 expect(2+2)는 expectation 객체를 반환함  
  일반적으로 expectation 객체로 많은 것을 하지는 않음  
  이 코드에서 .toBe(4)는 matcher임.  
  Jest가 실행될 때, 이것은 모든 failing matchers를 트래킹하고,  
  훌륭한 에러 메시지를 프린트 아웃해줌  
  
- toBe는 Object.is를 사용해서 정확한 동등함을 테스트함  
  object의 value를 테스트해보고 싶으면,  
  toEqual을 대신 테스트함  
  
```
test('object assignment', () => {
   const data = { one: 1 };
   data['two'] = 2;
   expect(data).toEqual({one: 1, two: 2 });
});
```

- toEqual은 재귀적으로 object 혹은 배열의 모든 필드들을 검사함  

- 또한 matcher의 반대도 테스트해볼 수 있음  

```
test('adding positive numbers is not zero', () => {
  for(let a = 1; a < 10; a++){
    for(let b = 1; b < 10; b++){
        expect(a+b).not.toBe(0);
    }
  }
});
```

### Truthiness

- 테스트에서, 때때로 undefined, null, false를 구분해야 함   
-> 하지만 이것들을 다르게 취급하고 싶지 않을 수 있음  
-> Jest는 helpers를 갖고 있고, 이것은 테스터가 어떤 것을 원하는지 명시해줌

- toBeNull은 오직 null과 match됨  
- toBeUndefined는 오직 undefined와 match 됨
- toBeDefined는 toBeUndefined의 반대임  
- toBeTruthy는 if문이 참일 때 match됨  
- toBeFalsy는 if문이 거짓일 때 match됨

- 예를 들어,

```
test('null', () => {
  const n = null;
  expect(n).toBeNull();
  expect(n).toBeDefined();
  expect(n).not.toBeUndefined();
  expect(n).not.toBeTruthy();
  expect(n).toBeFalsy();
});
```

```
test('zero', () => {
  const z = 0;
  expect(z).not.toBeNull();
  expect(z).toBeDefined();
  expect(z).not.toBeUndefined();
  expect(z).not.toBeTruthy();
});
```

- 코드가 동작하기를 원하는데로 동작하게 하고 싶다면 matcher를 사용해야 함  


### Numbers

- 숫자의 비교는 matcher equivalenets가 있음  

```
test('two plus two', () => {
   const value = 2 + 2;
   expect(value).toBeGreaterThan(3);
   expect(value).toBeGreaterThanOrEqual(3.5);
   expect(value).toBeLessThan(5);
   expect(value).toBeLessThanOrEqual(4.5);
   
   expect(value).toBe(4);
   expect(value).toEqual(4);
});
```

- 소수점 비교에 대해, toBeCloseTo를 toEqual대신 사용할 수 있음  
  
```
test('adding floating point numbers', () => {
   const value = 0.1 + 0.2;
   expect(value).toBeCloseTo(0.3);
});
```


### Strings

- toMatch를 사용해서 일반적인 expressions에 반하게 string을 검사할 수 있음  

```
test('there is no I in team', () => {
   expect('team').not.toMatch(/I/);
});

test('but there is a "stop" in Christoph', () => {
   expect('Christoph').toMatch(/stop/);
});
```


### Arrays and iterables 

- 배열 혹은 iterable이 특정한 item을 갖고 있는지 toContain으로 검사할 수 있음  

```
const shoppingList = [
  'diapers',
  'kleenex',
  'trash bags',
  'paper towels',
  'milk',
];

test('the shopping list has milk on it', () => {
   expect(shoppingList).toContain('milk');
   expect(new Set(shoppingList)).toContain('milk');
});
```


### Exceptions  

- 특정 함수가 실행될 때 error를 내뱉는지 테스트하려면,  
  toThrow를 사용함  
  
```
function compileAndroidCode(){
  throw new Error('you are using the wrong JDK');
}
  
test('compiling android goes as expected', () => {
    expect(() => compileAndroidCode()).toThrow();
    expect(() => compileAndroidCode()).toThrow(Error);
    
    expect(() => compileAndroidCode()).toThrow('you are using the wrong JDK');
    expect(() => compileAndroidCode()).toTrhow(/JDK/);
});
```




















