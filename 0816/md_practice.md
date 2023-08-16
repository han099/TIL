## Django

#### 8월 10일 학습내용
1. Django 프로젝트 구조를 살펴보고 앱을 추가해서 구현할 수 있다.
2. 단계적인 앱의 구성을 습득할 수 있다.
3. Django의 원리를 이용해서 MVT 대한 설계를 구현할 수 있다.
   (모델 인스턴스 -> 모델 폼 양식 -> 모델필드로 렌더링)
---

#### mysite02 순서

1. blog 앱 생성
```python
python manage.py startapp blog
```
2. mysite02.settings 파일에 ['blog'] 추가
```python
INSTALLED_APPS = ['blog']
```
3. blog.view.py 함수생성 (request, response)
```python
from django.http import HttpResponse

def home(request):
    posts = Post.objects.all()  #selectall _QuerySet
    context = {'posts': posts}
    return render(request, 'blog/home.html', context)
```

4. url패턴을 매핑선언
```python
blog.urls.py    #mysite02.urls.py를 복사
```
5. mysite02.urls.py에 blog.urls.py를 연결
```python
urlpatterns = [
    path('', include('blog.urls')),
]
```
**추가작업 ->  3,4만 반복**	

--- 

#### MVT
- Model DataBase 연동(orm)
- View  Data 구성 (business logic)
- Template  Data 표현(presentation layer)
###### controller : django framework 자체

#### M << 모델정의 -> 마이그레이션 >>

- 'django-admin'의 db관련 명령어
- makemigrations -> db 새로 생성
- migrate -> 생성된 db에 테이블 수정
- sqlflush
- sqlmigrate  -> sql 미리보기 : 쿼리 출력
- sqlsequencereset
- showmigrations

> 모델을 변경하고(table) 마이그레이션을 생성(db)하고 변경사항을 데이터베이스에 적용하는 프로세스
1. 새 모델을 정의하거나 기존 모델을 변경  ( 새로운 테이블을 생성하거나 수정할 때 )
2. 명령을 실행하여 새 마이그레이션을 수행 makemigrations.	( 새로운 데이터 베이스 생성 )
3. 명령을 실행하여 모델의 변경사항을 데이터베이스에 적용 migrate. ( 테이블 생성, 수정 -> 기존DB )

ex) 모델정의 
```python
blog.models.py # django.db.models.Model의 하위클래스 및 필드가 명시되어야 한다.
```
  - 상속해서 클래스를 생성 / DEFAULT_AUTO_FIELD = 'django.db.models.BigAutoField'
  - __str__ 문자열 표현 재정의 메소드
  - class Meta 구성

ex) 내장모델과 함께 사용한다. 참조키를 생성했다.
```python
from django.contrib.auth.models import User 
```

<실습 1> 새 마이그레이션 생성 ( blog\migrations\0001.py 생성)
```python
python manage.py makemigrations
```
<실습 2> 내용확인(sql구문 미리보기)
```python
python manage.py sqlmigrate blog 0001
```
<실습 3> 변경사항을 데이터베이스에 적용
```python
python manage.py migrate
```
<실습 4> 프로젝트에서 해당 마이그레이션의 상태를 나열해보자
```python
python manage.py showmigrations
```
*관련오류들*
> "no changes detected"
- 모델변경 X (세션, 브라우저) 
    - 앱이 지정되지 않았다. 
    - 해결방법 : python manage.py makemigrations 앱이름
- INSTALLED_APPS에 등록된 앱이 인식하지 못 할 경우 
- 마이그레이션 파일이 이미 있을 때 
- 모델 정의 오류
- 수동 삭제할 경우
