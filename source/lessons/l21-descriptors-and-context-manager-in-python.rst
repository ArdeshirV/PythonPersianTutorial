.. role:: emoji-size

.. meta::
   :description: پایتون به پارسی - کتاب آنلاین و آزاد آموزش زبان برنامه‌نویسی پایتون - درس بیست و یکم: شی گرایی (OOP) در پایتون: Context Manager ،Descriptors ،Decorator


.. _lesson-21:

درس ۲۱: شی گرایی (OOP) در پایتون: Context Manager ،Descriptors ،Decorator
===================================================================================================

.. figure:: /_static/pages/21-python-object-oriented-programming-property-descriptors.jpg
    :align: center
    :alt: شی گرایی (OOP) در پایتون: __Descriptors ، Context Manager ،Decorator ،__slots و property@
    :class: page-image

    Photo by `Mathyas Kurmann <https://unsplash.com/photos/fb7yNPbT0l8>`__
  
این درس نیز در ادامه مجموعه دروس آموزش شی گرایی در زبان برنامه‌نویسی پایتون می‌باشد که به شرح و جمع‌بندی برخی موارد مرتبط با مفاهیم کلاس و شی موجود در پایتون می‌پردازد. مواردی که ممکن است قابل گذر باشند ولی هریک نکاتی دارند که در توسعه برنامه شی گرای پایتونی به شما کمک خواهند کرد. مواردی همچون صفت ویژه __slots__ در کلاس‌ها، ایجاد Decorator با استفاده از کلاس در پایتون و همچنین ایجاد قابلیت getter و setter در پایتون با استفاده از مفاهیم Descriptors و دکوراتور property که در ادامه تا حد کافی شرح داده خواهند شد.


:emoji-size:`✔` سطح: متوسط

----


.. contents:: سرفصل‌ها
    :depth: 2

----


__slots__
----------------------------

پیش از هر توضیحی به نمونه کد زیر توجه نمایید:


.. code-block:: python
    :linenos: 

    class Sample:
        def __init__(self, a, b):
            self.a = a
            self.b = b


    objet = Sample(1, 2)
    print(objet.__dict__)

    print('-' * 30)

    objet.c = 3
    print(objet.__dict__)

    print('-' * 30)

    objet.__dict__['d'] = 4
    print(objet.__dict__)
    print(objet.d)

::

    {'a': 1, 'b': 2}
    ------------------------------
    {'a': 1, 'b': 2, 'c': 3}
    ------------------------------
    {'a': 1, 'b': 2, 'c': 3, 'd': 4}
    4

پیشتر نیز صحبت کرده بودیم، می‌توان حتی پس از ایجاد یک شی نیز به آن Attribute جدید اضافه کنیم (به دو سطر ۱۲ و ۱۷ توجه نمایید). داده‌های مربوط به تمام Attributeهای یک شی توسط یک شی دیکشنری که از طریق ``__dict__`` در دسترس می‌باشد، نگهداری می‌شود. در پس زمینه پایتون این ``__dict__`` می‌باشد که امکان افزودن Attribute به شی را به صورت پویا (Dynamic) فراهم آورده است.

``__slots__`` [`اسناد پایتون <https://docs.python.org/3/reference/datamodel.html#slots>`__] یک Attribute ویژه در پایتون می‌باشد که با مقداردهی آن می‌توان از ایجاد ``__dict__`` جلوگیری و در نتیجه قابلیت افزودن Attribute جدید به شی را غیرفعال و تعداد Attributeهای آن را از همان نقطه ایجاد، ثابت نگه‌داشت:


.. code-block:: python
    :linenos: 

    class Sample:

        __slots__ = ('a', 'b')

        def __init__(self, a, b):
            self.a = a
            self.b = b


    obj = Sample(1, 2)
    print(obj.__dict__)

::

    Traceback (most recent call last):
      File "sample.py", line 11, in <module>
        print(obj.__dict__)
    AttributeError: 'Sample' object has no attribute '__dict__'


از مزایای ``__slots__`` می‌توان به کاهش مصرف حافطه (RAM) به خصوص در مورد کلاس‌هایی که قرار است اشیایی خیلی زیادی از آن‌ها ایجاد گردد، اشاره نمود.


از طریق ``__slots__`` همچنین می‌توان اجازه داد که کدام Attribute در آینده برای شی ایجاد گردد:

.. code-block:: python
    :linenos: 

    class Sample:

        __slots__ = ('a', 'b', 'c')

        def __init__(self, a, b):
            self.a = a
            self.b = b

    objet = Sample(1, 2)

    objet.c = 3

    print('a: ', objet.a)
    print('b: ', objet.b)
    print('c: ', objet.c)

    objet.d = 4

::


    a:  1
    b:  2
    c:  3
    Traceback (most recent call last):
      File "sample.py", line 17, in <module>
        objet.d = 4
    AttributeError: 'Sample' object has no attribute 'd'



**اکنون نمونه کد زیر را در وضعیت وراثت در نظر بگیرید:**

.. code-block:: python
    :linenos: 

    class Parent:
        def __init__(self, a, b):
            self.a = a
            self.b = b


    class Child(Parent):
        def __init__(self, a, b):
            super().__init__(a, b)


    child = Child(1, 2)
    print(child.__dict__)

    child.c = 3
    print(child.__dict__)

    print('a: ', child.a)
    print('b: ', child.b)
    print('c: ', child.c)

::

    {'a': 1, 'b': 2}
    {'a': 1, 'b': 2, 'c': 3}
    a:  1
    b:  2
    c:  3


اگر کلاس Parent شامل ``__slots__`` بوده و در نتیجه فاقد ``__dict__`` باشد:

.. code-block:: python
    :linenos: 

    class Parent:
        __slots__ = ('a', 'b')

        def __init__(self, a, b):
            self.a = a
            self.b = b


    class Child(Parent):

        def __init__(self, a, b):
            super().__init__(a, b)


    child = Child(1, 2)
    print(child.__dict__)

    child.c = 3
    print(child.__dict__)

    print('a: ', child.a)
    print('b: ', child.b)
    print('c: ', child.c)


::

     {}
     {'c': 3}
     a:  1
     b:  2
     c:  3

اگر هر دو کلاس شامل ``__slots__`` باشند:

.. code-block:: python
    :linenos: 

    class Parent:
        __slots__ = ('a', 'b')

        def __init__(self, a, b):
            self.a = a
            self.b = b


    class Child(Parent):
        __slots__ = ('c')

        def __init__(self, a, b):
            super().__init__(a, b)


    child = Child(1, 2)

    child.c = 3
    print('a: ', child.a)
    print('b: ', child.b)
    print('c: ', child.c)

::

    a:  1
    b:  2
    c:  3


**در وراثت چندگانه،** چنانچه ``__slots__`` مربوط به superclassها حاوی مقدار تکراری باشد، آنگاه باعث بروز خطا می‌گردد:

.. code-block:: python
    :linenos: 

    class ParentOne:
        __slots__ = ('a', 'b')

    class ParentTwo:
        __slots__ = ('z', 'b')


    class Child(ParentOne, ParentTwo):
        __slots__ = ('c')


    child = Child()

::

    Traceback (most recent call last):
      File "sample.py", line 8, in <module>
        class Child(ParentOne, ParentTwo):
    TypeError: multiple bases have instance lay-out conflict


بهتر است superclassها حاوی یک ``__slots__`` خالی (شی توپِل خالی) باشند و هر subclass خود محتوای ``__slots__`` خود را تعریف نماید:

.. code-block:: python
    :linenos: 

    class ParentOne:
        __slots__ = ()

    class ParentTwo:
        __slots__ = ()


    class Child(ParentOne, ParentTwo):
        __slots__ = ('a', 'b', 'z', 'c')


    child = Child()


در مواقع خاص که می‌خواهید هم Attributeها را محدود کنید و هم قابلیت ``__dict__`` را حفظ کنید، می‌توانید ``__dict__`` را هم به مقدار ``__slots__`` اضافه نمایید.


|


[`مطالعه بیشتر: پرسش و پاسخ مرتبط در StackOverflow <https://stackoverflow.com/a/28059785>`__]

Decorators
----------------------------

از درس سیزدهم با مفهوم Decoratorها و نیز کاربرد آن‌ها به همراه تابع در زبان برنامه‌نویسی پایتون آشنا شده‌ایم، در این بخش به بررسی Decoratorها به همراه کلاس‌ها و متدها می‌پردازیم.

علاوه بر اینکه با استفاده از کلاس می‌توان یک Decorator ایجاد کرد، از Decorator‌ها نیز می‌توان بر روی کلاس یا متدهای داخل یک کلاس بهره گرفت. در ادامه به بررسی این موارد می‌پردازیم.


.. _python-decorator-on-methods:

قراردادن Decorator بر روی متد
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

این کار همانند قراردادن Decorator بر روی تابع می‌باشد (درس سیزدهم) و تفاوتی ندارد. پیش‌تر نیز از Decoratorهایی همچون ``classmethod@`` یا ``staticmethod@`` بر روی متدها استفاده می‌کردیم. به مثالی در همین زمینه توجه نمایید:


.. code-block:: python
    :linenos:

    import functools

    def debug(func):
        """Print the function signature and return value
           Source: https://realpython.com/primer-on-python-decorators/#debugging-code"""

        @functools.wraps(func)
        def wrapper_debug(*args, **kwargs):
            args_repr = [repr(a) for a in args]                     
            kwargs_repr = [f"{k}={v!r}" for k, v in kwargs.items()]
            signature = ", ".join(args_repr + kwargs_repr)      
            print(f"Calling {func.__name__}({signature})")
            value = func(*args, **kwargs)
            print(f"{func.__name__!r} returned {value!r}")       
            return value
        return wrapper_debug



    class Sample:

        @debug
        def __init__(self, x=0, y=0):
            self.x = x
            self.y = y


    sample = Sample(5, y=6)

::

    Calling __init__(<__main__.Sample object at 0x7fd96ddec8d0>, 5, y=6)
    '__init__' returned None

در نمونه کد بالا یک Decorator با نام ``debug`` ایجاد گردیده است (Decorator درس سیزدهم و f-string درس هفتم)، با قراردادن این Decorator بر روی یک تابع یا متد: نام تابع، آرگومان‌های ارسال شده و همچنین مقدار خروجی تابع را بر روی خروجی نمایش می‌دهد.


.. _python-decorator-on-class:

قراردادن Decorator بر روی کلاس
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

در زبان برنامه‌نویسی پایتون می‌توان یک Decorator را به کل یک کلاس اعمال کرد، در این صورت نیز تفاوتی با آنچه در توابع دیدیم، نمی‌کند. تنها در این حالت، این کلاس است که به Decorator ارسال می‌گردد. دو نمونه کد زیر معادل یکدیگر هستند::


    def decorator_name(a_class):
        def wrapper():
            # Do Something!
            print('Class name:', a_class.__name__)
            return a_class()

        return wrapper


::

     # 1

     @decorator_name
     class Sample():
         pass


     sample = Sample()


::

      # 2

      class Sample():
          pass

      SampleWrapper = decorator_name(Sample)
      sample = SampleWrapper()


::

      # Output

      Class name: Sample



.. _python-decorator-class:

کلاس به عنوان Decorator
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

در زبان برنامه‌نویسی پایتون می‌توان از کلاس‌ها همچون توابع برای ایجاد Decorator استفاده کرد. در این صورت شی‌ای که Decorator به آن اعمال شده است از طریق متد ``__init__`` دریافت می‌گردد. همچنین می‌بایست متد ``__call__`` را پیاده‌سازی کرده باشیم تا اشیای کلاس قابلیت callable را داشته باشند (درس هفدهم)، عملیات اصلی Decorator می‌بایست داخل این متد پیاده‌سازی گردد:



::

    class CountCalls:
        def __init__(self, func):
            self.func = func
            self.num_calls = 0

        def __call__(self):
            self.num_calls += 1
            print(f"Call {self.num_calls} of {self.func.__name__!r}")
            return self.func()

::

    # 1

    @CountCalls
    def func():
        ''' a function'''

    print(func.__doc__)
    func()
    func()


::

    # 2

    def func():
        ''' a function'''

    obj = CountCalls(func)

    print(obj.__doc__)
    obj()
    obj()


::


    # Output

    None
    Call 1 of 'func'
    Call 2 of 'func'



**functools.update_wrapper**

همانند کاربرد تابع ``wraps`` از ماژول ``functools`` در هنگام ساخت Decorator از توابع، در اینجا نیز می‌توانیم جهت حفظ اطلاعات مربوط به تابع اصلی، این‌بار از تابع ``update_wrapper`` این ماژول استقاده کنیم [`اسناد پایتون <https://docs.python.org/3/library/functools.html#functools.update_wrapper>`__] - اگر کلاس CountCalls را به صورت زیر تغییر دهیم، آنگاه خروجی هر دو حالت نیز به شرح زیر تغییر خواهد کرد، چرا که اکنون ``__doc__`` در دسترس باقی مانده است::


    import functools

    class CountCalls:
        def __init__(self, func):
            functools.update_wrapper(self, func)
            self.func = func
            self.num_calls = 0

        def __call__(self):
            self.num_calls += 1
            print(f"Call {self.num_calls} of {self.func.__name__!r}")
            return self.func()


::

     a function
     Call 1 of 'func'
     Call 2 of 'func'


Descriptors
----------------------------

توصیف‌گر (Descriptor) کلاسی است که کنترل عملیات‌های دریافت (get)، تنظیم (set) و حذف (delete) را بر روی یک attribute از شی‌ای دیگر را فراهم می‌کند. Descriptor یک راهکار پایتونی (Pythonic) برای ایجاد مکانیزم get & set رایج در دیگر زبان‌های برنامه‌نویسی می‌باشد.

**چگونه می‌توان یک Descriptor در پایتون ایجاد کرد؟** [`اسناد پایتون <https://docs.python.org/3/reference/datamodel.html#implementing-descriptors>`__]

۱- یک کلاس ایجاد کنیم که در آن حداقل یکی از متدهای خاص ``__set__`` ،``__get__`` و ``__delete__`` بازپیاده‌سازی (یا بهتر است بگوییم Override) شود.

۲- از شی این کلاس به عنوان مقدار attribute مناسب از کلاس مورد نظر استفاده کنیم.


**کاربرد Descriptor پایتون چیست؟**

هر زمان بخواهیم رویدادهایی همچون دریافت (get)، تنظیم (set) و حذف (delete) را بر روی یک attribute کنترل کنیم. برای مثال کلاسی شامل یک attribute با نام ایمیل (email) است، می‌خواهیم پیش از تنظیم مقدار بر روی این فیلد، مقدار جدید به صورت خودکار اعتبارسنجی (Validation) شود و در صورت صحت عملیات انجام شود:


.. code-block:: python
    :linenos:


    import re

    class EmailField:

        def __init__(self, email=None):
            self.email = email

        def __get__(self, instance, owner=None):
            print('-' * 10, 'CALLED[__get__]')
            print('instance:', instance)
            print('owner:', owner)
            print('-' * 30)
            print()

            return self.email

        def __set__(self, instance, value):
            print('-' * 10, 'CALLED[__set__]')
            print('instance:', instance)
            print('value:', value)
            print('-' * 30)

            if re.match('^[a-zA-Z0-9_.+-]+@[a-zA-Z0-9-]+.[a-zA-Z0-9-.]+$', value):
                self.email = value
                print('Successful!\n')
            else:
                print(f'{value} is not a valid email!\n')


    class Student:
        email = EmailField()


    obj = Student()

    email = obj.email               # CALLED[__get__]

    obj.email = 'python$$1400'      # CALLED[__set__]

    obj.email = 'python@coderz.ir'  # CALLED[__set__]

    print(obj.email)                # CALLED[__get__]


::

    ---------- CALLED[__get__]
    instance: <__main__.Student object at 0x7f828bb9f4e0>
    owner: <class '__main__.Student'>
    ------------------------------

    ---------- CALLED[__set__]
    instance: <__main__.Student object at 0x7f828bb9f4e0>
    value: python$$1400
    ------------------------------
    python$$1400 is not a valid email!

    ---------- CALLED[__set__]
    instance: <__main__.Student object at 0x7f828bb9f4e0>
    value: python@coderz.ir
    ------------------------------
    Successful!

    ---------- CALLED[__get__]
    instance: <__main__.Student object at 0x7f62e42c64e0>
    owner: <class '__main__.Student'>
    ------------------------------

    python@coderz.ir


در نمونه کد، بالا کلاس ``EmailField`` یک Descriptor برای اتریبیوت ``email`` از کلاس ``Student`` می‌باشد. همانطور که مشاهده می‌شود، هرگاه مقداری به ``email`` انتساب داده می‌شود (سطرهای ۳۸ و ۴۰)، به صورت خودکار متد ``__set__`` از کلاس Descriptor آن فراخوانی می‌گردد و به همین ترتیب هرگاه مقدار آن درخواست می‌گردد (سطرهای ۳۶ و ۴۲)، متد ``__get__`` فراخوانی می‌گردد.

پیشنهاد می‌شود در صورت امکان مقدار attribute را توسط Descriptor نگهداری نکنید و از Descriptor تنها برای انجام عملیات‌ مربوطه استفاده نمایید. بنابراین مثال قبل را می‌توانیم به صورت زیر بازنویسی نماییم:


.. code-block:: python
    :linenos:

    import re

    class EmailField:

        def __init__(self, attr_name):
            self.attr_name = attr_name

        def __get__(self, instance, owner=None):
            return instance.__dict__.get(self.attr_name)

        def __set__(self, instance, value):
            if re.match('^[a-zA-Z0-9_.+-]+@[a-zA-Z0-9-]+.[a-zA-Z0-9-.]+$', value):
                instance.__dict__[self.attr_name] = value


    class Student:
        email = EmailField('email')


    obj = Student()
    obj.email = 'python@coderz.ir'

    print(obj.email)


::

    python@coderz.ir


در این روش تنها نام attribute نگهداری و از آن برای دستیابی به مقدار آن attribute، از طریق خود شی اقدام کردیم.

اگر از **نسخه 3.6 به بعد پایتون** بهره‌مند هستید،‌ با استفاده از متد ``__set_name__`` [`اسناد پایتون <https://docs.python.org/3/reference/datamodel.html#object.__set_name__>`__] در کلاس Descriptor، دیگر حتی نیازی به پیاده‌سازی متد ``__init__`` و ارسال دستی نام attribute هم نخواهد بود:


.. code-block:: python
    :linenos:

    import re

    class EmailField:

        def __set_name__(self, owner, name):
            self.attr_name = name

        def __get__(self, instance, owner=None):
            return instance.__dict__.get(self.attr_name)

        def __set__(self, instance, value):
            if re.match('^[a-zA-Z0-9_.+-]+@[a-zA-Z0-9-]+.[a-zA-Z0-9-.]+$', value):
                instance.__dict__[self.attr_name] = value


    class Student:
        email = EmailField()


.. tip:: 

  از Descriptor تنها برای Class Attributeها می‌توان استفاده کرد.




property@
----------------------------

خیلی ساده، این دکوراتور (``property@``) را می‌توان یک Descriptor سطح بالا دانست که توسط کتابخانه استاندارد پایتون برای Instance Attributeها فراهم آورده شده است. به نمونه کد زیر توجه نمایید:

.. code-block:: python
    :linenos:

    import re

    class Contact:

        def __init__(self, name, phone):
            self._name = name
            self._phone = phone

        @property
        def name(self):
            return self._name
	
        @name.setter
        def name(self, new_name):
            if new_name and len(new_name) > 0:
                self._name = new_name
            else:
                print("Please enter a valid name")

        @name.deleter
        def name(self):
            del self._name

        @property
        def phone(self):
            return self._phone


        @phone.setter
        def phone(self, new_phone):
            if re.match(r'^09\d{9}$', new_phone):
                self._phone = new_phone
            else:
                print("Please enter a valid phone")

        @phone.deleter
        def phone(self):
            del self._phone


    obj = Contact(name='Saeid', phone='09999999999')

    obj.phone = '09123456'
    print('-' * 30)
    print(obj.name)
    print(obj.phone)


::

     Please enter a valid phone
     ------------------------------
     Saeid
     09999999999


در این مثال، کلاس ``Contact`` حاوی دو Instance Attribute با نام‌های ``name`` و ``phone`` می‌باشد. برای اینکه بتوانیم رویدادهایی همچون دریافت (get)، تنظیم (set) و حذف (delete) را بر روی آن‌ها کنترل کنیم، از دکوراتور ``property@`` استفاده کردیم. به این صورت که:

**۱-** نخست باید توجه داشت که نام Attributeها با یک کاراکتر ``_`` شروع کردیم. با این کار به دیگر برنامه‌نویسان خواهیم گفت که این Attribute با سطح دسترسی protected می‌باشد (درس بیستم)::

    def __init__(self, name, phone):
        self._name = name
        self._phone = phone

**۲-** برای هر کدام یک متد getter ساختیم و به آن دکوراتور ``property@`` انتساب دادیم. نام این متد را همنام با Attributeها ولی بدون ``_`` انتخاب کردیم::

    @property
    def name(self):
        return self._name

    @property
    def phone(self):
        return self._phone   


نام این متد هر چیزی انتخاب شود، در زمان درخواست مقدار Attribute باید از این نام (به جای نام اصلی Attribute) استفاده گردد (سطرهای ۴۵ و ۴۶).

**۳-** اکنون می‌توانیم دو متد دیگر برای عملیات set و delete پیاده‌سازی کنیم و به آن‌ها دکوراتورهای زیر را انتساب دهیم::

     @<property_getter_method_name>.setter
     @<property_getter_method_name>.deleter


بخش نخست از نام دکوراتور (property_getter_method_name) می‌بایست همان نام متد getter باشد.

در این مثال ما از همان نام متد getter برای نام‌گذاری این دو متد استفاده کردیم. ولی باید توجه داشته باشید که نام این دو متد هر چیزی انتخاب شود، در زمان تنظیم مقدار (سطر ۴۳) یا حذف Attribute باید از این نام (به جای نام اصلی Attribute) استفاده گردد.



.. tip:: 

  از ``property@`` تنها برای Instance Attributeها می‌توان استفاده کرد.


یک کاربرد پنهان در استفاده از ``property@``، امکان ایجاد Attributeهای **read-only** و غیرقابل تغییر پس از نمونه‌سازی شی خواهد بود. برای این منظور تنها کافی است از پیاده‌سازی متد setter صرف‌نظر کنیم! به نمونه کد پایین توجه نمایید:


.. code-block:: python
    :linenos:

    class StaticNumber:

        def __init__(self, number):
            self._number = number

        @property
        def number(self):
            return self._number



    obj = StaticNumber(number='000111')

    obj.number = '000222'

::

    Traceback (most recent call last):
      File "sample.py", line 14, in <module>
        obj.number = '000222'
    AttributeError: can't set attribute




  
  
Context Manager و دستور ``with/as``
------------------------------------------

یکی دیگر از قابلیت‌های کمتر شناخته شده در زبان برنامه‌نویسی پایتون، Context Manager می‌باشد [`اسناد پایتون <http://docs.python.org/3/library/stdtypes.html#typecontextmanager>`__]. با این حال اکثر برنامه‌نویسان پایتون به صورت مداوم از آن بهره می‌گیرند. اگر درس دهم را به یاد داشته باشیم، از دستور ``with/as`` برای کار با فایل‌ها در پایتون استفاده می‌کردیم و شاهد راحتی و زیبایی کارها نسبت به قبل بودیم. در آن زمان تنها اشاره شد که شی فایل پایتون را می‌توان با دستور ``with/as`` استفاده کرد چون این شی از قابلیت Context Manager پشتیبانی می‌کند.

به صورت کلی Context Manager در زبان برنامه‌نویسی پایتون قابلیتی برای مدیرت منابع (فایل‌ها، دیتابیس، ارتباط و سایر منابع) می‌باشد، منابعی که کار کردن با آن‌ها همواره نیازمند عملیات‌ ثابتی همچون باز (Open) و بسته (Close) - Start/Stop, Lock/Release, Change/Reset - کردن هستند. 

در این بخش می‌خواهیم به بررسی چگونگی ایجاد یک کلاس به همراه قابلیت  Context Manager بپردازیم که در نهایت از اشیای آن بتوانیم در کنار دستور ``with/as`` استفاده نماییم. ابتدا اجازه دهید بار دیگر ساختار دستور ``with/as`` را بررسی نماییم::

    with context_expression [as target]:
        with_statement_body

در این ساختار بخش ``as`` اختیاری بوده و تنها زمانی که در داخل بدنه دستور ``with`` به شی تولید شده توسط ``context_expression`` نیاز داشته باشیم، استفاده می‌گردد؛ در این صورت یک ارجاع از شی مورد نیاز به نام دلخواه ``target`` ایجاد و در دسترس قرار می‌گیرد. ``context_expression`` نیز معرف یک شی‌ای است که توانایی مدیریت یا handle کردن دو وضعیت «ورود به» (entry into) و «خروج از» (exit from) را داشته باشد. برای ایجاد همچین شی‌ای می‌بایست دو متد خاص ``__enter__`` 	[`اسناد پایتون <https://docs.python.domainunion.de/3/reference/datamodel.html#object.__enter__>`__] و ``__exit__`` [`اسناد پایتون <https://docs.python.domainunion.de/3/reference/datamodel.html#object.__exit__>`__] را در کلاس مورد نظر خود پیاده‌سازی کنیم:

.. code-block:: python
    :linenos:
    
    class SampleContextManager:
        def __enter__(self):
            print('---> Entered into context manager!')

        def __exit__(self, *args):
            print('<--- Exiting from context manager!')


    with SampleContextManager():
        print('Inside context manager!')

::

    ---> Entered into context manager!
    Inside context manager!
    <--- Exiting from context manager!

همانطوری که از خروجی نمونه کد بالا قابل مشاهده می‌باشد، در هنگام اجرای دستور ``with``، ابتدا متد ``__enter__`` از شی Context Manager و سپس دستورات داخل بدنه دستور ``with`` و در نهایت نیز متد ``__exit__`` از شی Context Manager اجرا می‌گردد.


اگر بخواهیم کمی عمیق‌تر به ماجرا نگاه کنیم:

* اجرای متد ``__enter__`` زمانی است که خط اجرای برنامه می‌خواهد وارد اجرای دستورات داخل ``with`` یا به اصطلاح  وارد runtime context شود و خروجی این متد می‌بایست شی‌ای باشد که می‌خواهیم در طول اجرای دستور  ``with`` یا به اصطلاح context، با آن کار کنیم. البته خروجی می‌تواند ``None`` باشد ولی باید توجه داشت که خروجی این متد است که توسط دستور ``as`` به نام ``target`` ارجاع می‌خورد!

* اجرای متد ``__exit__`` زمانی است که انجام کار دستورات ``with`` یا اجرای context به پایان رسیده است. این متد در واقع  فرصتی برای تمیزکاری یا به اصطلاح clean up کردن آثار اجرای context می‌باشد. به مانند پاک کردن فایل‌هایی که موقت ایجاد شده‌اند، حذف اشیای اضافی باقی‌مانده یا انجام عمل بستن یک فایل یا پایان دادن یک ارتباط (Connection) یا...

برای آشنایی بیشتر در نمونه کد زیر یک Wrapper برای شی فایل ایجاد کرده‌ایم:

.. code-block:: python
    :linenos:
    
    class FileWritterWrapper:
        def __init__(self, filename):
            self.filename = filename
        
        def __enter__(self):
            self.opened_file = open(self.filename, 'a')
            self.opened_file.write('====== OPEN FILE ======\n')
            return self.opened_file
    
        def __exit__(self, *args):
            self.opened_file.write('\n====== CLOSE FILE ======\n')
            self.opened_file.close()


    with FileWritterWrapper('test_log.txt') as managed_file:
        managed_file.write('Inside context manager!')

محتویات فایل test_log.txt، پس از اجرای کد بالا:

::

    
    ====== OPEN FILE ======
    Inside context manager!
    ====== CLOSE FILE ======

به متد ``__exit__`` برگردیم، براساس مستندات پایتون تعریف کامل این متد به شکل زیر است::

    __exit__(self, exc_type, exc_value, traceback)

سه پارامتر انتهایی در صورت بروز Exception هنگام اجرای context (دستورات داخل بدنه ``with``) دارای مقدار غیر ``None`` و در غیر این صورت برابر با مقدار ``None`` خواهند بود. وجود این مقادیر به معنی عدم پایان صحیح context می‌باشد که ممکن است بتواند در گرفتن تصمیم شما در زمان خروج از context تاثیر داشته باشد.

.. code-block:: python
    :linenos:

    class SampleContextManager:
        def __enter__(self):
            print('---> Entered into context manager!')

        def __exit__(self, exc_type, exc_value, traceback):
            print('exc_type:', exc_type)
            print('exc_value:', exc_value)
            print('traceback:', traceback)
            print('<--- Exiting from context manager!')


    with SampleContextManager():
        print('|||||||||Inside context manager! - Top')
        a = 8 / 0
        print('|||||||||Inside context manager! - Bottom')


    print('***FINISH***')

::

     ---> Entered into context manager!
     |||||||||Inside context manager! - Top
     exc_type: <class 'ZeroDivisionError'>
     exc_value: division by zero
     traceback: <traceback object at 0x7f1c8aebd0c8>
     <--- Exiting from context manager!
     Traceback (most recent call last):
       File "sample.py", line 14, in <module>
         a = 8 / 0
     ZeroDivisionError: division by zero


همان‌طور که از نمونه کد بالا قابل مشاهده است، در زمان اجرای دستورات context یک خطای (تقسیم بر صفر) ``ZeroDivisionError`` رخ داده است. نکته قابل توجه این است که حتی با وجود بروز خطا و ناتمام ماندن اجرای context، ولی بدنه متد ``__exit__`` به صورت کامل اجرا شده است. در واقع مفسر پایتون اعلام Exception را که می‌تواند منجر به توقف کل برنامه شود را به صورت موقت تا پایان اجرا ``__exit__`` معلق نگه می‌دارد.

در چنین حالتی اگر متد ``__exit__`` مقدار ``True`` را برگرداند، مفسر پایتون از بروز Exception خودداری خواهد کرد:

.. code-block:: python
    :linenos:

    class SampleContextManager:
        def __enter__(self):
            print('---> Entered into context manager!')

        def __exit__(self, exc_type, exc_value, traceback):
            print('exc_type:', exc_type)
            print('exc_value:', exc_value)
            print('traceback:', traceback)
            print('<--- Exiting from context manager!')
            return True


    with SampleContextManager():
        print('|||||||||Inside context manager! - Top')
        a = 8 / 0
        print('|||||||||Inside context manager! - Bottom')


    print('***FINISH***')

::

    ---> Entered into context manager!
    |||||||||Inside context manager! - Top
    exc_type: <class 'ZeroDivisionError'>
    exc_value: division by zero
    traceback: <traceback object at 0x7f4b3d520048>
    <--- Exiting from context manager!
    ***FINISH***

یادآوری:‌ می‌دانیم که خروجی هر تابع یا متد به صورت پیش‌فرض برای ``None`` می‌باشد و این مقدار در مقام ارزش‌سنجی بولین، ارزشی برابر با مقدار ``False`` دارد.

*در طی دروس آینده به مبحث Exception و مدیریت آن خواهیم پرداخت.*

 



|

----

:emoji-size:`😊` امیدوارم مفید بوده باشه




