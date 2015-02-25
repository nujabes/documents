# METEOR 노트
===

## Deny, Allow
deny에 true인자가 들어오면 실행이 안되고.
allow에 false인자가 들어오면 실행이 안된다.


## LINKS

[Meteor Korea](http://www.meteorjs.kr/)
[Meteor 1.0.2.1 Documentation](http://docs.meteor.com/#/full/quickstart)
[Meteor 0.9.1.1](http://kr-docs.meteor.com/)
[discovery 소스](https://github.com/SachaG/Microscope)
[Development – Jason Im](http://jasonim.me/category/dev)
[강좌와 팁 - meteor - collection2 패키지 README 번역...](http://forum.falinux.com/zbxe/index.php?mid=lecture_tip&document_srl=828069)
[6 Must-Use Meteor Packages for (Almost) Every Project](http://www.sitepoint.com/6-must-use-meteor-packages-almost-every-project/)

## 메서드 호출 대 클라이언트에서의 데이터 가공
메서드 호출은 다음의 몇 가지 시나리오에서 더 적합하다:

반응성과 동기화가 전파되는 것을 기다리기 보다는 콜백을 통해 값을 리턴하거나 알아야 할 필요가 있는 경우.
대형의 컬렉션을 전송하기에는 너무 부담되는 무거운 데이터베이스 함수의 경우.
데이터를 요약하거나 모으기 위한 경우(예, 수량, 평균, 합계 등).

우리는 필요한 만큼 allow 콜백을 정의할 수 있다. 단지 변경이 발생했을 때 그 콜백들 중에서 최소한 하나만 true를 리턴하면 된다.
유사한 방식으로 하나 이상의 deny 콜백을 정의할 수 있다. 만약 이들 가운데 어느 것이라도 true를 리턴하면, 변경은 취소되고 403이 리턴된다. 이 로직은 성공적인 insert를 위해서는 하나 또는 그 이상의 allow와 모든 deny 콜백이 실행된다는 것을 의미한다.



## !!연산자 (doutble exclamation) 

`!!userId is the same as Boolean(userId)`

!!foo applies the unary not operator twice and is used to cast to boolean type similar to the use of unary plus +foo to cast to number and concatenating an empty string ''+foo to cast to string.

Instead of these hacks, you can also use the constructor functions corresponding to the primitive types (without using new) to explicitly cast values, ie

    Boolean(foo) === !!foo
    Number(foo)  === +foo
    String(foo)  === ''+foo

It's just the logical NOT operator, twice - it's used to convert something to boolean, e.g.:

    true === !!10
    false === !!0


## 서버와 클라이언트에서의 db 접근
- 서버
```meteor mongo
> db.posts.insert({title: "A new post"});
> db.posts.find();
{ "_id": ObjectId(".."), "title" : "A new post"};
```

- 클라이언트
```❯ Posts.findOne();
{title: "A new post", _id: LocalCollection._ObjectID};
```

클라이언트에서 컬렉션은 좀 더 흥미롭다. 클라이언트에서 Posts = new Meteor.Collection('posts'); 라고 선언하는 것은, 실제 Mongo 컬렉션의 로컬, 인-브라우저 캐시를 생성하는 것이다. 우리가 클라이언트 쪽의 컬렉션을 “캐시"라고 말하는 것은, 데이터의 부분 집합을 가지며, 데이터에 빠르게 접근할 수 있다는 것을 의미한다.

이 부분을 이해하는 것이 이것이 미티어가 작동하는 방식의 기본이라는 점에서 중요하다. 일반적으로, 클라이언트 쪽 컬렉션은 Mongo 컬렉션에 저장된 전체 도큐먼트의 부분집합이다.(결국, 우리는 전체 데이터베이스를 클라이언트로 보내는 것을 원하지 않는다).

두 번째, 이 도큐먼트들은 브라우저 메모리에 저장되는 데, 이는 여기에 접근하는 것이 기본적으로 순간적이라는 것을 의미한다. 그러므로 클라이언트에서 Posts.find()를 호출할 때, 데이터를 가져오려고 서버나 데이터베이스에 느리게 갔다오는 일은 없다. 데이터는 이미 로드되어 있기 때문이다.



## [spectrum | Atmosphere](https://atmospherejs.com/spectrum/~starred)
<https://atmospherejs.com/spectrum/~starred>
> 다들 선호하시는 패키지들이 있겠죠?
> 같이 공유하면 좋겠네요.
> 일단 저부터
> coffeescript : {}, [], function 너무 귀찮아. 커피를 안해본 사람은 있지만 한번만 해본 사람은 없...나?
> less : 계층구조를 만들 수 있죠. css의 지겨운 중복이 싫다면. sass는 사양합니다.
> fastclick : 모바일은 mouseup 이벤트 딜레이가 심하죠. 꼭 써야합니다!
> aldeed:collection2 : 진리의 collection2. 두번쓰세요.
> reywood:publish-composite : 복잡한 publish가 필요하다면?
> meteorhacks:subs-manager : subscribe를 캐슁해줍니다. 그냥 껴줬음.
> mrt:moment : 시간관련 종결자.
> thepumpinglemma:chance : 뭐든지 랜덤 생성. 짱재미. http://chancejs.com
> lepozepo:accounting : 돈 관련 종결자. 시간과 돈만 해결하면 반은 먹고 들어가...나?
> fortawesome:fontawesome : 벡터아이콘이 필요한가요? 그렇다면 (왜 네임스페이스 fortawesome;; )
> aldeed:autoform : collection2 친구. admin정도는 이걸로 발라도 되지않나. 덤으로 collection2의 기능도 확장됩니다.
> peerlibrary:fs : NPM 패키지를 안쓰고 파일 읽고 쓰기만 필요할때 가볍게~
> yogiben:admin : collection 전체를 조회/추가/수정/삭제하는 간단 어드민. autoform과 collection2에 대한 이해가 있으면 좋음. 생각보다 커스터마이징 자유로움
> pinglamb:bootstrap3 : 말이 필요있나요. 부트스트랩. 이거 뭐가 공식임?
> francocatena:status : 사용자 접속 상태 얻어오기. 약간 문제가 있는 듯 싶지만 대안이?
> jparker:crypto-md5 : 암호화는 중요하죠? gravatar 같은 걸 쓸때 필요.
> 일단 생각나는대로 fastosphere.meteor.com 뒤져가면서 썼는데 다른 분들은 어떤거 좋아하시나요?

> easy-search! 일래스틱서치 쓰는 SI용사들에겐 정말 좋겠네요!
> manuelschoebel:ms-seo 이거 추가요
> 저는 추가로 fast-render(렌더링 속도 상승)와 slingshot(클라이언트에서 클라우드 스토리지에 바로 올리기)
> 저는 collection2, autoform, fastclick, easy-search 정도 쓰고 있는거 같네요 ㅎㅎ

 
> 밑에 이재호님의 릴레이를 받아 사용 패키지 공개하고 갑니다. (중복패키지 제외)
> - fast click : 아 중복이긴한데 첨언이 있어서 씀니다. 이거 클릭 속도는 좀 빨라지나 특정 모바일 폰에서 오동작을 함니다. (특정 폰에 갤럭시 s4도 포함이라는 대목이 아주 잦같은...) 결론은 모바일에서 300밀의 이벤트 딜레이는 괜히 주던가 아니더라. (결국에 나중엔 없어질거라 봅니다만) 특히 애니메이션 액션을 시작하거나 하는 부분에서 이상한 짓을 좀하니까 사용하실땐 좀 유의하시면 좋겟십니다.
> - mrt:cheerio : 이재호님의 춫천으로 사용한 패키진데 베리베리굳- html을 파싱해야 할 경우에 좋은데요 css selector 로 파싱이 가능함니다. regex에 능통한 분들이라면... 그냥 하던대로 하세요 ㅠㅜ
> - peppelg:bootstrap-3-modal : 모달. 특히 붓스트랩 모달. 붓스트랩 변종들이 겁나 돌아당기는 마당에 모달은 오동작을 많이 합니다. 사용성도 거지같습니다.
> 이 패키지 쓰면 모달을 일반 template과 같이 사용할 수 있습니다. 
> header body footer 로 구성된 부분을 그냥 잘 구성해서 쓰면 댑니다.
> $('‪#‎modal‬').modal 'show' 와 같이 간편하게 조작도 가능하구요.
> 이건 궁여지책으로 잘 쓰고 잇긴한데, 뭔가 더 좋은게 잇을것 같.
> mizzao:user-status : 간단하게 로그인 된 유저의 last-login ip나 시간등을 체크하기에 좋십니다. 개인적으로는 결국 더 자세한 user-agent 정보가 필요해서 구현해서 씀니다만, 예전에 사용한 내역이 잇어서 아직 박혀 잇네요.
> percolate:velocityjs : 붓스트랩 애니메이션이 모바일에서 겁나 쳐 느림니다. 물론 최신폰에만 서비스 할거라면 돈 케어. 하지만 렌더링이 좀 있는 페이지들이라면 애니메이션 고려를 해야함니다. 이재호님의 어드바이스 + 우리수습사원의 삽질로 '좋으다'라는 것이 판명되엇습니다.
> brentjanderson:buzz.js : 혹자들은 이딴거 왜 쓰냐. 라고 하던데. 뭐 그냥 씀니다 ㅋㅋ 간단한 알람음을 울리기 위해서 사용함니다. loop stop play 등이 간편하게 조작되서 씀니다. 그냥 씀니다.





!!userId is the same as Boolean(userId)



## Deny, Allow
deny에 true인자가 들어오면 실행이 안되고.
allow에 false인자가 들어오면 실행이 안된다.



## 메서드 호출 대 클라이언트에서의 데이터 가공
메서드 호출은 다음의 몇 가지 시나리오에서 더 적합하다:

반응성과 동기화가 전파되는 것을 기다리기 보다는 콜백을 통해 값을 리턴하거나 알아야 할 필요가 있는 경우.
대형의 컬렉션을 전송하기에는 너무 부담되는 무거운 데이터베이스 함수의 경우.
데이터를 요약하거나 모으기 위한 경우(예, 수량, 평균, 합계 등).

우리는 필요한 만큼 allow 콜백을 정의할 수 있다. 단지 변경이 발생했을 때 그 콜백들 중에서 최소한 하나만 true를 리턴하면 된다.
유사한 방식으로 하나 이상의 deny 콜백을 정의할 수 있다. 만약 이들 가운데 어느 것이라도 true를 리턴하면, 변경은 취소되고 403이 리턴된다. 이 로직은 성공적인 insert를 위해서는 하나 또는 그 이상의 allow와 모든 deny 콜백이 실행된다는 것을 의미한다.



## !!연산자
!!foo applies the unary not operator twice and is used to cast to boolean type similar to the use of unary plus +foo to cast to number and concatenating an empty string ''+foo to cast to string.

Instead of these hacks, you can also use the constructor functions corresponding to the primitive types (without using new) to explicitly cast values, ie

Boolean(foo) === !!foo
Number(foo)  === +foo
String(foo)  === ''+foo

It's just the logical NOT operator, twice - it's used to convert something to boolean, e.g.:
true === !!10
false === !!0


## 서버와 클라이언트에서의 db 접근
- 서버

```
meteor mongo
> db.posts.insert({title: "A new post"});
> db.posts.find();
{ "_id": ObjectId(".."), "title" : "A new post"};
```

- 클라이언트
```
❯ Posts.findOne();
{title: "A new post", _id: LocalCollection._ObjectID};
```

클라이언트에서 컬렉션은 좀 더 흥미롭다. 클라이언트에서 Posts = new Meteor.Collection('posts'); 라고 선언하는 것은, 실제 Mongo 컬렉션의 로컬, 인-브라우저 캐시를 생성하는 것이다. 우리가 클라이언트 쪽의 컬렉션을 “캐시"라고 말하는 것은, 데이터의 부분 집합을 가지며, 데이터에 빠르게 접근할 수 있다는 것을 의미한다.

이 부분을 이해하는 것이 이것이 미티어가 작동하는 방식의 기본이라는 점에서 중요하다. 일반적으로, 클라이언트 쪽 컬렉션은 Mongo 컬렉션에 저장된 전체 도큐먼트의 부분집합이다.(결국, 우리는 전체 데이터베이스를 클라이언트로 보내는 것을 원하지 않는다).

두 번째, 이 도큐먼트들은 브라우저 메모리에 저장되는 데, 이는 여기에 접근하는 것이 기본적으로 순간적이라는 것을 의미한다. 그러므로 클라이언트에서 Posts.find()를 호출할 때, 데이터를 가져오려고 서버나 데이터베이스에 느리게 갔다오는 일은 없다. 데이터는 이미 로드되어 있기 때문이다.




In[ ]:



