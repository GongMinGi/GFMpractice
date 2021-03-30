# 마크다운 확장문법(GFM)
## 1. 표
- 표는 행과 열이 있는 데이터 배열로, 단일 헤더 행과 데이터에서 해더를 분리하는 딜리미터 행, 그리고 0개 이상의 데이터 행으로 구성됩니다.<br>

        | foo | bar |<br>
        | --- | --- |<br>
        | baz | bim |<br>
  위와 같은 표는 이렇게 출력됩니다.
  
    | foo | bar |
    | --- | --- |
    | baz | bim |
- 행의 길이는 같을 필요가 없으나 같으면 더욱 보기 좋습니다. 또한 앞, 뒤에 오는 파이프는 넣지 않아도 무관합니다.

        | abc | defghi|
        :-: | ----------:
        bar | baz
        
- 표는 처음 빈 줄을 만나거나 블록수준의 구문을 만났을 때 끊깁니다. 

        ex1)
        | abc | def |
        | --- | --- |
        | bar | baz |
        >bar
        
        ex2)
        | abc | def |
        | --- | --- |
        | bar | baz |
        bar
        
        bar
        
- 헤더 행의 개수는 반드시 딜리미터행의 개수와 맞아야 한다. 그렇지 않으면 표가 만들어지지 않는다.

        | abc | def |
        | --- |
        | bar |
        
- 표의 열의 개수는 각행마다 다를 수도 있다. 만약 열의 개수가 헤더 행의 개수보다 적다면 그만큼 빈 셀이 만들어지지만, 헤더 행의 개수보다 길다면 초과되는 열은 무시된다.

        | abc | def |
        | --- | --- |
        | bar |
        | bar | baz | boo |
        이 경우 3행 2열은 빈칸이 되고, 3행 3열은 사라진다.
        
- 만약 데이터 행이 없는 경우에는 HTML에서 <tbody>가 만들어지지 않습니다.

        | abc | def |
        | --- | --- |
        
## 2. 작업목록
- 작업목록을 이용하면 목록과 함께 그 목록에 대한 체크박스를 만들 수 있다. 작업목록은 다음과 같이 표기한다.
        
        - [ ] foo
        - [x] bar
  이는 이와 같이 나타난다
  - [ ] foo
  - [x] bar
  
  대괄호 안에 공백, x, X 세가지 문자중 하나는 들어가야하며, x,X를 적을경우 체크된것으로 취급한다.
  
      - [x] foo
        - [ ] bar
        - [x] baz
      - [ ] bim
   
   이과 같이 중첩하여 적는 것도 가능하며 결과는 아래와 같다.
   
   - [x] foo
      - [ ] bar
      - [x] baz
   - [ ] bim
  
 ## 3. 취소선
 - 두개의 틸데(~)로 둘러쌓인 텍스트는 취소선이 그이게 된다.
    
        ~~Hi~~ Hello, world!
    이 경우, 다음과 같이 나타난다.
    
    ~~Hi~~ Hello, world!
    
    일반 강조 기호와 마찬가지로 새로운 단락을 만들면 취소선은 끊긴다
    
        This ~~ has a
        
        new paragraph~~.
        
    This ~~ has a
        
    new paragraph~~.  
    
    위와 같이 표기된다.
    
## 4. 오토링크
- 자동링크는 링크를 설정하기 위해 <, > 등을 사용하지 않아도 자동으로 링크를 만들어줍니다. 이러한 자동링크는 줄의 시작점, 공백문자, 혹은 *, _ , ~ , ( 뒤에만 올수 있습니다.

      www.commonmark.org
  이런 경우 http가 쓰여있지 않아도 자동으로 삽입된다.
  www.commonmark.org
  
- 유효한 링크 뒤에는 공백문자, < 가 아닌 다른 문자들은 올 수 없습니다.

        Visit www.commonmark.org/help for more information
   
  Visit www.commonmark.org/help for more information 여기서 help 뒤에 공백을 지우면 for 까지 링크로 인식해 잘못된 곳으로 연결된다.
  
- 링크의 뒤에오는 특수문자들 (?, !, . , , ,:, *, _ , ~) 등은 자동링크의 일부로 간주되지 않지만, 링크 내부에 포함될 수 도 있습니다.

        Visit www.commonmark.org.

        Visit www.commonmark.org/a.b
        이 두 링크는 다른 주소를 가리킵니다.
  Visit www.commonmark.org.

  Visit www.commonmark.org/a.b
  
- 자동링크가 )로 끝날 때, 우리는 자동링크 전체를 검사해서 닫는 괄호가 여는 괄호보다 많을 경우 남는 괄호를 링크에 포함시키지 않습니다.

    www.google.com/search?q=Markup+(business)

    www.google.com/search?q=Markup+(business)))

    (www.google.com/search?q=Markup+(business))

    (www.google.com/search?q=Markup+(business)
    
  3,4번의 경우 www 부터 링크로 인식하기 때문에 앞의 괄호를 인식하지 않는것이다.
  
  또한 이 규칙은 링크가 괄호로 끝날 때만 적용되기 때문에 링크 내부의 괄호에 대해서는 아무런 규칙도 적용되지 않습니다.
  
  www.google.com/search?q=(business))+ok
  
- 만약 링크가 세미콜론(;)으로 끝나고, 링크내부 & 뒤에 영어, 숫자가 1개이상존재한다면, 그 영문자와 숫자들은 링크에서 제외됩니다.

  www.google.com/search?q=commonmark&hl=en

  www.google.com/search?q=commonmark&hl;
  
- < 기호는 입력되는 즉시 링크를 끝냅니다.

  www.commonmark.org/he<lp
  
- 메일 자동링크의 경우 메일 수신인이 자동으로 생성됩니다.
  
  foo@bar.baz
  
- 플러스(+) 는 @앞에는 올 수 잇지만, 뒤에는 올 수 없습니다.
  
      hello@mail+xyz.example isn't valid, but 
      hello+xyz@mail.example is.

- . , -, _ 은 @의 양쪽 모두 올 수 있지만,  . 이외에는 메일주소의 끝에 올 수 없습니다.

  a.b-c_d@a.b

  a.b-c_d@a.b.

  a.b-c_d@a.b-

  a.b-c_d@a.b_
  
- url 자동링크는 http: // 혹은 https:// 이후에 공백이나 <기호가 없는 유효한 주소가 입력되어야 합니다.

  http://commonmark.org

  (Visit https://encrypted.google.com/search?q=Markup+(business))
  
## 5. 허용되지 않는 HTML
- GFM 에서 다음의 태그들은 필터링 처리됩니다.
- <title>
- <textarea>
- <style>
- <xmp>
- <iframe>
- <noembed>
- <noframes>
- <script>
- <plaintext>

         <strong> <title> <style> <em>
  
         <blockquote>
          <xmp> is disallowed. <XMP> is also disallowed.
         </blockquote>
         
위와 같이 쓸경우 아래처럼 출력됩니다.

  <strong> <title> <style> <em>
  
  blockquote>
    <xmp> is disallowed. <XMP> is also disallowed.
  </blockquote>
