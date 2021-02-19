# 0217_미팅기록

> 서울4반_4팀 2021년 2월 17일 미팅기록

---

[TOC]

---



## 공지사항

> 발표준비, UCC 준비 잘 할 수 있도록!!

- 이송영 14시 교육생 간담회
- 이송영 16시 개인면담



## 주제

- UCC 촬영
- 코드 서버 업로드
- 버그 수정



## 내용

### 주요 업무

|  팀원  |         주요 업무          |
| :----: | :------------------------: |
| 강용욱 |           디버깅           |
| 박종원 |         Badge 작업         |
| 이규용 |   Badge 디자인, UCC 작업   |
| 이송영 | 더미 데이터 생성, 발표준비 |



### 주요 버그

> 코드를 서버에 올렸을 때 발생하는 주요 버그 및 그에 대한 해결법을 정리하였다.

#### :ballot_box_with_check: 회원가입 인증 메일이 도착하지 않는 버그

**원인**

- 이메일 인증 요청시, 개발자 중 한 명의 개인 메일로 인증 메일을 발송하도록 코드를 작성하였다.
- 동일한 하나의 메일로 인증 메일을 발송하도록 여러번 요청하다보니 해당 메일업체 측에서 보안 목적으로 요청을 deny한다는 것을 발견하였다.

**해결방안**

- 사이트의 url주소가 변경되었을 경우(예, localhost -> udong.shop),인증 메일을 보내주는 계정의 비밀번호를 재설정해준다.

#### :ballot_box_with_check: 사용자가 업로드한 이미지가 파일이 불러와지지 않는 버그

> 서버에 업로드 시 FE를 `npm run build`라는 명령어로 BE의 static 파일로 넣어 사용했다.

**원인**

- local에서는 `../upload/`이하에 저장되어 있는 이미지를 가져오도록 코드를 작성하였다.
- 하지만 서버에 올렸을 경우 `home/ec2-user/`이하의 폴더에 이미지가 저장되어 있다는 것을 발견하였다.
  - 예시: `/home/`ec2-user`/0218/uploads/userPost/"+url.get(0).substring(17);`
  - 여기서 `0218`은 개발자가 직접 작성한 폴더명이다.
- 이 때문에 경로를 찾는 부분에 있어서 오류가 발생한다는 것을 알게 되었다.

**해결방안**

- 서버 업로드시 저장되어 있는 이미지를 불러오는 코드를 수정하였다.

#### :ballot_box_with_check: 리뷰가 불러와지지 않는 버그

**원인**

- FE router에 BE와 동일한 주소가 존재했다.
  - `review/<int: review_id>`
- 이 때문에 url 요청시 충돌이 발생한다는 사실을 알게 되었다.

**해결방안**

- FE나 BE의 중복되는 주소 중 하나를 수정해서 중복되지 않도록 해준다.



## :hand: 다음과제

- 자세한 내용은 `jira` 참고