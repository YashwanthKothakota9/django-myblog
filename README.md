- A `slug` is a short label that contains only letters,
numbers, underscores, or hyphens.

- `BigAutoField` is `64-bit` integer that automatically increments according to available IDs.

- `timezone.now` returns current datetime in a timezone-aware format.

- To use database-generated default values, we use the `db_default` attribute instead of `default`.

- By using `auto_now_add`, the date will be saved automatically when creating an object.

- By using `auto_now`, the date will be updated automatically when saving an object.

- `Meta` class defines metadata for the model.
  
- `Index ordering` is not supported on `MySQL`. If you use
MySQL for the database, a descending index will be created
as a normal index

- We use `related_name` to specify the name of the reverse relationship, from `User` to `Post`. This will allow us to access related objects easily from a user object by using the `user.blog_posts` notation.

- The `sqlmigrate` command takes the migration names and returns their SQL without executing it.

- We can specify a custom database name for your model in the `Meta` class of the model using the `db_table` attribute.

Django creates an auto-incremental id column that is used as the primary
key for each model, but you can also override this by specifying `primary_key=True` on one of your model fields. The default `id` column
consists of an integer that is incremented automatically. This column
corresponds to the `id` field that is automatically added to your model.

- `facet counts` indicate the number of objects corresponding to each specific filter.

- The `Django ORM` is compatible with MySQL, PostgreSQL, SQLite, Oracle, and MariaDB.
- The Django ORM is based on `QuerySets`. A QuerySet is a collection of
database queries to retrieve objects from your database. You can apply filters to QuerySets to narrow down the query results based on given parameters.

- `get_or_create()` method facilitates this by either retrieving an object or creating it if not found.
- Django model has at least one manager, and the default manager is called `objects`. You get a QuerySet object using your model manager.
- To retrieve all objects from a table, we use the all() method on the default objects manager.
```py
all_posts = Post.objects.all()
```

- Django QuerySets are lazy, which means they are only evaluated when they are forced to.
- To filter a QuerySet, you can use the `filter()` method of the manager.
- Two underscores are used to define the lookup type, with the format
`field__lookup`.
- The `contains` lookup translates to a SQL lookup using the `LIKE` operator

Examples:
```py
Post.objects.filter(id__in=[1, 3])
Post.objects.filter(id__gt=3)
Post.objects.filter(id__gte=3)
Post.objects.filter(id__lt=3)
Post.objects.filter(id__lte=3)
Post.objects.filter(title__istartswith='who')
Post.objects.filter(title__iendswith='reinhardt?')
```

```py
from datetime import date
Post.objects.filter(publish__date=date(2024, 1, 31))
Post.objects.filter(publish__year=2024)
Post.objects.filter(publish__month=1)
Post.objects.filter(publish__day=1)
Post.objects.filter(publish__date__gt=date(2024, 1, 1))
Post.objects.filter(author__username='admin')
Post.objects.filter(author__username__starstwith='ad')
Post.objects.filter(publish__year=2024, author__username='admin')
```

```py
Post.objects.filter(publish__year=2024) \
     .filter(author__username='admin')
```

```py
Post.objects.filter(publish__year=2024) \
     .exclude(title__startswith='Why')
```

```py
Post.objects.order_by('title')
Post.objects.order_by('-title')
Post.objects.order_by('author', 'title')
Post.objects.order_by('?') #To order randomly
```

```py
Post.objects.all()[:5] #limit 5
Post.objects.all()[3:6] #offset 3 limit 6
Post.objects.order_by('?')[0]
```

```py
Post.objects.filter(id_lt=3).count()
Post.objects.filter(title__startswith='Why').exists()
```

```py
post = Post.objects.get(id=1)
post.delete()
```

- A `Q` object allows you to encapsulate a collection of field lookups. You can compose statements by combining Q objects with the & (and), | (or), and ^(xor) operators.
```py
from django.db.models import Q
starts_who = Q(title__istartswith='who')
starts_why = Q(title__istartswith='why')
Post.objects.filter(starts_who | starts_why)
```

- Creating a QuerySet doesn’t involve any database activity until it is
evaluated. When a QuerySet is evaluated, it translates into a SQL query to the database.

QuerySets are only evaluated in the following cases:
- The first time you iterate over them
- When you slice them, for instance, Post.objects.all()[:3]
- When you pickle or cache them
- When you call repr() or len() on them
- When you explicitly call list() on them
- When you test them in a statement, such as bool(), or, and, or if
  

- URL patterns allow you to map URLs to views. A URL pattern is composed
of a string pattern, a view, and, optionally, a name that allows you to name the URL project-wide.

- `slug` (a string that can only contain letters, numbers, underscores, or hyphens).
- `Canonical URLs` allow you to specify the URL for the master copy of a
page. Django allows you to implement the `get_absolute_url()` method in
your models to return the canonical URL for the object.
- Class-based views are an alternative way to implement views as Python
objects instead of functions. Since a view is a function that takes a web
request and returns a web response, you can also define your views as class methods. Django provides base view classes that you can use to implement your own views. All of them inherit from the `View` class, which handles HTTP method dispatching and other common functionalities.


`Class-based views` offer some advantages over function-based views that are useful for specific use cases. Class-based views allow you to:
- Organize code related to HTTP methods, such as GET, POST, or PUT, in
separate methods, instead of using conditional branching.
- Use multiple inheritance to create reusable view classes (also known as
`mixins`).

Django comes with two base classes to build forms:
- `Form`: This allows you to build standard forms by defining fields and
validations.
- `ModelForm`: This allows you to build forms tied to model instances. It
provides all the functionalities of the base Form class, but form fields
can be explicitly declared, or automatically generated, from model
fields. The form can be used to create or edit model instances.

- The `django-anymail` application simplifies the task of adding email service providers to your project like `SendGrid` or `Amazon SES`.

- To write emails to console
`EMAIL_BACKEND = 'django.core.mail.backends.console.EmailBackend'`

- By default, Django checks for the `CSRF token` in all POST requests. Remember to include the `csrf_token` tag in all forms that are submitted via `POST`.