

  #  [Flask](http://flask.pocoo.org/)기초



1. 설치

   ```
   $ sudo pip3 install flask
   ```


2. 기본코드

   ``` python
   #/app.rb(파일명과 디렉토리명 명시)
   #-*- coding:utf-8 -*-
   from flask import Flask
   app = Flask(__name__)
   
   @app.route("/")
   def hello():
       return "Hello World!"
   
   ```

3.서버 실행 명령어

```
$ flask run --host 0.0.0.0 --port 8080
```

* c9 서버에서는 ` flask run`  명령어에 ` host` 와 ` port` 를 직접 설정해줘야 한다.

* 로컬에서 구동시에는 `flask run` 많  해도 되며 , 접속 url은 http://localhost:5000 이기본 이다.

* ` flask run`  명령어를 실행 할 때, 파일명이 app.rb가 아니면 직접 설정해줘야한다.

  예) 만약에 위의 코드가 ` applicatin.rb` 로 설정해 두었다면 실행코드는 다음과 같다.

  ```
  $ FLASK_APP = application.rb flask run 혹은 $export 
  ```

  ` $ FLASK_APP = application.rb flask run`  혹은 $export FLASK_APP=application.rb로 환경변수를 설정하고 `$ flask run` 을 실행시킨다

4. `render_template`  모듈 사용하기
   1.  `render template` 불러오기

```python

#/app.rb(파일명과 디렉토리명 명시)
#-*- coding:utf-8 -*-
from flask import Flask
app = Flask(__name__)

@app.route("/")
def hello():
    return "Hello World!"

@app.route("/')
def hello():
           return reder_template("index.html")
```

2) .html 파일 만들기

```html
<!-- /templates/index.html -->
<!Doctype html>
<html>
    <head>
        <title>프로젝트</title>
    </head>
    <body>
        <h1>
            안녕!
        </h1>
    </body>
</html>
```

3)python 변수 활용하기

```python
def lunch():
    lunch_box=["멀캠20층","김밥카페"]
    lunch=random.choice(lunch_box)
    return render_template("lunch.html", lunch=lunch)
```

```html
<!-- /templates/lunch.html-->
점심은 {{lunch}}  입니다.
<hr>
{% for menu in lunch_box %}
<p>
    {{menu}}
</p>
{% endfor %}

```



5. `layout` 활용하기 - `jinja2`  템플릿 활용

```html
<!--/templates/layout.html-->

<!Doctype html>
<html>
    <head>
        <title>{% block title %}{% endblock %}</title>
    </head>
    <body>
        <h1>
            {% block body %}
            {% endblock %}
        </h1>
    </body>
</html>

```

```html
<!--/templates/index.html-->
{% extends "layout.html" %}
{% block title %} 홈{% endblock %}
 {% block body %}
	<h1>
        Hello,world!	
	</h1>
 {% endblock %}
```



6. `variable routing` 

   ```python
   @app.route('/hello/<string:name>')
   def hello(name):
       return render_template("index.html", name=name)
   
   @app.route('/cube/<int:num>')
   def cube(num):
       return render_template("cube.html", cube=num*num)
   ```


