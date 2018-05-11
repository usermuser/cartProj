# cartProj
https://github.com/diefenbach/django-lfs/blob/master/lfs/cart/models.py

## Для начала нужно создать каталог с товарами и продуктами

# Корзине нужны функции для корзины (добавить товар, удалить, получить корзину)

def add_to_cart():
def remove_from_cart():
def get_cart():

корзина будет храниться в сессии.

## Тут будет описание как реализовать хранение корзины в сессии СТРАНИЦА 217
We will use Django's session framework to persist the cart. The cart will be kept in
the session until it finishes or the user checks out of the cart. We will also need
to build additional Django models for the cart and its items.

Using Django sessions
Django provides a session framework that supports anonymous and user sessions.
The session framework allows you to store arbitrary data for each visitor. Session
data is stored on the server side, and cookies contain the session ID, unless you use
the cookie-based session engine. The session middleware manages sending and
receiving cookies. The default session engine stores session data in the database,
but as you will see next, you can choose between different session engines.
To use sessions, you have to make sure that the MIDDLEWARE_CLASSES setting of your
project contains 'django.contrib.sessions.middleware.SessionMiddleware' .
This middleware manages sessions and is added by default when you create a new
project using the startproject command.

The session middleware makes the current session available in the request object.
You can access the current session using request.session , by utilizing it similar to
a Python dictionary to store and retrieve session data. The session dictionary accepts
any Python object by default that can be serialized into JSON. You can set a variable
in the session like this:

request.session['foo'] = 'bar'

Retrieve a session key:

request.session.get('foo')

Delete a key you stored in the session:

del request.session['foo']

As you saw, we just treated request.session like a standard Python dictionary.
When users log into the site, their anonymous session is lost and a new
session is created for the authenticated users. If you store items in an
anonymous session that you need to keep after users log in, you will have
to copy the old session data into the new session


если пользователь не залогинился или не зарегистрировался тогда его считаем анонимом.

class Cart(models.Model):
	pass

class Customer(models.Model):
	pass

не забываем добавить __str__ метод

## смотри ниже пример из доки по джанге

'''
from django.db import models
from django.utils.encoding import python_2_unicode_compatible

@python_2_unicode_compatible  # only if you need to support Python 2
class Question(models.Model):
    # ...
    def __str__(self):
        return self.question_text
'''

## Внешний вид корзины примерно следующий

Товар  |  Количество  |    Цена
       |              |
=======+==============+==========
       |              |
товар1 |     - 2 +    |    10 руб.
товар2 |     - 1 +    |    15 руб.
       |              |
=======+==============+==========
Итого:        3          25 руб.


Когда пользователь находится в каталоге товаров, под каждым товаром должна быть 
надпись "В корзину".
Опционально: если товар уже находится в корзине, то под товаром в каталоге
должна быть надпись "В корзине"

Иконка корзины должна быть в шапке, и корзина должна быть видна везде, даже при перемотке.
Возле иконки корзины отображать количество товаров в ней.