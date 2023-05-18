# class-based-generic-views

##Django comes with a handful of built-in generic views to help generate list and detail views of objects.

`models.py`
```python
from django.db import models 

class Publisher(models.Model):
   name=models.CharField(max_length=112)
   adress=models.CharField(max_length=112)
   phone=models.CharField(max_length=120)
   website=models.URLField()
   country=models.CharField(max_length=120)
   
   
   
   def __str__(self):
   
   
      return self.name
      
      
 class Book(models.Model):
    title = models.CharField(max_length=100)
    authors = models.ManyToManyField("Author")
    publisher = models.ForeignKey(Publisher, on_delete=models.CASCADE)
    publication_date = models.DateField()
```   
      
-----------------------------------------------------------------------------------------------------------------------------------
-----------------------------------------------------------------------------------------------------------------------------------
-----------------------------------------------------------------------------------------------------------------------------------
`views.py`
```python
from django.views.generic import ListView
from books.models import Publisher

class PublisherListView(ListView):
    model=Publisher
    
 ```     
------------------------------------------------------------------------------------------------------------------------------------
------------------------------------------------------------------------------------------------------------------------------------
------------------------------------------------------------------------------------------------------------------------------------

`urls.py`

```python
from django.urls import path
from books.views import PublisherListView

urlpatterns = [
    path("publishers/", PublisherListView.as_view()),
]
```  
-----------------------------------------------------------------------------------------------------------------------------------
-----------------------------------------------------------------------------------------------------------------------------------
-----------------------------------------------------------------------------------------------------------------------------------
#template rendering 

`publisher_list.html`
```html
{% extends "base.html" %}

{% block content %}
    <h2>Publishers</h2>
    <ul>
        {% for publisher in object_list %}
            <li>{{ publisher.name }}</li>
        {% endfor %}
    </ul>
{% endblock %}
   

```


