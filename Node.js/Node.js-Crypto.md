# Crypto

### 단방향 암호화

* 해시 함수를 이용함. 단, 단순하게 해시만 할 경우 변환된 결과를 보고 원래 문자열을 알아낼 수 있다.
* 그러므로 `salt`를 이용하여 단순 해쉬의 결과를 좀 더 변형한다.

```js
crypto.randomBytes(64, (err, buf) => {
  crypto.pbkdf2('비밀번호', buf.toString('base64'), 100000, 64, 'sha512', (err, key) => {
    console.log(key.toString('base64'));
  });
});
//'dWhPkH6c4X1Y71A/DrAHhML3DyKQdEkUOIaSmYCI7xZkD5bLZhPF0dOSs2YZA/Y4B8XNfWd3DHIqR5234RtHzw=='
```

##### `crypto.randomBytes(size, [, callback])`

| parameter      | type     |
| -------------- | -------- |
| size           | Number   |
| callback       | Function |
| callback - err | Error    |
| callback - buf | Buffer   |

* Returns: 만약 `callback`함수 부분이 없다면 `Buffer`를 반환한다.
* Parameter
  * size: 생성할 Byte 수. 위의 예제코드에서는 64Byte의 길이를 생성.
* 제로초 코드에서는 반환된 `Buffer`로 `salt` 값으로 사용



##### `crypto.pbkdf2(password, salt, iterations, keylen, digest, callback)`

| prameter               | type                                             |
| ---------------------- | ------------------------------------------------ |
| password               | String \|\| Buffer \|\| TypedArray \|\| DataView |
| salt                   | String \|\| Buffer \|\| TypedArray \|\| DataView |
| interactions(반복횟수) | Number                                           |
| keylen(비밀번호 길이)  | Number                                           |
| digest(해시 알고리즘)  | String                                           |
| callback               | Function                                         |
| callback - err         | Error                                            |
| callback - derivedKey  | Buffer                                           |

* 비동기 방식으로 `PBKDF2(Password-Based Key Derivation Function 2 )` 함수(?)를 실행한다.
* 위 randomBytes가 버퍼형태로 리턴되므로, `buf.toString('base64')`로 문자열로 변경.
* 반복횟수 10만번으로 해도 시간이 생각보다 걸리지 않으며 불규칙한 정수로 사용할 것.
* `salt` 값을 하나의 Key값처럼 별도로 저장해두는 것이 좋다.
  &rarr; 위의 코드 처럼 `randomBytes`를 이용해서 만들어내면 매번 암호화 결과가 달라져버리기 때문.

##### 비교할 때

```js
crypto.pbkdf2('입력비밀번호', '기존salt', 100000, 64, 'sha512', (err, key) => {
  console.log(key.toString('base64') === '기존 비밀번호');
});
```



참고링크 : [제로초 블로그](https://www.zerocho.com/category/NodeJS/post/593a487c2ed1da0018cff95d), [Node.js문서](https://nodejs.org/api/crypto.html#crypto_crypto_pbkdf2_password_salt_iterations_keylen_digest_callback)

