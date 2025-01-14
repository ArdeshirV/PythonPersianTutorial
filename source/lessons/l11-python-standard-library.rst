.. role:: emoji-size

.. meta::
   :description: پایتون به پارسی - کتاب آنلاین و آزاد آموزش زبان برنامه‌نویسی پایتون - درس یازدهم: کتابخانه استاندارد پایتون


.. _lesson-11: 

درس ۱۱: کتابخانه استاندارد پایتون
============================================================================

.. figure:: /_static/pages/11-python-os-path-math.jpg
    :align: center
    :alt: کتابخانه استاندارد پایتون: math و os
    :class: page-image

    Photo by `Yousef Espanioly <https://unsplash.com/photos/L6g30JaQ5Tc>`__


کتابخانه استاندارد پایتون مجموعه‌ وسیعی از امکانات آماده است که با نصب بسته نرم‌افزاری پایتون (درس دوم) در اختیار قرار می‌گیرد. تمام تابع‌ها و ماژول‌هایی که تاکنون با آن آشنا شده‌ایم، بخشی از این کتابخانه هستند. فهرست کامل ابزارهای ارایه شده توسط این کتابخانه را می‌توانید از نشانی‌ [`The Python Standard Library <https://docs.python.org/3/library/>`_] مشاهده نمایید. 

لازم به یادآوری است که بخشی بزرگی از قدرت پایتون به دلیل وجود کتابخانه‌های فراوان و قدرتمند آن است که تعداد زیادی از آن‌ها خارج کتابخانه استاندارد پایتون و درون جامعه کاربری در حال توسعه هستند که فهرست تقریبا کاملی از آن‌ها نیز توسط `PyPI <https://pypi.python.org/pypi>`_ قابل جستجو و دریافت هستند.


این درس به عنوان آخرین درس از سطح مقدماتی کتاب به بررسی بخشی از امکان‌های کاربردی این کتابخانه اختصاص یافته است که البته ممکن است در طول درس‌های گذشته از آن‌ها استفاده کرده باشیم!. پیش‌تر کمی با ماژول ``sys`` آشنا شده‌ایم، در این درس به بررسی سه ماژول کاربردی دیگر خواهیم پرداخت. ماژول‌های مهم دیگری نیز طی دروس آینده بررسی خواهند شد (مانند: ``re`` و ``datetime``).



:emoji-size:`✔` سطح: مقدماتی

----


.. contents:: سرفصل‌ها
    :depth: 2

----

.. _python-math: 

math
------
این ماژول حاوی ثابت‌ها (Constants) و تابع‌های ریاضی است [`اسناد پایتون <https://docs.python.org/3/library/math.html>`__] که برخی از آن‌ها به شرح پایین است:

* ``math.pi``: ثابتی حاوی عدد π (`ویکی‌پدیا <https://en.wikipedia.org/wiki/Pi>`__) است [`اسناد پایتون <http://docs.python.org/3/library/math.html#math.pi>`__]::

    >>> import math

    >>> math.pi
    3.141592653589793
    >>> 

* ``math.e``: ثابتی حاوی عدد e (`ویکی‌پدیا <https://en.wikipedia.org/wiki/E_(mathematical_constant)>`__) است [`اسناد پایتون <http://docs.python.org/3/library/math.html#math.e>`__]::

    >>> import math

    >>> math.e
    2.718281828459045
    >>> 

* ``math.inf``: (از نسخه 3.5 به بعد) - ثابتی حاوی مقدار مثبت بی‌نهایت (Positive infinity) است که این مقدار برابر با خروجی تابع ``('float('inf`` می‌باشد. ``math.inf -`` نیز برابر منفی بی‌نهایت است [`اسناد پایتون <https://docs.python.org/3/library/math.html#math.inf>`__].

  برای بررسی inf بودن (مثبت یا منفی) از تابع ``(math.isinf(x`` [`اسناد پایتون <http://docs.python.org/3/library/math.html#math.isinf>`__] استفاده می‌شود::

      >>> import math

      >>> a = math.inf
      >>> b = 10
      >>> a > b
      True

      >>> math.inf + math.inf
      inf
      >>> 1 / math.inf
      0.0
      >>> math.inf / 2
      inf
      >>> 3 * math.inf
      inf
      >>> -3 * math.inf
      -inf

      >>> math.isinf(a)
      True
      >>> math.isinf(b)
      False
      >>> 

* ``math.nan``: از نسخه 3.5 به بعد - ثابتی حاوی مقدار «تعریف نشده» یا NaN - اختصار Not a Number (`ویکی‌پدیا <https://en.wikipedia.org/wiki/NaN>`__) - می‌باشد که این مقدار برابر با خروجی تابع ``('float('nan`` است [`اسناد پایتون <https://docs.python.org/3/library/math.html#math.nan>`__].

  برای بررسی nan بودن از تابع ``(math.isnan(x`` [`اسناد پایتون <http://docs.python.org/3/library/math.html#math.isnan>`__] استفاده می‌شود::

      >>> import math

      >>> a = math.nan
      >>> a
      nan

      >>> 0 * math.inf
      nan
      >>> math.inf - math.inf
      nan

      >>> math.isnan(a)
      True
      >>>


* ``(math.ceil(x``: کوچکترین عدد صحیحی که بزرگتر یا مساوی با عدد ``x`` باشد را برمی‌گرداند [`اسناد پایتون <https://docs.python.org/3/library/math.html#math.ceil>`__]::

    >>> import math

    >>> math.ceil(4)
    4
    >>> math.ceil(-4.17)
    -4
    >>> math.ceil(4.17)
    5
    >>> 

* ``(math.floor(x``: بزرگترین عدد صحیحی که کوچکتر یا مساوی با عدد ``x`` باشد را برمی‌گرداند [`اسناد پایتون <https://docs.python.org/3/library/math.html#math.floor>`__]::

    >>> import math

    >>> math.floor(4)
    4
    >>> math.floor(-4.17)
    -5
    >>> math.floor(4.17)
    4
    >>> 

* ``(math.fabs(x``: همانند تابع آماده ``()abs`` [`اسناد پایتون <http://docs.python.org/3/library/functions.html#abs>`__] مقدار قدر مطلق (`ویکی‌پدیا <https://en.wikipedia.org/wiki/Absolute_value>`__) عدد ``x`` را برمی‌گرداند [`اسناد پایتون <https://docs.python.org/3/library/math.html#math.fabs>`__].

 تابع آماده ``abs`` بدون نیاز به import همواره قابل استفاده است و خروجی آن بر اساس نوع داده ورودی می‌تواند صحیح یا ممیز شناور باشد. ولی 
 تابع ``(math.fabs(x`` برای کار با داده های float طراحی شده است و خروجی آن همواره یک عدد ممیز شناور است::

    >>> import math

    >>> math.fabs(-4.17)
    4.17
    >>> math.fabs(-4)
    4.0
    >>> math.fabs(4)
    4.0
    >>> 

* ``(math.factorial(x``: مقدار فاکتوریل (`ویکی‌پدیا <https://en.wikipedia.org/wiki/Factorial>`__) عدد x را برمی‌گرداند [`اسناد پایتون <http://docs.python.org/3/library/math.html#math.factorial>`__]::

    >>> import math

    >>> math.factorial(5)
    120
    >>>

* ``(math.exp(x``: حاصل ``e**x`` (`ویکی‌پدیا <https://en.wikipedia.org/wiki/Exponential_function>`__) را برمی‌گرداند [`اسناد پایتون <http://docs.python.org/3/library/math.html#math.exp>`__]::

    >>> import math

    >>> math.exp(3)
    20.085536923187668
    >>> 

* ``(math.log(x[, base]``: حاصل لگاریتم (Logarithm) عدد x در پایه base را برمی‌گرداند؛ آرگومان base اختیاری است و چنانچه ذکر نگردد به صورت پیش‌فرض حاصل لگاریتم عدد x در پایه عدد e یا همان لگاریتم طبیعی (`ویکی‌پدیا <https://en.wikipedia.org/wiki/Natural_logarithm>`__) برگردانده می‌شود [`اسناد پایتون <http://docs.python.org/3/library/math.html#math.log>`__]::

    >>> import math

    >>> math.log(math.e)     # ln e == 1
    1.0
    >>> math.log(1)          # ln 1 == 0
    0.0
    >>>

  ::
      
      >>> math.log(8, 2)       # 2**3 == 8
      3.0
      >>> math.log(100, 10)    # 10**2 == 100
      2.0
      >>> math.log(81, 3)      # 3**4 == 81
      4.0
      >>> math.log(2, 10)
      0.30102999566398114
      >>> 

  برای سادگی استفاده در محاسبه‌های ریاضی دو تابع ``(log10(x`` [`اسناد پایتون <http://docs.python.org/3/library/math.html#math.log10>`__] - محاسبه لگاریتم عدد x در پایه عدد 10 - و ``(log2(x`` [`اسناد پایتون <http://docs.python.org/3/library/math.html#math.log2>`__] - محاسبه لگاریتم عدد x در پایه عدد 2؛ که از **نسخه 3.3** به بعد اضافه شده است - نیز در دسترس هستند::

      >>> math.log10(100)
      2.0
      >>> math.log2(8)
      3.0
      >>> 


* ``(math.sqrt(x``:  ریشه دوم (Square root) یا همان جذر (`ویکی‌پدیا <https://en.wikipedia.org/wiki/Square_root>`__)‌ عدد x را برمی‌گرداند [`اسناد پایتون <http://docs.python.org/3/library/math.html#math.sqrt>`__]::


    >>> import math

    >>> math.sqrt(4)
    2.0
    >>>

* ``(math.pow(x, y``: عدد x را به توان عدد y می‌رساند و حاصل را برمی‌گرداند [`اسناد پایتون <http://docs.python.org/3/library/math.html#math.pow>`__]::

    >>> import math

    >>> math.pow(3, 2)
    9.0

  این تابع هر دو آرگومان خود را به نوع float تبدیل می‌کند؛ چنانچه می‌خواهید با اعداد صحیح کار کنید، از عملگر ``**`` یا تابع آماده ``()pow`` [`اسناد پایتون <http://docs.python.org/3/library/functions.html#pow>`__] استفاده نمایید::

    >>> 3**2
    9
    >>> pow(3, 2)
    9


* توابع مثلثاتی (Trigonometric functions) [`اسناد پایتون <http://docs.python.org/3/library/math.html#trigonometric-functions>`__]:  ``(cos(x`` و ``(sin(x`` و ``(tan(x`` و ``(acos(x`` و ``(asin(x`` و ``(atan(x`` که در تمام آن‌ها زاویه x بر حسب **رادیان (Radian)** است::

    >>> import math

    >>> math.cos(0)
    1.0
    >>> math.sin(0)
    0.0
    >>> math.tan(0)
    0.0
    >>> 

* ``(math.degrees(x``: زاویه x را از رادیان به **درجه** تبدیل می‌کند [`اسناد پایتون <http://docs.python.org/3/library/math.html#math.degrees>`__]::

    >>> import math

    >>> math.degrees(0)
    0.0

* ``(math.radians(x``: زاویه x را از درجه به **رادیان** تبدیل می‌کند [`اسناد پایتون <http://docs.python.org/3/library/math.html#math.radians>`__]::

    >>> import math

    >>> math.degrees(0)
    0.0
    >>> math.radians(30)
    0.5235987755982988

  ::

      >>> math.sin(math.radians(90))
      1.0

* توابع هذلولی (Hyperbolic functions) [`اسناد پایتون <http://docs.python.org/3/library/math.html#hyperbolic-function>`__]:  ``(cosh(x`` و ``(sinh(x`` و ``(tanh(x`` و ``(acosh(x`` و ``(asinh(x`` و ``(atanh(x``.


.. _python-os: 

os
-----
این ماژول امکان استفاده از برخی قابلیت‌های وابسته به سیستم عامل را فراهم می‌آورد؛ مانند گرفتن مسیر دایرکتوری برنامه [`اسناد پایتون <http://docs.python.org/3/library/os.html>`_]. برخی از تابع‌های موجود در این ماژول به شرح پایین است:

* ``os.environ``: یک شی از نوع نگاشت - مانند نوع دیکشنری [به درس هشتم رجوع شود] - است که حاوی متغیرهای محیطی سیستم عامل می‌باشد [`اسناد پایتون <http://docs.python.org/3/library/os.html#os.environ>`__]

  باید توجه داشت که مقدار این دستور متناسب با لحظه‌ای از سیستم عامل است که ماژول ``os`` به اسکریپت import شده است و شامل متغیرهایی که پس از این لحظه ایجاد شده باشند نمی‌شود.

  ::


    >>> # Python 3.x, GNU/Linux

    >>> import os
    >>> os.environ
    environ({'LOGNAME': 'saeid', 'PWD': '/home/saeid', '_': '/usr/bin/python3', 'LANG': 'en_US.UTF-8', 'PATH': '/usr/local/sbin:/usr/local/bin:/usr/bin', 'ZSH': '/home/saeid/.oh-my-zsh'})
    >>> 

  ::

      >>> os.environ['PATH']
      '/usr/local/sbin:/usr/local/bin:/usr/bin'

      >>> os.environ['LANG']
      'en_US.UTF-8'


* ``()os.getcwd``: مسیر دایرکتوری جاری (Current Working Directory)‌ را برمی‌گرداند. خروجی این تابع برابر با دستور ``pwd`` در خط فرمان گنولینوکس یا ``%echo %CD`` در خط فرمان ویندوز می‌باشد. [`اسناد پایتون <http://docs.python.org/3/library/os.html#os.getcwd>`__]::

    # Python 3.x, GNU/Linux

    ~ pwd
    /home/saeid

 ::

    ~ python3 -q 
    >>> import os
    >>> os.getcwd()
    '/home/saeid'
    >>>


* ``(os.chdir(path``: مسیر دایرکتوری جاری را به مسیر آرگومان دریافتی path تغییر می‌دهد. عملکرد این تابع برابر با دستور ``cd`` در خط فرمان‌های گنولینوکس و ویندوز است. [`اسناد پایتون <http://docs.python.org/3/library/os.html#os.chdir>`__]::

    >>> import os

    >>> os.getcwd()
    '/home/saeid'

    >>> os.chdir('/etc')

    >>> os.getcwd()
    '/etc'

* ``(os.listdir(path``: یک شی لیست که شامل محتویات درون دایرکتوری path است را برمی‌گرداند. چنانچه آرگومان path ارسال نشود به صورت پیش‌فرض مسیر دایرکتوری جاری در نظر گرفته می‌شود. [`اسناد پایتون <http://docs.python.org/3/library/os.html#os.listdir>`__] ::

    >>> import os
    >>> os.listdir('/home/saeid/Pictures')
    ['scan0001.jpg', 'smplayer_screenshots', 'GNU.png', 'Wallpapers']


* ``(os.mkdir(path``: یک دایرکتوری که نام کامل آن توسط آرگومان path تعیین شده است را ایجاد می‌کند. در صورتی که این دایرکتوری از قبل موجود باشد یک استثنا ``FileExistsError`` رخ می‌دهد. [`اسناد پایتون <http://docs.python.org/3/library/os.html#os.mkdir>`__]::

    >>> import os
    >>> os.mkdir('dir1')

  در نمونه کد بالا از آنجا که مسیر دایرکتوری ذکر نشده است؛ دایرکتوری dir1 به صورت پبش فرض در مسیر دایرکتوری جاری (که در اینجا: ``/home/saeid/`` است) ایجاد می‌گردد؛ همین امر باعث بروز استثنا با اجرای دستور پایین می‌شود::

      >>> os.mkdir('/home/saeid/dir1')
      Traceback (most recent call last):
        File "<stdin>", line 1, in <module>
      FileExistsError: [Errno 17] File exists: '/home/saeid/dir1'



  ::

    >>> os.mkdir('/home/saeid/Documents/dir2')

  *نمونه کد بالا موجب ایجاد دایرکتوری dir2 درون مسیر دایرکتوری Documents می‌شود.*

  مسیر دایرکتوری می‌بایست به صورت صحیح وارد شود؛ در نمونه کد پایین نیز به همین دلیل که دایرکتوری dir3 وجود ندارد، استثنایی رخ داده است.

  ::

      >>> os.mkdir('/home/saeid/Documents/dir3/dir4')
      Traceback (most recent call last):
        File "<stdin>", line 1, in <module>
      FileNotFoundError: [Errno 2] No such file or directory: '/home/saeid/Documents/dir3/dir4'


* ``(os.makedirs(path``: همانند ``(os.mkdir(path`` است ولی با این تفاوت که تمامی دایرکتوری‌های میانی مورد نیاز را هم ایجاد می‌کند. [`اسناد پایتون <http://docs.python.org/3/library/os.html#os.makedirs>`__]

  *در نمونه کد پایین برای ایجاد دایرکتوری dir5 دایرکتوری‌های dir3 و dir4 - که البته وجود ندارند - نیز ایجاد می‌گردند.*

  ::

    >>> import os
    >>> os.makedirs('/home/saeid/Documents/dir3/dir4/dir5')

* ``(os.rmdir(path``: دایرکتوری مشخص شده توسط آرگومان path را حذف می‌کند. این دایرکتوری می‌بایست خالی باشد در غیر این صورت یک استثنا ``OSError`` رخ می‌دهد. [`اسناد پایتون <http://docs.python.org/3/library/os.html#os.rmdir>`__]


  البته برای حذف کامل یک دایرکتوری به همراه تمام محتویات آن می‌توانید از تابع ``(rmtree(path`` درون ماژول ``shutil`` [`اسناد پایتون <http://docs.python.org/3/library/shutil.html#shutil.rmtree>`__] استفاده نمایید::

    >>> import shutil
    >>> shutil.rmtree("/home/saeid/Documents/dir1")


* ``(os.removedirs(path``: همانند ``(os.rmdir(path`` است ولی با این تفاوت که عملکردی بازگشتی دارد و تا زمانی که خطایی رخ نداده دایرکتوری‌های مشخص شده در آرگومان path را یکی یکی حذف می‌کند. [`اسناد پایتون <http://docs.python.org/3/library/os.html#os.removedirs>`__] ::

    >>> import os
    >>> os.removedirs('/home/dir1/dir2/dir3')

  در نمونه کد بالا ابتدا دایرکتوری dir3 (با مسیر ``'home/dir1/dir2/dir3/'``) حذف می‌شود - البته اگر خالی باشد - و بعد از آن برای حذف دایرکتوری dir2 (با مسیر ``'home/dir1/dir2/'``) تلاش می‌شود که اگر آن‌هم خالی باشد و حذف گردد، روند حذف به همین شکل برای باقی مسیر ادامه می‌یابد.

* ``(os.rename(src, dst``: این تابع برای تغییر نام یک فایل یا دایرکتوری کاربرد دارد. آرگومان ``src`` نام اصلی و آرگومان ``dst`` نیز نام جدید برای فایل یا دایرکتوری مورد نظر می‌باشند [`اسناد پایتون <http://docs.python.org/3/library/os.html#os.rename>`__]::

    >>> import os
    >>> os.getcwd()
    '/home/saeid/Documents/dir'
    >>> os.listdir(os.getcwd())
    ['fontsdir', 'index.html', 'style.css']

    >>> os.rename("fontsdir", "_fonts")

    >>> os.listdir(os.getcwd())
    ['index.html', 'style.css', '_fonts']

  توجه داشته باشید چنانچه فایل یا دایرکتوری موردنظر در مسیری دیگری از مسیر دایرکتوری جاری باشد؛ لازم است نام به شکل کامل (همراه با مسیر) ذکر گردد. همچنین بدیهی است که تغییر مسیر در آرگومان ``dst`` موجب عمل انتقال (Move) می‌شود::

    >>> import os
    >>> os.getcwd()
    '/home/saeid/Documents/dir/dir1'
    >>> os.listdir(os.getcwd())
    ['index.html', 'style.css', '_fonts']

    >>> os.rename("_fonts", "/home/saeid/Documents/dir/dir2/_fonts")

    >>> os.listdir(os.getcwd())
    ['index.html', 'style.css']

    >>> os.chdir('/home/saeid/Documents/dir/dir2')
    >>> os.listdir(os.getcwd())
    ['_fonts']

  در گنولینوکس چنانچه بخواهیم نام **فایلی** به یک نام از پیش موجود تغییر داده شود؛‌ [در صورتی که کاربر نیز اجازه دسترسی (Permission) لازم را داشته باشد] یک عمل جایگزینی (Replace) صورت می‌گیرد، ولی برای چنین مواقعی در سیستم عامل ویندوز یک خطای ``OSError`` رخ خواهد داد. رویداد این ماجرا در هنگام تغییر نام یک **دایرکتوری**، باعث بروز خطای ``OSError`` در هر دو سیستم عامل می‌شود.


* ``(os.renames(old, new``: عملکردی مشابه با تابع ``()rename`` دارد با این تفاوت که اگر دایرکتورهای میانی از مسیر آرگومان ``new``، وجود نداشته باشند، آن‌ها را نیز ایجاد می‌کند [`اسناد پایتون <http://docs.python.org/3/library/os.html#os.renames>`__]::

    >>> import os
    >>> os.getcwd()
    '/home/saeid/Documents/dir'
    >>> os.listdir(os.getcwd())
    ['index.html', 'style.css', '_fonts', 'js']

    >>> os.renames("style.css", "css/style.css")

    >>> os.listdir(os.getcwd())
    ['index.html', 'css', '_fonts', 'js']


* ``(os.walk(rootdirpath``: مسیر یک دایرکتوری را به عنوان دایرکتوری ریشه پیمایش می‌کند و مسیر هر دایرکتوری را که می‌بیند به همراه نام دایرکتوری‌ها و فایل‌های درون آن برمی‌گرداند. [`اسناد پایتون <http://docs.python.org/3/library/os.html#os.walk>`__]::

    dir1
    ├── dir2
    │   └── file21
    ├── file11
    └── file12

  ::

      >>> import os

      >>> tuple(os.walk('/home/saeid/Documents/dir1'))
      (('/home/saeid/Documents/dir1', ['dir2'], ['file12', 'file11']), ('/home/saeid/Documents/dir1/dir2', [], ['file21']))


  ::

      >>> import os

      >>> for root, dirs, files in os.walk('/home/saeid/Documents/dir1'):
      ...     print('Found directory: {}'.format(root))
      ...     for filename in files:
      ...         print('\t{}'.format(filename))
      ... 
      Found directory: /home/saeid/Documents/dir1
      	file12
      	file11
      Found directory: /home/saeid/Documents/dir1/dir2
      	file21
      >>> 

  جهت پیمایش دایرکتوری‌ها به صورت پیش‌فرض از بالا (دایرکتوری ریشه) به پایین است که می‌توان با ``False`` قرار دادن آرگومان اختیاری ``topdown`` آن را معکوس نمود::

    >>> for root, dirs, files in os.walk('/home/saeid/Documents/dir1', topdown=False):
    ...     print('Found directory: {}'.format(root))
    ...     for filename in files:
    ...         print('\t{}'.format(filename))
    ... 
    Found directory: /home/saeid/Documents/dir1/dir2
    	file21
    Found directory: /home/saeid/Documents/dir1
    	file12
    	file11
    >>> 


* ``os.sep``: این متغیر حاوی کاراکتری می‌باشد که سیستم‌عامل از آن برای جدا سازی اجزای یک مسیر استفاده می‌کند. مانند: ``/`` در گنولینوکس یا ``\\`` در ویندوز [`اسناد پایتون <https://docs.python.org/3/library/os.html#os.sep>`__]


* ``os.extsep``: این متغیر حاوی کاراکتری می‌باشد که در سیستم‌عامل جاری از آن برای جدا سازی نام فایل از پسوند آن استفاده می‌گردد. مانند: ``.`` (نام فایل: script.py) [`اسناد پایتون <https://docs.python.org/3/library/os.html#os.extsep>`__]


* ``os.pardir``: حاوی مقداری است که در سیستم‌عامل جاری از آن برای اشاره به یک دایرکتوری بالاتر از دایرکتوری جاری استفاده می‌گردد (Parent Directory). مانند: ``..`` در گنولینوکس و ویندوز [`اسناد پایتون <https://docs.python.org/3/library/os.html#os.pardir>`__]::

    # GNU/Linux

    ~ pwd
    /home/saeid/Documents

    ~ cd ..

    ~ pwd
    /home/saeid


* ``os.curdir``: حاوی مقداری است که در سیستم‌عامل جاری از آن برای اشاره به دایرکتوری جاری استفاده می‌گردد (Current Directory). مانند: ``.`` در گنولینوکس و ویندوز [`اسناد پایتون <https://docs.python.org/3/library/os.html#os.curdir>`__]::


    # GNU/Linux

    ~ pwd
    /home/saeid

    ~ cd .

    ~ pwd
    /home/saeid

    ~ cd ./..

    ~ pwd
    /home 


.. _python-os-path: 

os.path
--------

این ماژول توابعی مفیدی برای کار با مسیر فایل‌ها و دایرکتوری‌ها پیاده‌سازی کرده است [`اسناد پایتون <https://docs.python.org/3/library/os.path.html>`__]. 


.. caution::
    برای خواندن و نوشتن فایل‌ها از ``()open`` و برای دسترسی به سیستم‌فایل از ماژول ``os`` استفاده نمایید.



* ``(os.path.split(path``: مسیر path دریافتی را به یک توپِل (dirname, basename) تجزیه می‌کند که در آن **basename** آخرین بخش از مسیر path و **dirname** نیز هر آنچه قبل از basename باشد، خواهند بود [`اسناد پایتون <https://docs.python.org/3/library/os.path.html#os.path.split>`__]::


    >>> import os.path

    >>> for path in [ '/one/two/three', 
    ...               '/one/two/three/',
    ...               '/',
    ...               '.',
    ...               '']:
    ...     print ('"%s" : "%s"' % (path, os.path.split(path)))
    ... 
    "/one/two/three" : "('/one/two', 'three')"
    "/one/two/three/" : "('/one/two/three', '')"
    "/" : "('/', '')"
    "." : "('', '.')"
    "" : "('', '')"
    >>>


* ``(os.path.basename(path``: مقداری برابر با **بخش دوم** از توپِل خروجی تابع ``(os.path.split(path`` را برمی‌گرداند [`اسناد پایتون <https://docs.python.org/3/library/os.path.html#os.path.basename>`__]::


    >>> import os.path
    >>> 
    >>> for path in [ '/one/two/three', 
    ...               '/one/two/three/',
    ...               '/',
    ...               '.',
    ...               '']:
    ...     print ('"%s" : "%s"' % (path, os.path.basename(path)))
    ... 
    "/one/two/three" : "three"
    "/one/two/three/" : ""
    "/" : ""
    "." : "."
    "" : ""
    >>> 


* ``(os.path.dirname(path``: مقداری برابر با **بخش یکم** از توپِل خروجی تابع ``(os.path.split(path`` را برمی‌گرداند [`اسناد پایتون <https://docs.python.org/3/library/os.path.html#os.path.dirname>`__]::

    >>> import os.path
    >>> 
    >>> for path in [ '/one/two/three', 
    ...               '/one/two/three/',
    ...               '/',
    ...               '.',
    ...               '']:
    ...     print ('"%s" : "%s"' % (path, os.path.dirname(path)))
    ... 
    "/one/two/three" : "/one/two"
    "/one/two/three/" : "/one/two/three"
    "/" : "/"
    "." : ""
    "" : ""
    >>>



* ``(os.path.splitext(path``: مشابه تابع ``(os.path.split(path``  است با این تفاوت که پسوند را از path جدا کرده و نتیجه را به شکل توپِل بر می‌گرداند [`اسناد پایتون <https://docs.python.org/3/library/os.path.html#os.path.splitext>`__]::

      >>> import os.path
      >>> 
      >>> for path in [ 'filename.txt', 
      ...               'filename',
      ...               '/path/to/filename.txt',
      ...               '/',
      ...               '.',
      ...               '']:
      ...     print ('"%s" : "%s"' % (path, os.path.splitext(path)))
      ... 
      "filename.txt" : "('filename', '.txt')"
      "filename" : "('filename', '')"
      "/path/to/filename.txt" : "('/path/to/filename', '.txt')"
      "/" : "('/', '')"
      "." : "('.', '')"
      "" : "('', '')"
      >>> 


* ``(os.path.join(*paths``: اجزای یک مسیر را به یکدیگر متصل می‌کند [`اسناد پایتون <https://docs.python.org/3/library/os.path.html#os.path.join>`__]::

    # GNU/Linux

    import os
    
    >>> os.path.join('one', 'two', 'three')
    'one/two/three'

    >>> os.path.join(os.sep, 'one', 'two', 'three')
    '/one/two/three'

  ::

      # Windows  

      import os  

      >>> os.path.join('one', 'two', 'three')
      'one\\two\\three'

      >>> os.path.join(os.sep, 'one', 'two', 'three')
      '\\one\\two\\three'

  همچنین برای ایجاد چندین مسیر به صورت همزمان، می‌توان اجزای هر مسیر را به صورت یک توپِل (یا لیست) درون یک لیست قرار داد و سپس با استفاده از حلقه ``for``، اجزای هر مسیر را جداگانه به تابع ``join`` ارسال نمود. البته باید توجه داشت که می‌بایست پارامتر مشخص شده در تعریف تابع ``join`` با یک ستاره مشخص شده باشد؛ در این حالت اجزای درون یک توپِل (یا لیست) به صورت پارامترهای جدا تابع در نظر گرفته می‌شوند، چیزی مانند نمونه کد بالا - در درس تابع دوباره به این شیوه ارسال پارامتر اشاره خواهد شد - به نمونه کد پایین توجه نمایید::

      >>> import os 

      >>> for parts in [ ('one', 'two', 'three'),
      ...                ('/', 'one', 'two', 'three'),
      ...                ('/one', 'two', '/three', 'four'),
      ...                ]:
      ...     print (parts, ':', os.path.join(*parts))
      ... 
      ('one', 'two', 'three') : one/two/three
      ('/', 'one', 'two', 'three') : /one/two/three
      ('/one', 'two', '/three', 'four') : '/three/four'
      >>>

  .. note::
    هر مسیر می‌بایست دقیقا شامل یک کاراکتر جدا کننده دایرکتوری (``os.sep``) باشد در غیر این صورت اجزا فقط از آخرین نمونه به بعد در نظر گرفته می‌شوند. این اتفاق در توپِل سوم  از نمونه کد بالا رخ داده است::
               
                ('one', 'two', '/three', 'four/')


* ``(os.path.expanduser(path``: این تابع تنها یک پارامتر با ترکیب ``user~`` می‌پذیرد و کاراکتر ``~`` را به مسیر دایرکتوری کاربر user در سیستم عامل تبدیل می‌کند [`اسناد پایتون <https://docs.python.org/3/library/os.path.html#os.path.expanduser>`__]::

    # GNU/Linux

    >>> os.path.expanduser('~saeid')
    '/home/saeid'

  ::

      # Windows

      >>> os.path.expanduser('~saeid')
      'C:\\Documents and Settings\\saeid'


  ::

      # GNU/Linux

      >>> for user in [ '', 'saeid', 'www-data', 'postgres' ]:
      ...     lookup = '~' +  user
      ...     print (lookup, ':', os.path.expanduser(lookup))
      ... 
      ~ : /home/saeid
      ~saeid : /home/saeid
      ~www-data : /var/www
      ~postgres : /var/lib/postgresql
      >>> 


* ``(os.path.expandvars(path``: این تابع مقدار متغیرهای محیطی موجود در پارامتر دریافتی را جایگزین کرده و حاصل را برمی‌گرداند. نام متغیرها می‌بایست با الگوی ``name$`` داخل پارامتر ذکر گردند. [`اسناد پایتون <https://docs.python.org/3/library/os.path.html#os.path.expandvars>`__]::


    >>> import os

    >>> os.environ['MYVAR'] = 'VALUE'
    >>> os.path.expandvars('/path/to/$MYVAR')
    '/path/to/VALUE'


* ``(os.path.normpath(path``: مسیر را نرمال‌سازی می‌کند. در این راه تمام مسیرهایی که به یکی از اشکال ``A//B`` ``A/B/`` ``A/./B`` ``A/foo/../B`` هستند، به صورت ``A/B`` ارزیابی می‌شوند. همچنین در سیستم عامل ویندوز کاراکتر جداکننده دایرکتوری گنولینوکس (``/``) را به ``\`` تبدیل می‌کند [`اسناد پایتون <https://docs.python.org/3/library/os.path.html#os.path.normpath>`__]::


    >>> for path in [ 'one//two//three', 
    ...               'one/./two/./three', 
    ...               'one/../one/two/three',
    ...               ]:
    ...     print (path, ':', os.path.normpath(path))
    ... 
    one//two//three : one/two/three
    one/./two/./three : one/two/three
    one/../one/two/three : one/two/three
    >>>


  ::

      # Windows

      >>> for path in [ 'one/two/three',
      ...
      ...               'one\\two\\three',
      ...               'one\\.\\two\\.\\three',
      ...               'one\\..\\one\\two\\three',
      ...               ]:
      ...     print (path, ':', os.path.normpath(path))
      ...
      one/two/three : one\two\three
      one\two\three : one\two\three
      one\.\two\.\three : one\two\three
      one\..\one\two\three : one\two\three


* ``(os.path.abspath(path``: مسیر نسبی را نرمال‌سازی کرده و به مسیر مطلق (Absolute - مسیری از ابتدا یا همان روت سیستم فایل - در گنولینوکس: مسیری که با ``/`` شروع شده باشد - در ویندوز: مسیری که با نام یک درایو شروع شده باشد) تبدیل می‌کند. حاصل این تابع برابر با حاصل متد پایین می‌باشد. [`اسناد پایتون <https://docs.python.org/3/library/os.path.html#os.path.abspath>`__]::

         (os.path.normpath(os.path.join(os.getcwd(), path)


  .. code:: python

      >>> import os

      >>> os.getcwd()
      '/mnt/Data/WorkSpace/PythonPersianTutorial'

      >>> for path in [ '.', 
      ...               '..', 
      ...               './one/two/three', 
      ...               '../one/two/three']:
      ...     print ('"%s" : "%s"' % (path, os.path.abspath(path)))
      ... 
      "." : "/mnt/Data/WorkSpace/PythonPersianTutorial"
      ".." : "/mnt/Data/WorkSpace"
      "./one/two/three" : "/mnt/Data/WorkSpace/PythonPersianTutorial/one/two/three"
      "../one/two/three" : "/mnt/Data/WorkSpace/one/two/three"
      >>> 


  .. code:: python
      
      # Windows 

      >>> import os

      >>> os.getcwd()
      'C:\\Python34'
      
      >>> for path in [ '.',
      ...               '..',
      ...               './one/two/three',
      ...               '../one/two/three']:
      ...     print ('"%s" : "%s"' % (path, os.path.abspath(path)))
      ...
      "." : "C:\Python34"
      ".." : "C:\"
      "./one/two/three" : "C:\Python34\one\two\three"
      "../one/two/three" : "C:\one\two\three"
      >>>


* گاهی لازم است که یک مسیر بررسی شود که آیا مربوط به یک فایل است یا دایرکتوری یا لینک نمادین (`Symbolic link <https://fa.wikipedia.org/wiki/پیوند_نمادین>`__)، مسیر مطلق (Absolute) است یا خیر، اصلا وجود دارد یا خیر و ... برای این منظور می‌توان از توابع پایین استفاده کرد:

  ``isabs(path)``: چنانچه مسیر مطلق باشد ``True`` برمی‌گرداند [`اسناد پایتون <https://docs.python.org/3/library/os.path.html#os.path.isabs>`__]

  ``isfile(path)``: چنانچه مسیر مربوط به یک فایل که موجود نیز هست باشد ``True`` برمی‌گرداند. این تابع لینک‌های به فایل را نیز دنبال می‌کند، پس این تابع می‌تواند همراه با تابع ``islink`` برای یک مسیر مشخص مقدار ``True`` را برگرداند.  [`اسناد پایتون <https://docs.python.org/3/library/os.path.html#os.path.isfile>`__]

  ``isdir(path)``: چنانچه مسیر مربوط به یک دایرکتوری که موجود نیز هست باشد ``True`` برمی‌گرداند. این تابع لینک‌های به دایرکتوری را نیز دنبال می‌کند، پس این تابع می‌تواند همراه با تابع ``islink`` برای یک مسیر مشخص مقدار ``True`` را برگرداند.  [`اسناد پایتون <https://docs.python.org/3/library/os.path.html#os.path.isdir>`__]


  ``islink(path)``: چنانچه مسیر مربوط به یک لینک نمادین باشد ``True`` برمی‌گرداند. [`اسناد پایتون <https://docs.python.org/3/library/os.path.html#os.path.islink>`__]

  ``exists(path)``: چنانچه مسیر دریافتی صرف نظر از اینکه مربوط به یک فایل است یا دایرکتوری، موجود باشد ``True`` برمی‌گرداند. [`اسناد پایتون <https://docs.python.org/3/library/os.path.html#os.path.exists>`__]


  ``lexists(path)``:چنانچه مسیر لینک نمادین دریافتی موجود باشد ``True`` برمی گرداند. این تابع لینک را دنبال نمی‌کند و بررسی نمی‌کند که لینک سالم هست یا خیر. [`اسناد پایتون <https://docs.python.org/3/library/os.path.html#os.path.lexists>`__]

  .. code-block:: python
      :linenos:

      # Python 3.x
      # File Name: file_script.py

      import os

      for path in [ __file__, os.path.dirname(__file__), '/', '/var/www/html/wordpress']:
          print ('Path            :', path)
          print ('Absolute        :', os.path.isabs(path))
          print ('Is File?        :', os.path.isfile(path))
          print ('Is Directory?   :', os.path.isdir(path))
          print ('Is Link?        :', os.path.islink(path))
          print ('Is Mount point? :', os.path.ismount(path))
          print ('Exists?         :', os.path.exists(path))
          print ('Link Exists?    :', os.path.lexists(path))
          print ()


  ::

      Path            : /home/saeid/Desktop/file_script.py
      Absolute        : True
      Is File?        : True
      Is Directory?   : False
      Is Link?        : False
      Is Mount point? : False
      Exists?         : True
      Link Exists?    : True

      Path            : /home/saeid/Desktop
      Absolute        : True
      Is File?        : False
      Is Directory?   : True
      Is Link?        : False
      Is Mount point? : False
      Exists?         : True
      Link Exists?    : True

      Path            : /
      Absolute        : True
      Is File?        : False
      Is Directory?   : True
      Is Link?        : False
      Is Mount point? : True
      Exists?         : True
      Link Exists?    : True

      Path            : /var/www/html/wordpress
      Absolute        : True
      Is File?        : False
      Is Directory?   : True
      Is Link?        : True
      Is Mount point? : False
      Exists?         : True
      Link Exists?    : True


  متغیر ``__file__`` در هر اسکریپتی به نام کامل آن اسکریپت اشاره دارد.

  مسیر چهارم در نمونه کد بالا در واقع مسیر لینکی است به یک دایرکتوری دیگر.



|

----

:emoji-size:`😊` امیدوارم مفید بوده باشه


