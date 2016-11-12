#SessionDB
----
Web Storage의 두 객체인 sessionStorage와 localStorage를 임시 DB로 사용할 수 있는 툴. H2 Database와 같은 in memory DB를 사용할 수도 있지만 그 보다 더 간단하게(아무런 설정이 없음) 프로토타입을 개발할 수 있는 장점이 있다. 다만 Web Storage를 사용하는 만큼 로컬에서만 확인이  가능한 단점도 고려를 해야 한다. 
###특징

- Web Storage 기반이므로 서버 구축 없이 로컬 환경에서 사용 가능
- JSON 기반의 schemeless DB
- 간단한 구현으로 데이터 저장소 역할 정도로 제한됨
- sessionStorage와 localStorage의 특성을 그대로 따름

###용도

- 빠른 프로토타입을 만들어 전체 흐름을 훑어보기 위해서
- 프로젝트 초기 네트워크 환경이 갖춰지지 않은 곳에서 간이 DB로 사용

###소스 코드 

Repositary : [https://github.com/mazdah/SessionDB]

Core module : cmsessiondb.js
기능 사용을 위해서는 cmsessiondb.js만 있으면 됨. 나머지 파일들은 모두 Admin 화면을 위한 소스들임.

###API

기본 객체 : SessionDB. SessionDB.함수명으로 API 호출

> SessionDB.insertRow(tblNm, rowData);

####함수

**SessionDB.init(tableType)**
```
@ SessionDB 초기화 : sessionStorage를 사용할 것인지, localStorage를 사용할 것인지 설정
@ parameter : tblType String ('session' 또는 'local')
@ return : 
```

**SessionDB. createTable(tblNm)**
```
 @ 전달받은 파라미터를 이름으로 하는 테이블 생성. 테이블의 기본 구조는 'table'을 키로 하는 배열로
   {"table":[]} 형태임
 @ parameter : tblNm String (테이블 이름, 문자열)
 @ return : boolean
```

**SessionDB. getTableList()**
```
 @ 테이블 목록 조회. 현재 storage에 생성된 테이블 목록을 가져옴
 @ parameter : 
 @ return : 테이블 이름이 담긴 JSNON 배열 객체
```

**SessionDB. dropTable(tblNm)**
```
 @ 테이블 Drop. 생성된 테이블 이름을 키로 하는 객체를 지움.
 @ parameter : tblNm String (테이블 이름, 문자열)
 @ return : 
```

**SessionDB. importTable(tblNm, dataArr, mode)**
```
 @ 테이블에 다수의 데이터 import
 @ parameter : 
   tblNm String (테이블 이름, 문자열), 
   dataArr JSON array (입력할 데이터 객체 배열), 
   mode String (기존 데이터에 추가할 것인지 전체 테이블을 대체할 것인지에 대한 플래그)
 @ return : number (import된 데이터 건수)
```

**SessionDB. insertRow(tblNm, rowData)**
```
 @ 테이블에 1건의 데이터 insert
 @ parameter : 
   tblNm String (테이블 이름, 문자열), 
   rowData String (JSON 포맷의 문자열)
 @ return : 0 - insert 실패, 1 - insert 성공
```

**SessionDB. getTable(tblNm)**
```
 @ 파라미터로 전달된 이름의 테이블 가져오기
 @ parameter : tblNm String (테이블 이름, 문자열)
 @ return : String (테이블 정보가 담긴 JSON 포맷 문자열)
```

**SessionDB. selectRow(tblNm, param)**
```
 @ tblNm이름을 가진 테이블에서 param과 동일한 key:value쌍을 가진 데이터 select
 @ parameter : 
   tblNm String (테이블 이름, 문자열), 
   param JSON object (key:value 쌍의 기본적인 JSON 객체)
   (param의 예 : {"name":"홍길동","email":"gdhong@gmail.com"})
 @ return : Array object (param 조건에 맞는 데이터 객체의 배열)
```

**SessionDB. deleteRow(tblNm, col, val)**
```
 @ tblNm 테이블에서 col 키의 값이 val인 데이터 delete
 @ parameter : 
   tblNm String (테이블 이름, 문자열), 
   col String (삭제할 조건이 되는 key), 
   val String (삭제할 조건이 되는 값)
 @ return : number (실패 : 0, 성공 : 삭제된 데이터 건수)
```

**SessionDB. updateRow(tblNm, col, val, param)**
```
 @ tblNm 테이블에서 col 키의 갑시 val인 row를 찾아 param 내의 키들과 동일한 키들의 값을 
   param 내의 value들로 update
 @ parameter : 
   tblNm String (테이블 이름, 문자열), 
   col String (업데이트할 조건이 되는 key), 
   val String (업데이트할 조건이 되는 값), 
   param JSON object(업데이트할 데이터)
 @ return : number (실패 : 0, 성공 : 삭제된 데이터 건수)
```

###개발자 정보
- Blog : [http://mazdah.tistory.com]
- Twitter ID: mazdah70
- Facebook : [https://www.facebook.com/profile.php?id=100000967897658]
- Project : [https://github.com/mazdah/SessionDB]

###ETC
2일만에 후딱 개발하고 배포합니다. 아직 부족한 부분이 많지만 개인 프로젝트에서 프로토타입을
개발하거나 프로젝트 초기에 네트워크 환경이 준비 안되었을 때 사용하면 좋을 것 같습니다.
너무 간단한 프로그램이라 별로 업데이트 할 것도 없지만 의견 주시면 가능한 한 반영해보기로
하겠습니다.

참고로 core 모듈인 cmsessiondb.js에 대해서는 사용상의 아무런 제약이 없으나 Admin 화면과
관련된 소스들은 AdminLTE를 가져다 쓴 것이기 때문에 해당 라이센스를 따라야 합니다.

감사합니다.
