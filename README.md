# cartProj
https://github.com/diefenbach/django-lfs/blob/master/lfs/cart/models.py
1. для начала нужны функции для корзины (добавить товар, удалить, получить корзину)

def add_to_cart():
def remove_from_cart():
def get_cart():

корзина будет храниться в сессии.
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
надпись "В коризну".
Опционально: если товар уже находится в корзине, то под товаром в каталоге
должна быть надпись "В корзине"

Иконка корзины должна быть в шапке, и корзина должна быть видна везде, даже при перемотке.
Возле иконки корзины отображать количество товаров в ней.