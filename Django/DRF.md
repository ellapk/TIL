# Rest framework (Django)

## 사용기술
**1. Django**
-

- 파이썬으로 만든 무료 오픈소스 웹 애플리케이션 프레임워크.
- 웹사이트 구축시, 회원가입, 로그인, 로그아웃과 같은 필수적인 구성요소들을 갖춤.


**2. Django Rest Framework(DRF)**
-
- Django에서 RESTful API 서버를 쉽게 구축할 수 있도록 도와주는 오픈 소스 라이브러리
- REST란 HTTP URL + HTTP Method(GET, POST, PUT, DELETE) 을 사용하여 API를 더 잘 쓸 수 있도록 도와주는 프레임워크.



## **View**
```
from django.contrib.auth.models import User, Group
from rest_framework import viewsets
from rest_framework import permissions
from tutorial.quickstart.serializers import UserSerializer, GroupSerializer


class UserViewSet(viewsets.ModelViewSet):

    """
    API endpoint that allows users to be viewed or edited.
    """
    
    queryset = User.objects.all().order_by('-date_joined')

    serializer_class = UserSerializer

    permission_classes = [permissions.IsAuthenticated]


class GroupViewSet(viewsets.ModelViewSet):

    """
    API endpoint that allows groups to be viewed or edited.
    """

    queryset = Group.objects.all()

    serializer_class = GroupSerializer

    permission_classes = [permissions.IsAuthenticated]
```

- 상단의 코드는 ViewSets라는 클래스로 그룹화한 코드이다. 뷰 논리가 간결하고 잘 정리되어 있다는 특징..
- Django의 View 클래스로 RESTful한 서버를 구축한다. GET, POST, PUT, DELETE를 오버라이딩해서 구현하면 각 HTTP의 메소드에 따라 HTML 응답이 아닌 JSON 혹은 XML로 응답하게 된다.


## **Serializer**


```
from django.contrib.auth.models import User, Group
from rest_framework import serializers


class UserSerializer(serializers.HyperlinkedModelSerializer):
    class Meta:

        model = User

        fields = ['url', 'username', 'email', 'groups']


class GroupSerializer(serializers.HyperlinkedModelSerializer):

    class Meta:

        model = Group

        fields = ['url', 'name']
```

- Serializer로 사용자 DB의 이름, 이메일, 성별 등을 직렬화한다. 
- 추가로, Serializer를 사용하기 이전에 DB sync -> initial user create 필요

```
python manage.py migrate
```
```
python manage.py createsuperuser --email admin@example.com --username admin
```
