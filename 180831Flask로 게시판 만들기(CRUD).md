# Flask로 게시판 만들기(CRUD)



## 환경 설정

1. 설치 

   ``` 
   #ubuntu pstgresql 설치하기 
   $ sudo pip3 install psycopg2 psycopg2-binary Flask-SQLAlchemy Flask-Migrate
   
   #python(flask)에서 사용 할 수 있또록 도아주는 애들
   $ sudo pip3 install psycopg2 psycopg2-binary 
   
   #flask에서 import 해서 쓸 것들 
   $ sudo Flask-SQLAlchemy Flask-Migrate
   ```



2.DB 설정

``` 
$ psql
ubuntu# CREATE DATABASE app WITH template=template0 encoding='UTF8'
              (데이터 베이스 네임) 
ubuntu# \q (나가기) 들어가는 거 \d
```



3.서버 리스타트

```
$ sudo /etc/init.d/postgresql restart
```







## 모델설정

``` python
# /models.py
from flask_alchemy import SQLAlchemy

db = SQLAlchemy()
class post(db.model):
    #데이터베이스 테이블 설정 (테이블 명 , 컬럼)
    __tablename__= 'posts' #(테이블 이름은 보통 클래스 이름의 복수형으로 만든다.)
    id = db.Column(db.Integer,primary_key=True)
    title=db.Column(db.string,nullable=False)
    content = db.Column(db.text)
    created_at=db.Column(db.DateTime)
    
    #객체 생성자
    def __init__(self,title,content):
        self.title=title
        self.content=content
        self.created_at=datetime.datetime.now()
        
#/app.py
from flask import Flask
#flask ORM
form flask_sqlalchemy import SQLAlchemy
#마이그레이션 관리
from flask_migrate import Migrate

#모델 설정 파일 import
from models import *

app = Flask(__name__)
#DB설정과 관련된 코드
app.config["SQLACHEMY_DATABASE_URI"] = 'postgresql:///app'
app.config["SQLALCHEMY_TRACK_MODIFICATION"]=Fasle
db.init_app(app)

@app.route('/')
def index():
    return "hello world"
```





## 마이그레이션

``` python
from flask_migrate import Migrate
migrate = Migrate(app,db)
```

1. ` flask db initalize `

   ``` 
   $ flask db init
   ```

   * migrations/
     * versions/
       * 12312dsafs.py

2. models.py 파일의 현재상태를 반영

   ``` 
   $ flask db migrate
   ```

3. DB에 반영

```
$ flask db upgrad
```

4. 실제로 DB에서 확인하기

   ```
   $psql app
   ubuntu# \d posts
   ```


## CRUD 

1.Create

```html
<!-- index.html -->
<a href="/posts/new">글 쓰러가기</a>
```



``` python
#app.py
@app.route("/posts/new")
def new():
    return render_template("new.html")
```



```html
<!-- new.html-->
<form action="/posts" method ="POST">
    <input type="text" name ="title">
    <textarea name =""></textarea>
    <input type="submit">
</form>
```



```python
@app.route("/posts", methods =["POST"])
def create():
    title = request.form.get('title')
    content = request.form.get('content')
    post = Post(title=title , content= content)
    db.session.add(post)
    db.session.commit()
    return render_template("create.html", post=post)
<!--create.html-->
{{post.id}}
{{post.title}}
{{post.content}}
{{post.created_at}}
```



` ORM `  =객체 조작만으로 db를 관리 할 수있는것 (객체와 관계와의 설정)



## 1:N database Association(Relation)

1.모델설정

```py
def Post(db.Model):
	#...
	comments = db.relationship('Comment',backref='post')
	#..

def Comment(db.Model):
	#...
	post_id =db.Column(db.Integer,db.Foreignkey('posts.id'), nullable=False)
```

2.댓글 저장하기

``` python
#app.py
def comment(post_id):
    content = request.form.get('content')
	comment = Comment("내용입니다.")
	Post.query.get(post_id)
    post.comments.append(comment)
    db.session.add(comment)
    db.session.commit()
    return render_template()
```



3.활용 예시

``` 
$ flask shell
>>from app import *
>>comment = Comment.query.first()
>>comment.post
>>post=Post.query.get(2)
>>post.comments

```





