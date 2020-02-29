# Express - MySQL 

### DB config 설정

```js
//mysql.js

var mysql      = require('mysql');
var db = mysql.createConnection({
  host     : 'localhost',
  user     : '< MySQL username >',
  password : '< MySQL password >',
  port     : < port >,
  //
  database : 'my_db'
});

// 연결 실행
db.connect();

//외부에서 mysql.js를 불러왔을 때 query함수로 쉽게 사용할 수 있도록 모듈화
function query(queryState,callback = ()=>{}){
  db.query(queryState,(err,rows)=>{
    if(err) throw err;
    let result = JSON.parse(JSON.stringify(rows));
    //내가 입력한 callback함수에 result 내용을 넣고 실행
    callback(result)
  });
};

exports.db = db;
exports.query = query;
```



* 데이터 타입: [http://www.incodom.kr/DB_-_%EB%8D%B0%EC%9D%B4%ED%84%B0_%ED%83%80%EC%9E%85/MYSQL](http://www.incodom.kr/DB_-_데이터_타입/MYSQL)

##### 컬럼 생성 시 옵션 및 의미

1. **Not Null**

   * 해당 컬럼 값으로 NULL을 허용하지 않음
   * (행 단위) 입력시 데이터를 무조건 받음
   * <u>유일하지 않고, 반드시 입력 또는 수정해야 할 컬럼에 설정</u>

2. **Unique**

   * 테이블 내에서 해당 컬럼값은 항상 **유일무이**한 값을 가질 것

   * 중복을 허용하지 않음

   * 중복 데이터는 방지하지만, <u>NULL의 중복은 방지하지 못함</u>

   * ADD NOT NULL은 불가능

     &rarr; 테이블 내의 모든 컬럼은 특별한 설정(NOT NULL 또는 PRIMARY KEY)을 하지 않았을 경우 NULL값이 기본으로 설정되어짐.
   
3. **Primary Key (기본키)**

   * 해당 컬럼 값은 **반드시 존재해야 하고 유일해야 한다**는 조건
   * NOT NULL과 UNIQUE 조건을 동시에 만족함
   * 테이블 내에서 서로 다른 행을 구분하기 위해서 사용
   * 한 테이블 내에 <u>단 한개의 PRIMARY KEY</u>만 존재

4. **Binary**

   * 데이터 바이너리 타입으로 변환하는 것으로 예상됌(자료 미확인..)

5. **Unsinged**

   * 숫자형 데이터 중 범위가 음수 ~ 양수 까지의 범위를 가지는 데, 음수가 필요하지 않을 때 체크하면 0~양수의 범위로 책정되면서 음수의 범위까지 양수로 넘어간다.

   * -2147483648 ~ 2147483647 &rarr; 0 ~ 4294967295

     출처: https://ellieya.tistory.com/134 [엘리네집]

6. **Zero Fill**

   * 괄호안의 숫자만큼 빈칸을 0으로 채우라는 의미

   * INT 와 같은 숫자형을 쓸 때 유의미 한 형식

   * ```mariadb
     create table TEST(seq INT(11) not null auto_increment primary key, \
     oops1_fillzero INT(1) zerofill, \
     oops1_nozero INT(1) , \
     oops2_fillzero INT(2) zerofill, \
     oops2_nozero INT(2) , \
     oops3_fillzero INT(3) zerofill, \
     oops3_nozero INT(3) \
     );
     
     ```

     &rarr; result: 1, 1, 01, 1, 001, 1, 0001, 1

##### 회원가입 구현

```js
router.route('/signup')
.post(async (req, res, next) => {
  const email  = req.body.email,
  password     = req.body.password,
  username     = req.body.username,
  phone        = req.body.phone,
  verifyNumber = req.body.verifyNumber;
  let verify, result;

  /** 
   * NOTE: result 값 
   * 1: 가입 완료
   * 2: 무엇인가의 에러로 인한 실패
   * 3: 인증 실패
   * 4: 중복 체크
   * */ 
  if(verifyNumber.length === 0){
    result = { result: 3 };
    res.json(result)
  } else {
    verify = 1;
    db.query(`select * from showplex.user where email="${email}"`, (err, results) => {
      if(err) throw err; // error 메세지 반환
      console.log(results, 'BACK:: Result'); //결과값  출력
      if(results.length > 0 ){
        res.json({ result: 4 });
      } else {
        // 회원가입
        db.query(`insert into showplex.user (email, password, username, phone, verifyNumber, verify) values ("${email}", "${password}", "${username}", "${phone}", "${verifyNumber}", "${verify}")`, (error, results) => {
          if(error){
            result = { result: 2 };
            res.json(results);
            console.log(`Error: 2 : ${error}`);
          } else {
            result = { result: 1 };
            res.json(result);
            console.log(`Success ! ${results}`);
          };
        });
      };
    });
  };
});
```

* `db.query` 함수를 쓸 때 들어가는 `querystate`값은  MySQL에서 나오는 쿼리문을 넣으면 된다. 단, insert 되어야 할 값들의 수와 values 값들의 수는 일치해야한다.
  &rarr; 틀릴 경우 `Error: ER_WRONG_VALUE_COUNT_ON_ROW: Column count doesn't match value count at row 1` 라는 오류 메세지를 보게 될 것이다.
* 여기에선 `async` 함수만 썼는데, `async` 함수의 반환값은 `promise`객체를 항상 반환한다. 그래서 `async` 함수의 리턴값에서 `then` method를 쓸 수 있음.
  참고: [자바스크립트-콜백부터-async-await까지-비동기-처리](https://velog.io/@ashnamuh/자바스크립트-콜백부터-async-await까지-비동기-처리)

참조: https://fora.tistory.com/61, 

