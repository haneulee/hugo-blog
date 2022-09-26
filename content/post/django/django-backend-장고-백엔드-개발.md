---
title: "Django Backend 장고 백엔드 개발 🤠"
date: 2022-09-26T20:42:29+02:00
categories:
  - development
  - django
  - backend
tags:
  - development
  - front-end
  - Django Backend 장고 백엔드 개발
  - django
  - backend
  - python
  - web develop
  - 장고
  - 백엔드
  - 파이썬
  - MVT
  - model-view-template
  - poetry
  - virtual environments
keywords:
  - development
  - front-end
cover: ""
thumbnailImagePosition: left
thumbnailImage: "https://warehouse-camo.ingress.cmh1.psfhosted.org/7238e9278feca226d99ec1e6109d4ba294f5ece0/68747470733a2f2f7261772e67697468756275736572636f6e74656e742e636f6d2f4e656b6d6f2f636f6f6b69656375747465722d646a616e676f2d6261636b656e642f6d61737465722f696d616765732f6c6f676f2e706e67"
# coverImage: //https://cdn.jsdelivr.net/gh/haneulee/haneulee.github.io/img/post/hugo/github-site.png
metaAlignment: center
coverMeta: out
draft: false
---

<!--toc-->

# Django Backend 장고 백엔드 개발 🤠

![](https://warehouse-camo.ingress.cmh1.psfhosted.org/7238e9278feca226d99ec1e6109d4ba294f5ece0/68747470733a2f2f7261772e67697468756275736572636f6e74656e742e636f6d2f4e656b6d6f2f636f6f6b69656375747465722d646a616e676f2d6261636b656e642f6d61737465722f696d616765732f6c6f676f2e706e67)

<!--adsense-->

## Django 장고 란?

{{< alert info >}}
Django is a high-level Python web framework that encourages rapid development and clean, pragmatic design. Built by experienced developers, it takes care of much of the hassle of web development, so you can focus on writing your app without needing to reinvent the wheel. It’s free and open source.

Djano란 보안이 우수하고 유지보수가 편리한 웹사이트를 신속하게 개발하는 하도록 도움을 주는 파이썬 웹 프레임워크
{{< /alert >}}

장고는 간단하게 백엔드 개발을 지원하는 프레임워크이며, 사용자 인증/콘텐츠 관리/어드민 등을 모두 지원한다.

![](https://miro.medium.com/max/1400/1*XohhamnRotq53fQaY5HQfA.png)

- MVT 패턴 (Model View Template)
- 구성요소들 간의 긴밀한 통합
- 객체관계 매핑(Object-Realtional Mapper, ORM)
- 간단한 URL 주소 설계
- 자동으로 구성되는 관리자 화면
- 풍부한 개발 환경
- 다국어 지원
- 간결하고 유지가 용이
- 빠른 개발 시간

## Django를 사용하는 사이트

- Disqus
- Mozila
- Open stack
- instagram
- pinterest
- national geographic

## Django가 지원하는 기능

1. `템플릿` : HTML 템플릿은 서버에서 처리할 사용자 데이터를 수집하는 데 사용됩니다. 장고는 양식 작성, 유효성 검사 및 처리를 단순화합니다.
   사용자 인증 및 권한 : 장고에는 보안을 염두에 두고 구축된 강력한 사용자 인증 및 권한 시스템이 포함되어 있습니다.
2. `캐싱` : 컨텐츠를 동적으로 작성하는 것은 정적 컨텐츠를 제공하는 것 보다 많은 연산을 필요로 하기 때문에 느립니다. 장고는 유연한 캐싱을 제공하여 렌더링된 페이지 전체 또는 일부를 저장하여 필요할 때를 제외하고 다시 렌더링하지 않도록 할 수 있습니다.
3. `관리 사이트` : 기본 스켈레톤을 사용하여 앱을 만들 때 장고 관리 사이트가 기본적으로 포함됩니다. 사이트 관리자가 사이트의 모든 데이터 모델을 작성, 편집 및 볼 수있는 관리 페이지를 쉽게 제공할 수 있습니다.
4. `데이터 직렬화` : 장고를 사용하면 데이터를 XML 또는 JSON으로 직렬화하고 제공할 수 있습니다. 이 기능은 웹 서비스 (다른 응용 프로그램이나 사이트에서 사용하기 위해 순수하게 데이터를 제공하고 자체를 표시하지 않는 웹 사이트)를 만들거나 클라이언트 쪽 코드가 모든 데이터 렌더링을 처리하는 웹 사이트를 만들 때 유용할 수 있습니다.

<!--adsense-->

## Django 설치

### 작업환경

- 파이썬
- poetry (가상환경)
- poetry 가상환경 내에 장고 설치

#### poetry & python 설치

```
curl -sSL https://raw.githubusercontent.com/python-poetry/poetry/master/get-poetry.py | python3 -
```

#### django 설치

```
poetry init //새로운 환경설정 초기화
poetry shell //해당 개발 환경 접속
poetry add django // 장고 설치
django-admin startproject config . // 장고 프로젝트 생성

```

## 장고 App

### 장고 실행 명령어

```
poetry shell // 가상환경 접속
python manage.py makemigrations // DB에 수정한 모델 migration 생성
python manage.py migrate // DB에 실제 migrate 하기
python manage.py runserver //로컬 서버 실행
python manage.py startapp rooms // 장고 app 생성
python manage.py createsuperuser //어드민 생성
```

### models.py

장고가 models.py의 파이썬 코드를 SQL 코드로 변환

모델은 응용프로그램의 데이터 구조를 정의하고 데이터베이스의 기록을 관리(추가, 수정, 삭제)하고 쿼리하는 방법을 제공하는 파이썬 객체입니다.

```
from django.db import models

class Team(models.Model):
    team_name = models.CharField(max_length=40)

    TEAM_LEVELS = (
        ('U09', 'Under 09s'),
        ('U10', 'Under 10s'),
        ('U11', 'Under 11s'),
        ...  #list other team levels
    )
    team_level = models.CharField(max_length=3, choices=TEAM_LEVELS, default='U11')
```

### admin.py

커스텀 데이터에 대한 관리 패널을 자동으로 생성해줌

- `list_display` : admin 페이지에서 보여질 list view들을 설정
- `list_filter` : admin 페이지에서 필터링 추가
- `fieldsets` : 세부 양식 안의 연관된 모델 정보를 그룹화하기 위해 "sections"를 추가할 수 있습니다.

```
@admin.register(BookInstance)
class BookInstanceAdmin(admin.ModelAdmin):
    list_display = ('title', 'author', 'display_genre')
    list_filter = ('status', 'due_back')

    fieldsets = (
        (None, {
            'fields': ('book', 'imprint', 'id')
        }),
        ('Availability', {
            'fields': ('status', 'due_back')
        }),
    )

```

### urls.py

단일 함수를 통해 모든 URL 요청을 처리하는 것이 가능하지만, 분리된 뷰 함수를 작성하는 것이 각각의 리소스를 유지보수하기 훨씬 쉽습니다. URL mapper는 요청 URL을 기준으로 HTTP 요청을 적절한 뷰(view)로 보내주기 위해 사용됩니다. 또한 URL mapper는 URL에 나타나는 특정한 문자열이나 숫자의 패턴을 일치시켜 데이터로서 뷰 함수에 전달할 수 있습니다.  
지정된 URL 패턴과 일치하는 HTTP 요청이 수신된다면 관련된 view 함수가 요청을 전달합니다.

```
urlpatterns = [
    path('admin/', admin.site.urls),
    path('book/<int:id>/', views.book_detail, name='book_detail'),
    path('catalog/', include('catalog.urls')),
    re_path(r'^([0-9]+)/$', views.best),
]
```

### views.py

뷰는 HTTP 요청을 수신하고 HTTP 응답을 반환하는 요청 처리 함수입니다. 뷰는 Model을 통해 요청을 충족시키는데 필요한 데이터에 접근합니다. 그리고 탬플릿에게 응답의 서식 설정을 맡깁니다.

```
from django.shortcuts import render
from .models import Team

def index(request):
    list_teams = Team.objects.filter(team_level__exact="U09")
    context = {'youngest_teams': list_teams}
    return render(request, '/best/index.html', context)

```

### templates

탬플릿은 파일의 구조나 레이아웃을 정의하고(예: HTML 페이지), 실제 내용을 보여주는 데 사용되는 플레이스홀더를 가진 텍스트 파일입니다. 뷰는 HTML 탬플릿을 이용하여 동적으로 HTML 페이지를 만들고 모델에서 가져온 데이터로 채웁니다. 탬플릿으로 모든 파일의 구조를 정의할 수 있습니다.탬플릿이 꼭 HTML 타입일 필요는 없습니다!

```
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>Home page</title>
</head>
<body>
  {% if youngest_teams %}
    <ul>
      {% for team in youngest_teams %}
        <li>{{ team.team_name }}</li>
      {% endfor %}
    </ul>
  {% else %}
    <p>No teams are available.</p>
  {% endif %}
</body>
</html>
```

---

참고 :  
[https://www.djangoproject.com/](https://www.djangoproject.com/),  
[django tutorial](https://developer.mozilla.org/ko/docs/Learn/Server-side/Django),
