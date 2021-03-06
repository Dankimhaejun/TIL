# Regular Expression

>정규 표현식은 특정한 규칙을 가진 문자열의 집합을 표현하는 데 사용하는 형식 언어이다. 정규 표현식은 많은 텍스트 에디터와 프로그래밍 언어에서 문자열의 검색과 치환을 위해 지원하고 있다.



### Reg Exp

- /\d/g : 전체에서 숫자를 찾는다.
- /\D/g : 전체에서 숫자가 아닌것을 찾는다.
- /walli/g : 전체에서 walli가 포함되있는 문자열을 찾는다.
- /[a-z]/g : 전체에서 a~z 사이의 모든 문자를 찾는다.
- /[A-Z]/g : 전체에서 A~Z 사이의 모든 문자를 찾는다.
- /[a-zA-Z]/g : 전체에서 a~z, A~Z 를 찾는다.
- /\w/g : 전체에서 모든 문자(알파벳과 숫자)를 찾는다.
- /\w+/g : 전체에서 모든 단어를 찾는다.
- /\W/g : 전체에서 문자(알파벳과 숫자)가 아닌것을 찾는다.
- /\s/g : 전체에서 공백문자(space, tabs, linebreaks)를 찾는다.
- /\S/g : 전체에서 공백문자가 아닌것을 찾는다.
- /[aeiou]/g : 전체에서 a,e,i,o,u를 찾는다.
- /[ ^aeiou]/g : 전체에서 a,e,i,o,u가 아닌것을 찾는다.
- /(character)\b/g : 전체에서 단어의 끝이 (character) 로 끝나는 부분을 찾는다.
- /(character)\B/g : 전체에서 단어의 끝이 (character) 로 끝나지 않는 부분을 찾는다.



### Object

```javascript
let reg = new RegExp(pattern, 'g');
//patten에는 문자열이 들어갈 수 있다.
```



### Method

- String.match( pattern ) : 정규표현식에 해당하는 부분을 배열로 반환.
- String.replace( pattern, string ) : 정규표현식에 해당하는 부분을 string으로 치환.