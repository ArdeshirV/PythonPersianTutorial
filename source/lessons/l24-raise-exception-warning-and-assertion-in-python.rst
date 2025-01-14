.. role:: emoji-size

.. meta::
   :description: پایتون به پارسی - کتاب آنلاین و آزاد آموزش زبان برنامه‌نویسی پایتون - درس بیست و چهارم: مدیریت خطا در پایتون: Warning ،raise Exception و Assertion


.. _lesson-24: 

درس ۲۴: مدیریت خطا در پایتون: Warning ،raise Exception و Assertion
===================================================================================================

.. figure:: /_static/pages/24-python-raise-exception-warning-assertion.jpg
    :align: center
    :alt: مدیریت خطا در پایتون:Warning ،raise Exception و Assertion
    :class: page-image

    Photo by `Sandy Manoa <https://unsplash.com/photos/DnuC3-ZNBPQ>`__
  
  
این درس در ادامه درس پیش می‌باشد و به شرح مفاهیم باقی‌مانده پیرامون مفهوم Exception در زبان برنامه‌نویسی پایتون می‌پردازد. اینکه چگونه می‌توان با استفاده از دستور raise یک Exception را به صورت عمدی در برنامه بروز داد و همچنین چگونه می‌شود یک Exception در زبان برنامه‌نویسی پایتون ایجاد نماییم. در ادامه این درس به بررسی مفاهیم Warning و Assertion در زبان‌برنامه‌نویسی پایتون و نیز ارتباط آن‌ها با Exception می‌پردازد.


:emoji-size:`✔` سطح: متوسط

----


.. contents:: سرفصل‌ها
    :depth: 2

----


دستور ``raise``
~~~~~~~~~~~~~~~~~~~~~~~~~~~

از درس پیش با Exception آشنا شده‌ایم و مشاهده کردیم در زمان اجرای برنامه پایتونی (Runtime) تمامی خطاها در قالب یک Exception اعلام می‌گردند. اما در برنامه‌نویسی زمان‌های بسیاری خواهد بود که برنامه‌نویس می‌بایست خود اقدام به بروز Exception نماید. یک ماژول در هنگام انجام کار مشخصی ممکن است با وضعیت‌های مختلفی روبرو گردد که می‌بایست این وضعیت‌ها را به ماژول سطح بالاتر خود اعلام کند تا در نهایت نتیجه و توضیح مناسب برای کاربر فراهم گردد. برای مثال در پیاده‌سازی API ماژولی که انجام خدمت را به عهده دارد، هنگامی که به خطا یا وضعیتی  خاص برخورد می‌کند، می‌تواند این وضعیت را در قالب بروز یک Exception اعلام کند و ماژولی که وظیفه تولید پاسخ یا Response را برعهده دارد، بر اساس نوع Exception رخ داده می‌تواند یک Response مناسب تولید نماید.

در زبان برنامه‌نویسی پایتون از دستور ``raise`` [`اسناد پایتون <https://docs.python.org/3/reference/simple_stmts.html#raise>`__] برای بروز یک Exception استفاده می‌گردد::

    raise exception_object

به نمونه کد زیر توجه نمایید:

.. code-block:: python
    :linenos:
    
    def self_sum_int(a):
        if not isinstance(a, int):
            raise TypeError()
        
        return a + a

    res = self_sum_int('C')
    print(res)


::

    Traceback (most recent call last):
      File "sample.py", line 7, in <module>
        res = self_sum_int('C')
      File "sample.py", line 3, in self_sum_int
        raise TypeError()
    TypeError

در نمونه کد بالا ما یک شی از کلاس ``TypeError`` ایجاد و آن را raise کردیم (سطر ۳). همانطور که مشاهده می‌کنید، شرح Exception در Traceback (سطر پایانی) با آن چیزی که در درس پیش شاهد آن بودیم، متفاوت است و همچنین علت بروز Exception نیز raise شدن آن اعلام شده است. 

می‌توان در هنگام نمونه‌سازی از کلاس Exception مورد نظر، یک متن دلخواه (یک شی از نوع ``str``) به عنوان شرح Exception در زمان نمونه‌سازی به صورت آرگومان ارسال کنیم:


.. code-block:: python
    :linenos:
    
    def self_sum_int(a):
        if not isinstance(a, int):
            raise TypeError(f"The input must be 'int' type, {a!r} is {type(a)}")
        
        return a + a

    res = self_sum_int('C')
    print(res)


::

    Traceback (most recent call last):
      File "sample.py", line 7, in <module>
        res = self_sum_int('C')
      File "sample.py", line 3, in self_sum_int
        raise TypeError(f'The input must be of the integer type, {a} is {type(a)}')
    TypeError: The input must be 'int' type, 'C' is <class 'str'>


طی درس پیش مشاهده کردیم، چنانچه در زمان handle کردن یک Exception، یک Exception دیگر رخ دهد؛ در نتیجه Traceback نهایی نیز شامل یک Traceback به ازای هر Exception خواهد بود. این امکان نیز توسط دستور ``raise`` برای برنامه‌نویس فراهم می‌باشد. می‌توان با استفاده از دستور ``from`` در کنار  ``raise``،  دو Exception را به یکدیگر متصل و سپس raise کرد::

   raise exception_object from other_exception_object

به نمونه کد ساده زیر و خروجی آن توجه نمایید:

.. code-block:: python
    :linenos:
    
    def sum_int(a, b):
        try:
            return a + b
        except Exception as exception:
            raise RuntimeError("Something bad happened") from exception

    res = sum_int(3, 'C')
    print(res)

::

    Traceback (most recent call last):
      File "sample.py", line 3, in sum_int
        return a + b
    TypeError: unsupported operand type(s) for +: 'int' and 'str'

    The above exception was the direct cause of the following exception:

    Traceback (most recent call last):
      File "sample.py", line 7, in <module>
        res = sum_int(3, 'C')
      File "sample.py", line 5, in sum_int
        raise RuntimeError("Something bad happened") from exception
    RuntimeError: Something bad happened

به عنوان یک نمونه کاربرد، از این روش می‌توان برای ایجاد یک Wrapper برای چندین Exception بهره برد. در این حالت کد سطح بالاتر تنها نیاز است یک نوع Exception را handle نماید:

.. code-block:: python
    :linenos:
    
    def sum_int(a, b):
        try:
            return a + b
        except TypeError as type_err:
            raise RuntimeError(f'Something bad happened \n    => {str(type_err)}') from type_err



    try:
        res = sum_int(3, 'C')
        print(res)
    
    except RuntimeError as runtime_err:
        print(f'{runtime_err.__class__.__name__}: {str(runtime_err)}')

::

    RuntimeError: Something bad happened 
        => unsupported operand type(s) for +: 'int' and 'str'

ایجاد Exception
~~~~~~~~~~~~~~~~~~~~~~~~~~~

در زبان برنامه‌نویسی پایتون با ایجاد یک کلاس و ارث‌بری از ``Exception`` یا یکی از subclassهای آن می‌توان یک Exception جدید ایجاد نمود:

.. code-block:: python
    :linenos:
    
    class NegativeNumberError(Exception):
        """Raised when the input value is negative number"""
        pass


    def plus(num):
        if num < 0:
            raise NegativeNumberError(f'{num} is a negative number!')
            
        return num + num


    try:
        print(plus(10))
        print('*' * 30)
        print(plus(-5))
    
    except NegativeNumberError as err:
        print(str(err))
    
    except:
        print('Something bad happened!')
        
::

   20
   ******************************
   -5 is a negative number!

بدیهی است که می‌توان کلاس‌های Exception خود را مطابق با میل خود پیاده‌سازی نمود:

.. code-block:: python
    :linenos:
    
    class NegativeNumberError(Exception):
        """Raised when the input value is negative number"""
    
        def __init__(self, number, message="Number must be positive"):
            self.number = number
            self.message = message
            super().__init__(self.message)

        def __str__(self):
            return f'ERROR[{self.number}] -> {self.message}'


    def plus(num):
        if num < 0:
            raise NegativeNumberError(num)
            
        return num + num


    try:
        print(plus(10))
        print('*' * 30)
        print(plus(-5))
    
    except NegativeNumberError as err:
        print(str(err))
    
    except:
        print('Something bad happened!')
        
::

   20
   ******************************
   ERROR[-5] -> Number must be positive


.. note::
  در  زبان‌برنامه‌نویسی پایتون پیشنهاد می‌شود که اگر هدف از ایجاد Exception نمایش یک خطا باشد، در انتهای نام کلاس از واژه Error استفاده گردد.


ماژول warnings
~~~~~~~~~~~~~~~~~~~~~~~~~~~

تا این لحظه با مفهوم Exception آشنا شده‌ایم. می‌دانیم که بروز Exception در واقع اعلام یک خطا یا یک رویداد مهم در برنامه می‌باشد که می‌بایست حتما handle شود، در غیر این صورت برنامه قادر به انجام دستورات نخواهد بود.

اما گاهی اعلام یک رویداد آنقدر مهم نیست که بخواهد روند اجرای برنامه را تهدید کند. بلکه صرفا یک هشدار برای توجه بیشتر یا اصلاح رفتار برای نسخه‌های بعدی خواهد بود که **بیشتر کاربرد آن برای توسعه‌دهندگان برنامه می‌باشد تا کاربرانی که به نوعی مصرف‌کنندگان آن برنامه محسوب می‌شوند**. در زبان برنامه‌نویسی پایتون، ماژول ``warnings`` [`اسناد پایتون <https://docs.python.org/3/library/warnings.html>`__] برای استفاده در چنین زمان‌هایی فراهم آورده شده است [`PEP 230 <https://www.python.org/dev/peps/pep-0230>`__].


پیش از مراجعه به این ماژول از کتابخانه استاندارد زبان برنامه‌نویسی پایتون لازم است نگاهی دوباره به انتهای فهرست سلسله‌مراتب وراثت Exceptionها که در درس پیش آن را بررسی کردیم بیاندازیم، در انتهای این فهرست کلاس‌هایی با پسوند Warning قراردارند [`Exception hierarchy <https://docs.python.org/3/library/exceptions.html#exception-hierarchy>`__]:


.. image:: /_static/lessons/l24-python-exception-hierarchy-warnings.png
    :align: center
    :alt: Exception Hierarchy در پایتون به همراه warnings

همان‌طور که مشاهده می‌شود، تمام این کلاس‌ها از کلاسی با نام ``Warning`` ارث‌بری دارند که خود این کلاس نیز از کلاس ``Exception`` ارث‌بری دارد. 

این‌ها Warning هستند، Exceptionهایی که هدف از توسعه آنها اعلام یک هشدار می‌باشد و نه اعتراضی که تنبیه آن توقف برنامه باشد. با این حال به نمونه کد زیر توجه نمایید:

.. code-block:: python
    :linenos:

    def sum_int(a, b):
        raise DeprecationWarning('"sum_int" will be removed in version 2.0')
        sum = a + b
        print(sum)


    sum_int(6, 5)
    print('Done.')

::

    Traceback (most recent call last):
      File "sample.py", line 7, in <module>
        sum_int(6, 5)
      File "sample.py", line 2, in sum_int
        raise DeprecationWarning('"sum_int" will be removed in version 2.0')
    DeprecationWarning: "sum_int" will be removed in version 2.0

ساختار سلسله‌مراتب به ما گفته بود که Warningها در اصل Exception هستند (وجود رابطه IS-A به دلیل وراثت - درس هجدهم) و زمانی که یک Exception به اصطلاح raise شود، حتما می‌بایست یک handler برای آن پیش‌بینی شده باشد. در واقع اگر برای بروز یک Warning از دستور ``raise`` استفاده شود، دستور ``raise`` همان کاری را با Warning انجام می‌دهد که با هر نوع Exception دیگری انجام خواهد داد.


تابع ``warnings.warn``
---------------------------


اگر بخواهیم بروز یک Exception به صورتی هشدارگونه باشد، می‌بایست به سراغ ماژول ``warnings`` برویم. اکنون اگر نمونه کد قبل را با کمک این ماژول بازنویسی نماییم، نتیجه زیر حاصل می‌گردد:

.. code-block:: python
    :linenos:

    import warnings

    def sum_int(a, b):
        warnings.warn('"sum_int" will be removed in version 2.0', DeprecationWarning)
        sum = a + b
        print(sum)


    sum_int(6, 5)
    print('Done.')

::

    sample.py:4: DeprecationWarning: "sum_int" will be removed in version 2.0
      warnings.warn('"sum_int" will be removed in version 2.0', DeprecationWarning)
    11
    Done.

همان‌طور که مشاهده می‌شود تنها یک پیام هشدار در خروجی چاپ (print) می‌شود و دیگر خبری از Traceback نیست و برنامه بدون هیچ اخلالی باموفقیت تا خط پایان به اجرای خود ادامه داده است. 


برای اعلام یک هشدار از تابع ``warn`` در ماژول ``warnings`` استفاده می‌شود [`اسناد پایتون <https://docs.python.org/3/library/warnings.html#warnings.warn>`__] که تعریف آن به شکل زیر می‌باشد::

    warn(message, category=None, stacklevel=1, source=None)

بر اساس تعریف، این تابع یک پارامتر اجباری (``message``) و سه پارامتر اختیاری دارد.

* **message**: می‌بایست یک شی ``str`` باشد و متن هشداری است که می‌خواهیم نمایش داده شود.

* **category**: نوع Warning را مشخص می‌کند که می‌بایست **نام یک subclass از کلاس** ``Warning`` باشد. برای مشاهده انواع Warningهای از پیش آماده در پایتون می‌توانید به `Warning Categories <https://docs.python.org/3/library/warnings.html#warning-categories>`__ مراجعه نمایید. ارسال آرگومان برای این پارامتر اختیاری است و در صورت عدم ارسال، نوع ``UserWarning`` به صورت پیش‌فرض در نظر گرفته خواهد شد. 

* **stacklevel**: اگر دقت کرده باشید متن هشدار شامل اطلاعاتی از محل بروز آن می‌باشد. این پارامتر یک عدد از نوع ``int`` و بزرگتر یا مساوی از ``1`` را دریافت و تعیین می‌کند که این اطلاعات مربوط به کدام سطح از  فراخوانی کد و رسیدن به این هشدار باشد. به این صورت که: عدد ``1`` (مقدار پیش‌فرض) به محل دقیق بروز هشدار، عدد ``2`` به یک مرحله قبل‌تر از محل بروز هشدار و ...

  .. code-block:: python
      :linenos:


      import warnings

      def sum_int(a, b):
          print('-' * 30,  'stacklevel=1')
          warnings.warn('"sum_int" will be removed in version 2.0', stacklevel=1)
          print('-' * 30,  'stacklevel=2')
          warnings.warn('"sum_int" will be removed in version 2.0', stacklevel=2)
          print('-' * 30,  'stacklevel=3')
          warnings.warn('"sum_int" will be removed in version 2.0', stacklevel=3)
          print('-' * 30,  'stacklevel=4')
          warnings.warn('"sum_int" will be removed in version 2.0', stacklevel=4)
          print('-' * 30,  'stacklevel=5')
          warnings.warn('"sum_int" will be removed in version 2.0', stacklevel=5)
          print('-' * 30)
          sum = a + b
          print(sum)


      def action(a, b):
         sum_int(6, 5)


      action(6, 5)
      print('Done.')

  ::

      ------------------------------ stacklevel=1
      sample.py:5: UserWarning: "sum_int" will be removed in version 2.0
        warnings.warn('"sum_int" will be removed in version 2.0', stacklevel=1)
      ------------------------------ stacklevel=2
      sample.py:20: UserWarning: "sum_int" will be removed in version 2.0
        sum_int(6, 5)
      ------------------------------ stacklevel=3
      sample.py:23: UserWarning: "sum_int" will be removed in version 2.0
        action(6, 5)
      ------------------------------ stacklevel=4
      sys:1: UserWarning: "sum_int" will be removed in version 2.0
      ------------------------------ stacklevel=5
      ------------------------------
      11
      Done.

Warnings Filter
----------------------

حالتی را تصور کنید که برنامه شما پر از Warningهای متنوع می‌باشد. Warnings Filter امکانی است برای اینکه مشخص کنیم کدام نوع Warning نادیده گرفته شود یا کدام نوع نمایش داده شود یا کدام نوع همچون یک Exception واقعی رفتار کند. برای این منظور از از تابع ``simplefilter`` در ماژول ``warnings`` استفاده می‌شود [`اسناد پایتون <https://docs.python.org/3/library/warnings.html#warnings.simplefilter>`__] که تعریف آن به شکل زیر می‌باشد::

    simplefilter(action, category=Warning, lineno=0, append=False)

بر اساس تعریف، این تابع یک پارامتر اجباری (``action``) و سه پارامتر اختیاری دارد.


* **action**: از نوع ``str`` بوده و می‌تواند یکی از مقادیر پایین باشد. این مشخص می‌کند که چه عملیاتی می‌بایست بر روی Warningها اعمال شود:

  .. container:: table

	  ======================  ===================================================================
	  مقدار                   توضیحات
	  ======================  ===================================================================
	  ``'default'``           حالت پیش‌فرض، هر Warning به ازای سطری که در آن قرار دارد یکبار چاپ شود
	  ``'error'``             تبدیل رفتار Warning به Exception واقعی - بروز خطا
	  ``'ignore'``            نادیده گرفتن Warning
	  ``'always'``            Warning هر بار چاپ شود
	  ``'module'``            هر Warning به ازای هر ماژول تنها یکبار چاپ شود
	  ``'once'``              هر Warning به ازای کل برنامه تنها یکبار چاپ شود
	  ======================  ===================================================================

* **category**: نوع Warning را مشخص می‌کند که می‌بایست **نام یک subclass از کلاس** ``Warning`` باشد. ارسال آرگومان برای این پارامتر اختیاری است و در صورت عدم ارسال، عمل مشخص شده توسط پارامتر action برای تمام انواع Warningها در برنامه اعمال می‌گردد. 

به نمونه کدهای زیر توجه نمایید:

.. code-block:: python
    :linenos:

    import warnings
    warnings.simplefilter('ignore')
    # $ python3 -Wi sample.py
    # $ python3 -Wignore sample.py


    print('-------Before #01-------')
    warnings.warn('#01')
    print('-------After  #01-------')

::

    -------Before #01-------
    -------After  #01-------


.. code-block:: python
    :linenos:

    import warnings
    warnings.simplefilter('ignore', DeprecationWarning)
    # $ python3 -Wignore::DeprecationWarning sample.py
    # $ python3 -Wi::DeprecationWarning sample.py


    print('-------Before #02-------')
    warnings.warn('#02')
    print('-------After  #02-------')

    print('-------Before #03-------')
    warnings.warn('#03', DeprecationWarning)
    print('-------After  #03-------')

::

    -------Before #02-------
    sample.py:8: UserWarning: #02
      warnings.warn('#02')
    -------After  #02-------
    -------Before #03-------
    -------After  #03-------


.. code-block:: python
    :linenos:

    import warnings
    warnings.simplefilter('error')
    # $ python3 -We sample.py
    # $ python3 -Werror sample.py


    print('-------Before #04-------')
    warnings.warn('#04')
    print('-------After  #04-------')


::

      -------Before #04-------
      Traceback (most recent call last):
        File "sample.py", line 8, in <module>
          warnings.warn('#04')
      UserWarning: #04


.. tip:: 

   اعمال Filter در زمان اجرای اسکریپت نیز با استفاده از کلید ``W-`` ممکن می‌باشد [`اسناد پایتون <https://docs.python.org/3/using/cmdline.html#cmdoption-w>`__] که در هر نمونه کد، معادل دستور اجرای پایتون نیز به صورت کامنت درج شده است.


.. tip:: 

  همانند Exceptionها می‌توانید انواع Warning خود را ایجاد نمایید. برای این منظور تنها کافی است یک کلاس ایجاد نمایید که از کلاس ``Warning`` یا یکی از subclassهای آن ارث‌بری داشته باشد.

.. note:: 

  این بخش به دلیل وابستگی مبحث Warning با مبحث مهم Exception در زبان‌برنامه‌نویسی پایتون و صرفا به منظور آشنایی خوانندگان با همچنین قابلیتی در این زبان تهیه شده است. ماژول ``warnings`` امکانات گسترده‌تری را فراهم می‌آورد که پرداختن به تمام آن‌ها خارج از حوصله این درس می‌بود، بنابراین علاقه‌مندان برای مطالعه بیشتر می‌توانند به مستندات رسمی پایتون مراجعه نمایند.



دستور ``assert``
~~~~~~~~~~~~~~~~~~~~~~~~~~~

ادعا یا Assertion در برنامه‌نویسی به عبارت‌های ساده از شرط‌های بولی گفته می‌شود که درستی یک «وضعیت» یا یک «حقیقت» در کد را بررسی می‌کنند. باید توجه داشت Assertion در واقع یک ابزار برای کمک به توسعه برنامه می‌باشد که کاربرد آن در ایجاد تست کد در زمان تست‌نویسی و دیباگ (Debug) برنامه در محیط توسعه می‌باشد و نه در محیط اجرای برنامه به عنوان محصول.


فلوچارت یک Assertion به صورت زیر ترسیم می‌شود:

.. image:: /_static/lessons/l24-python-assertion-flowchart.png
    :align: center
    :width: 450
    :alt: دستور ``assert`` در پایتون - فلوچارت Assertion


در زبان برنامه‌نویسی پایتون Assertion با استفاده از دستور ``assert`` پیاده‌سازی می‌گردد [`اسناد پایتون <https://docs.python.org/3/reference/simple_stmts.html#the-assert-statement>`__] و با یکی از دو سینتکس زیر قابل پیاده‌سازی می‌باشد::

    assert condition_expression 

::

    assert condition_expression, 'error_message'


به نمونه کد زیر توجه نمایید:

.. code-block:: python
    :linenos:

    def average(numbers):
        assert len(numbers) != 0
        return sum(numbers)/len(numbers)

    numbers = [1, 2, 3, 4, 5]
    print(f'Average of {numbers}: {average(numbers)}')

    print('-' * 30)

    numbers = []
    print(f'Average of {numbers}: {average(numbers)}')

::

    Average of [1, 2, 3, 4, 5]: 3.0
    ------------------------------
    Traceback (most recent call last):
      File "sample.py", line 11, in <module>
        print(f'Average of {numbers}: {average(numbers)}')
      File "sample.py", line 2, in average
        assert len(numbers) != 0
    AssertionError


فرض توسعه‌دهنده تابع ``average`` مثال قبل این بوده که به این تابع داده‌ای با طول صفر ارسال نمی‌گردد، ولی اگر در زمان تست یا ادامه مراحل توسعه برنامه این مقدار ارسال گردد، باید یک فکری برای اصلاح آن کرد! چرا که این تابع آمادگی کافی برای تبدیل شدن به یک باگ در برنامه را دارد!

می‌توان برای دستور ``assert`` یک پیام خطا نیز اختصاص داد:


.. code-block:: python
    :linenos:

    def average(numbers):
        assert len(numbers) != 0, 'List[numbers] is empty.'
        return sum(numbers)/len(numbers)

    numbers = []
    print(f'Average of {numbers}: {average(numbers)}')

::

    Traceback (most recent call last):
      File "sample.py", line 6, in <module>
        print(f'Average of {numbers}: {average(numbers)}')
      File "sample.py", line 2, in average
        assert len(numbers) != 0, 'List[numbers] is empty.'
    AssertionError: List[numbers] is empty.


همانطور پیش‌تر بیان شده دستورهای ``assert`` یک قابلیت برای زمان توسعه می‌باشند بنابراین باید توجه داشت که تمامی این دستورات هنگامی که برنامه با کلید بهینه‌سازی (Optimization - درس چهارم) یعنی ``O-`` یا ``OO-`` اجرا گردد، در زمان کامپیال حذف و در بایت‌کد قرار نخواهند گرفت::

    $ python -O script.py


این شرایط مشابه حالتی است که بجای دستور ``assert``، مستقیم از دستور ``raise`` به شکل زیر استفاده نماییم::

    if __debug__:
        if not condition_expression: raise AssertionError()

::

    if __debug__:
        if not condition_expression: raise AssertionError('error_message')

``__debug__`` یک متغیر داخلی در محیط اجرای پایتون با مقدار پیش‌فرض ``True`` می‌باشد [`اسناد پایتون <https://docs.python.org/3/library/constants.html#__debug__>`__]. مقدار این متغیر در تمام طول مدت اجرای برنامه ثابت خواهد بود و تنها زمانی که برنامه با کلید بهینه‌سازی اجرا گردد، مقدار آن به ``False`` تغییر می‌یابد. بنابراین دستور ``raise AssertionError`` هیچگاه اجرا نخواهد شد.


همچنین نباید فراموش کرد که ``AssertionError`` یکی از Exceptionهای آماده پایتون می‌باشد [`اسناد پایتون <https://docs.python.org/3/library/exceptions.html#AssertionError>`__]. بنابراین هنگام بروز ممکن است توسط دستور ``try``، به صورت ناخواسته handle شود:

.. code-block:: python
    :linenos:

    def average(numbers):
        assert len(numbers) != 0, 'List[numbers] is empty.'
        return sum(numbers)/len(numbers)

    try:

        numbers = []
        print(f'Average of {numbers}: {average(numbers)}')

    except Exception as err: # or except:
        print('Something bad happened!')

::

    Something bad happened!



|

----

:emoji-size:`😊` امیدوارم مفید بوده باشه



