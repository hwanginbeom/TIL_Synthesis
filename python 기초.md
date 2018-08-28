# python 기초 

## 크롤링

  크롤링은 코드를 통해 웹사이트의 정보를 수집하는 것을 뜻 한다.

#### 필요한 라이브러리

1. `requests` : 요청을 python 코드를 통해 보내주는 라이브러리
2. ` bs4 `: 요청받은 결과(html,xml)를 쉽게 탐색 할 수 있도록 도와주는 라이브러리

 rkskekfk 

`dkdfkf` erkw

#### 예제코드

``` python
import requests
from bs4 import BeautifulSoup
res = requests.get('https://finance.naver.com/sise/')
soup = BeautifulSoup(res.content, 'html.parser')
kospi = soup.select('#KOSPI_now')
print(kospi)

```

#### 

```python
import requests
from bs4 import BeautifulSoup

url='https://finance.naver.com/sise/'
#요청을 보낼 주소를 가져온다
res=requests.get(url)
#2.그 주소로요청을 보낸다. 
print(res)
#res.status_code=> 200 이면 값은 성공적으로 가져 왔다는 것
#3.원하는 값을 찾는다. 
#print(res.content)
#페이지 소스보기 
print(res.url)
result=BeautifulSoup(res.content , 'html.parser')
a = result.select_one('#KOSPI_now')
b = result.select('#KOSPI_now')
print(a)
print(b)
c = result.select_one('#KOSPI_now')# 하나는 <class 'bs4.element.Tag'> 이 형태로 온다 
d = result.select('#KOSPI_now')[0]# 이게 하나는 list형식이고 
print(type(c))
print(c.text)
print(d.text)
#BeautifulSoup 를 통해 이 소스를 조절한다.

#KOSPI_now
#content

```



### 추가설명

``` python 
# 1. BeautifulSoup type 으로 변형 하여 찾기 편하게 활용
# 1)request 보낸 이후 
type(res)
# => <class byte>
# 2) BeautifulSoup 으로 바꾼 이후
type(result)
#=> <class 'bs4.BeautifulSoup'>
# 3) 특정 tag를 select 한 이후
type(kospi)
#=> <class 'bs4.element.tag'>

```





### Selector(셀렉터)

1. 요소 선택자 : HTML 문서에서 tag를 선택하는것.
   ` <span>코스피 지수</span>: `  =>    ` span `

2. 클래스 선택자 : HTML 문서에서 tag에 정의된 class를 통해 선택하는 것.
   ` <span class="blue"> 코스피 지수 </span> ` => ` .blue `

3. 아이디 선택자 : HTML 문서에서 tag 에 정의된 id  를 통해 선택하는 것.  **문서에서 단한개**

   ` <span id ="KOSPI_now"> 2456.24</span>` => ` #KOSPI_now `
