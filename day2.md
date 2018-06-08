# Day 2

- *서버 접속 : ruby 실행시킬 루비파일명 -o $IP -p $PORT*
- *각 인스턴스 변수는 오브젝트의 소유 기간 동안 메모리에 상주한다.* 

### 새로운 폴더에 sinatra 프로젝트 넣기

* app.rb 파일 생성 후 views 폴더 생성
* sinatra 와 sinatra-reloader 잼을 설치

*test_app/app.rb*

```ruby
require 'sinatra'
require 'sinatra/reloader'

get '/' do
	erb :app
end
```

### 페이지간 이동

* <a> </a> : anchor 태그 
* <form></form> : 다음 페이지로 넘겨야할 데이터가 있을 때.

### GET 방식과 POST 방식(method)

method:  form데이터를 어떻게 보낼 것인지

- GET : URL에 데이터 추가

~~~ruby
get '/form' do
    erb :form
end
~~~



- POST : 트랜잭션이 일어남. 사이즈 제한이 없음. http request body안에 form데이터 추가. 데이터는 URL에 보여지지 않는다.

  ~~~ruby
  post '/login' do
      if id.eql?(params[:id])
         # 비밀번호를 체크하는 로직
         if pw.eql?(params[:password])
             erb :complete
         else
             @msg = "비밀번호가 틀립니다."
             erb :error
         end
      else
         # ID가 존재하지 않습니다
         @msg = "ID가 존재하지 않습니다."
         erb :error
      end
  end
  ~~~

  

### 로그인

* ID / PASSWORD 입력창

* ID / PASSWORD 검사

  *redirection*

* 완료페이지

### 게시판 글쓰기

* 글을 쓰는 form
* 작성
* 내가 쓴 글 페이지

*post method일 경우 반드시 , **redirect***

post방식으로는 무조건 두 번, 처음 데이터를 로직으로 전달. view를 보여주지 않고 다른 페이지로 다시 이동시킴 . 그 후에 view에 보여준다.

~~~ruby
post '/login' do
    if id.eql?(params[:id])
       # 비밀번호를 체크하는 로직
       if pw.eql?(params[:password])
           redirect '/complete'
       else
           @msg = "비밀번호가 틀립니다."
           redirect '/error'
       end
    else
       # ID가 존재하지 않습니다
       @msg = "ID가 존재하지 않습니다."
       redirect '/error'
    end
end
~~~

> @msg : 인스턴스 변수이므로 사이클이 끝나면 초기화. 동작할 수 없음.

* 기본적으로 post요청에 대한 로직은 직접 뷰를 렌더링하는 것이 아니라 다른 페이지로 redirect시킨다.
* 새로고침을 통한 접속불가등의 현상을 막기위한 방편이다.
* 이후 게시판 글을 만드는 요청에 대한 로직을 구성할 때에도 동일한 방식으로 구성한다.

~~~ruby
User.find_id(params[:id]).authenticate(params[:password])
else
 @msg = "아이디가 없거나 비밀번호가 일치하지 않습니다."
~~~

### http 상태 코드

* 1xx (조건부 응답)
* 2xx (성공)
* 3xx(리다이렉션 완료)
* 4xx(요청 오류)
* 5xx(서버 오류)

#### 검색창 만들기

#### '/search'

- 검색어 입력창 2개(구글 검색, 네이버 검색)

#### 결과

네이버(구글) 검색 결과로 redirection

### string interpolation

~~~~ruby
name = "Ada"
puts "Hello, " + name + "!"
~~~~

~~~ruby
name = "Ada"
puts "Hello, #{name}!"
~~~

### OP.GG 만들기

1. OP.GG 에서 검색한 결과

2. 승/패 수만 보여주기

3. select태그를 이용해서 두가지 방법중 선택하기

4. 조건 form태그는 1개 action 1개만

   <erb(embedded ruby)>

* 눈에 보이는 것(숫자,텍스트,메시지)
* 눈에 안 보이는 것(분기문,반복문)

