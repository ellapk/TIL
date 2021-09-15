# Django admin


**settings.py**
```
INSTALLED_APPS = [
    'django.contrib.admin',
]
```
- superuser 계정에 한해 접근 가능



**model.py**

1. 기본 Model Admin등록

```
# myapp/admin.py
from django.contrib import admin
from blog.models import Post


admin.site.register(Post) # 기본 ModelAdmin으로 등록
```


2. ```admin.ModelAdmin``` 상속을 통해 커스터마이징

```
# myapp/admin.py
from django.contrib import admin
from blog.models import Post

class PostAdmin(admin.ModelAdmin):
    list_display = ['id', 'title', 'created_at', 'updated_at' ]

admin.site.register(Post, PostAdmin)
```



3. 장식자 형태로 등록
```
# myapp/admin.py
from django.contrib import admin
from blog.models import Post

@admin.register(Post)

class PostAdmin(admin.ModelAdmin):

    list_display = ['id', 'title', 'content']

    list_display_links = ['id', 'title']

```   


- 나는 tartproject에 2번 방식으로 Question class등등...작성 

```
class Question(models.Model):

    question_text = models.CharField(max_length=200,default='')

    pub_date = models.DateTimeField('date published')

    list_filter = ['pub_date']

    @admin.display(
        boolean=True,
        ordering='pub_date',
        description='Published recently?',
    )
    def was_published_recently(self):
        now = timezone.now()
        return now - DateTimeCheckMixin.timedelta(days=1) <= self.pub_date <= now

    def __str__(self): 
        return self.question_text


    class Meta:
    	verbose_name_plural = '선택 가능 종류'
```

**modeladmin_options**
- list_display : Admin 목록에 보여질 필드 목록

- list_display_links : 목록 내에서 링크로 지정할 필드 목록 

- list_editable : 목록 상에서 수정할 필드 목록

- list_filter : 필터 옵션을 제공할 필드 목록. 원하는 값만 filtering 가능

- search_fields : 원하는 데이터 검색 가능




**admin.py**

```
from .models import Choice, Question, Post

class QuestionAdmin(admin.ModelAdmin):
    fieldsets = [
        (None,               {'fields': ['question_text']}),
        ('Date information', {'fields': ['pub_date'], 'classes': ['collapse']}),
    ]
    list_filter = ['pub_date'] # 필터 사이드바 추가

admin.site.register(Question,QuestionAdmin) 
```
- admin.py파일 내에 원하는 모델을 import, register, unregister 하기