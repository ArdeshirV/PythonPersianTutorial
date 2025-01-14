.. role:: emoji-size

.. meta::
      :description: پایتون به پارسی - کتاب آنلاین و آزاد آموزش زبان برنامه‌نویسی پایتون - درس بیست و سوم: مدیریت خطا در پایتون: Exception ،Traceback و Exception Handling


.. _lesson-23: 

درس ۲۳: مدیریت خطا در پایتون: Exception ،Traceback و Exception Handling
===================================================================================================

.. figure:: /_static/pages/23-python-exception-error-warning-try.jpg
    :align: center
    :alt: مدیریت خطا در پایتون: Exception ،Traceback و Exception Handling و try/except/else/finally
    :class: page-image

    Photo by `krakenimages <https://unsplash.com/photos/8RXmc8pLX_I>`__
  

این درس به شرح یکی از مفاهیم جدانشدنی از برنامه‌نویسی یعنی **خطا (Error)** پرداخته و چگونگی بروز و مدیریت آن در زبان برنامه‌نویسی پایتون را بررسی خواهد کرد. در این درس خواهیم آموخت که ردیابی خطا در پایتون توسط **Traceback** چگونه خواهد بود و اینکه اساسا **Exception** چیست و چه مفهومی در پایتون دارد، پیاده‌سازی دستور **try/except** در پایتون چگونه می‌باشد و همچنین نقش دستورات دیگری به مانند **else** و **finally** در کنار دستور **try** پایتون چیست.

این درس تمام مفاهیم مربوط به **Error** و **Exception** را در زبان‌ برنامه‌نویسی پایتون پوشش نمی‌دهد و مطالب باقی مانده طی درس بعد ارائه خواهد شد.



:emoji-size:`✔` سطح: متوسط

----


.. contents:: سرفصل‌ها
    :depth: 2

----


.. _introduction-to-python-errors: 

مقدمه
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

بروز **خطا (Error)** همواره جزیی از برنامه‌نویسی بوده و هست. خطاهای برنامه‌نویسی انواع گوناگونی دارند؛ «خطاهای زمان کامپایل» (Compile-time errors) که آنقدر فاحش هستند که مانع از ترجمه کدهای برنامه به زبان ماشین و در نهایت اجرای آن خواهند شد و برخی دیگر که می‌توانند آنقدر ناقلا باشند که تا مدت‌ها پس از اجرا نیز خودشان را نشان ندهند! به این دسته از خطاها به اصطلاح «خطاهای زمان اجرا» (Runtime errors) می‌گویند.

**«خطاهای زمان کامپایل» (Compile-time errors)** حاصل اشتباه فاحش برنامه‌نویس بوده و معمولا نیز کشف و برطرف نمودن آن‌ها نیز بسیار ساده می‌باشد و از عدم رعایت درست قواعد زبان برنامه‌نویسی مانند سینتکس نشات می‌گیرند.

اما بروز **«خطاهای زمان اجرا» (Runtime errors)** می‌تواند به عوامل گوناگونی وابسته باشد همانند دخالت یک عامل بیرونی یا مشکلات سخت‌افزاری که ناگهان به برنامه تحمیل می‌گردند که اگر از فرض این احتمال نیز صرف نظر کنیم!، باز هم برای دفاع در برابر این دسته از خطاها، برنامه‌نویس می‌بایست کاملا هوشیار باشد. به خصوص در زبان‌های برنامه‌نویسی پویا به مانند پایتون که انواع داده در زمان اجرا تعیین می‌گردند. برای مثال فرض کنید در داخل یک تابع قرار است با یک نوع ``int`` کار شود ولی به علت ضعف برنامه‌نویسی و عدم کنترل ورودی‌ها، یک داده با نوع ``str`` به آن ارسال گردد که در این صورت نتیجه مشخص است! البته جلوگیری از این دست خطاها نیز همچنان ساده می‌باشد!. گاهی ممکن است وضعیت آنچنان مهلک باشد که یا خیلی دیر به وجود یک خطا در برنامه پی ببریم یا برای کشف علت آن زمان زیادی صرف کنیم یا هر دو! به این نوع از خطاهای زمان اجرا، «خطاهای منطقی» (Logical errors) گفته می‌شود.

**«خطاهای منطقی» (Logical errors)** برخلاف دیگر خطاها باعث توقف اجرای برنامه نشده بلکه باعث تولید نتایج نادرستی می‌شوند که از دیدگاه برنامه‌نویسی درست بوده ولی از دیدگاه منطقی کاملا اشتباه هستند. به عنوان یک مثال ساده فرض کنید فرمول محاسبه معدل اشتباه پیاده‌سازی شده باشد! این نوع خطا مصداق بارز «باگ» (Bug) در برنامه است که همیشه پیشگیری، از کشف و اصلاح آن‌ها به مراتب ساده‌تر خواهد بود.


با وجود این توضیحات و همانطور که مشاهده خواهید کرد، بروز خطا همواره یک امر زشت و ناخواسته نبوده بلکه گاهی نیز یک استراتژی از سوی برنامه‌نویس خواهد بود تا یک وضعیت را به سطوح دیگر از برنامه اعلام یا اینکه مستقیما تغییری در روند اجرای برنامه ایجاد کند. در این صورت خطاها دیگر با نام زشت خطا خوانده نمی‌شوند بلکه به آنها **استثنا یا اعتراض یا Exception** می‌گویند.


به صورت کلی، **Exception** امکانی برای خروج برنامه از یک وضعیت مشخص است و بروز آن، همانند اعلام عمومی یک خبر مهم در برنامه می‌باشد. می‌توان با پیش‌بینی بروز Exceptionها در برنامه، به اصطلاح آن‌ها را **catch** نمود و فرآیندی - یا به اصطلاح یک **handler** - را برای مدیریت آن‌ها پیاده‌سازی کرد. 

درک وقوع یک Exception و امکان ایجاد یک فرآیند برای مدیریت آن (پیاده‌سازی handler)، قابلیت مهمی در یک زبان‌برنامه‌نویسی محسوب می‌شود. چرا که می‌توان از Exception در دو نقش زیر بهره گرفت:

**۱) مدیریت خطا (Error handling):** هر Exception می‌تواند معرف یک نوع خطا یا وضعیتی نادرست در برنامه باشد، می‌توان بر اساس نوع Exception و خطایی که رخ داده برای آن از پیش چاره‌اندیشی و فرآیندی را برای مدیریت آن خطا در برنامه پیش‌بینی کرد.


**۲) اطلاع‌رسانی یک رویداد (Event notification):** از Exceptionها می‌توان برای اعلام وقوع یک حادثه مثبت نیز در برنامه استفاده کرد. به این صورت می‌توان در زمان اجرای برنامه و بر حسب شرایط، روند اجرای برنامه را تغییر داد.

----

**اما مفهوم خطا در زبان برنامه‌نویسی پایتون چگونه است؟** انواع خطاها در پایتون را می‌توان در دو دسته کلی زیر در نظر گرفت:

* خطای سینتکس (Syntax error)

* خطای زمان اجرا (Runtime error)

برای درک این دسته‌بندی و مطابقت دادن آن با توضیحات پیش لازم است تا بار دیگر به روند اجرای کدهای پایتون توجه نماییم (درس سوم - پشت صحنه اجرا). می‌دانیم پایتون یک زبان مفسری است، ولی پیش‌ از اجرا، کدهای پایتون به یک زیان میانی به نام بایت‌کد (ByteCode) ترجمه یا کامپایل می‌شوند؛ در این مرحله قواعد پایتون بررسی و در صورتی که مشکل یا خطایی وجود نداشته باشد، بایت‌کد ایجاد و به اجرا در می‌آید. خطاهایی که در این مرحله (یعنی تلاش برای ترجمه و ایجاد بایت‌کد) ممکن است رخ دهند، در پایتون **خطای سینتکس (Syntax error)** نامیده می‌شوند.

زمانی که برنامه پایتونی به اجرا درمی‌آید، یعنی از نظر رعایت قوانین یا سینتکس مشکلی وجود نداشته است، بنابراین باقی خطاها در زمان اجرا رخ خواهند داد. در زبان برنامه‌نویسی پایتون تمام خطاهای زمان اجرا در قالب یک Exception اعلام یا به اصطلاح **raise** خواهند شد.

.. _python-traceback: 

ردیابی خطا در پایتون (Traceback)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

پس از وقوع یک خطا در زمان اجرای یک برنامه پایتونی، برای ردیابی و کشف علت رخ دادن آن خطا از Traceback استفاده می‌گردد. منظور از **Traceback**، گزارشی است که جهت راهنمایی برنامه‌نویس در هنگام وقوع یک خطای زمان اجرا، توسط مفسر پایتون ارائه داده می‌شود و گاهی نیز از آن به عنوان **Stack Trace** یاد می‌شود:


.. code-block:: python
    :linenos:
    
    def sum_int(a, b):
        return a + b
    
    res = sum_int(2, 3)
    print(res)

    res = sum_int(3, 'C')
    print(res)

::

    5
    Traceback (most recent call last):
      File "sample.py", line 7, in <module>
        res = sum_int(3, 'C')
      File "sample.py", line 2, in sum_int
        return a + b
    TypeError: unsupported operand type(s) for +: 'int' and 'str'

نمونه کد بالا نمایش مثالی از بروز خطا در زمان اجراست که پیش‌تر نیز به آن اشاره کردیم. در این مثال، یک اسکریپت با نام ``sample.py`` ایجاد کرده‌ایم که کد بالا در آن درج گردیده است. تابع ``sum_int`` یک بار با مقدار قابل پذیریش (هر دو از نوع ``int``) فراخوانی می‌گردد (سطر ۴) و نتیجه (یعنی مقدار ``5``) نیز با موفقیت در خروجی چاپ می‌گردد (توسط دستور موجود در سطر ۵). اما در سطر هفتم، آرگومان‌هایی با نوع نامتناسب برای عملگر جمع ریاضی (``+``) ارسال می‌گردد و باعث بروز یک خطا یا اگر بهتر بگوییم، raise شدن یک Exception به نام ``TypeError`` می‌گردد.

خروجی حاصل از وقوع Exception فوق نمایش Traceback در پایتون می‌باشد. Traceback پایتون یک راهنمایی کامل از نوع Exception و مراتب وقوع آن را به برنامه‌نویس گزارش می‌دهد که درک درست آن یک الزام برای برنامه‌نویسی می‌باشد.

برخلاف برخی دیگر از زبان‌های برنامه‌نویسی به مانند Java باید توجه داشت که Traceback پایتون را  می‌بایست از پایین، یعنی سطر پایانی مورد بررسی قرار داد، این سطر توضیحی از نوع Exception رخ داده را ارائه می‌دهد و از این سطر به بالا مراحلی از روند اجرای برنامه که باعث بروز این Exception شده است را به ترتیب نمایش می‌دهد. ترتیب نمایش مراتب Exception نیز، از نمایش نقطه بروز Exception به قبل می‌باشد. به عنوان نمونه برای مثال قبل، می‌توانیم مشاهده کنیم که گفته شده:

* **نوع Exception چیست؟** Exception از  نوع ``TypeError`` می‌باشد که در زمان استفاده از انواع نادرست از مقادیر  برای عملگر ``+`` رخ داده است که در اینجا، این دو نوع عبارتند از: ``'int' and 'str'``. 

* **Exception در کجا رخ داده است؟‌** در سطر دوم از ``sample.py`` و  داخل بدنه ``sum_int`` و هنگام اجرای دستور ``return a + b``.

* **نقطه قبل از ورود به ناحیه Exception کجا بوده است؟** در سطر هفتم از ``sample.py`` و داخل حوزه ماژول، تابع ``sum_int`` با مقادیر ``3`` و ``'C'`` فراخوانی شده است:‌ ``res = sum_int(3, 'C')``.

* **آیا نقطه قبل‌تری نیز وجود دارد؟** خیر

پایتون تا چندین سطح قبل‌تر از نقطه بروز Exception را توسط Traceback آشکار می‌کند. این امر کمک بسیاری در فهمیدن مسیر رسیدن به Exception را در اختیار برنامه‌نویس قرار می‌دهد.

اکنون اجازه دهید نمونه کد مربوط به مثال قبل یعنی اسکریپت ``sample.py`` را با حفظ مشکل ``TypeError`` و افزودن کمی تغییر برای نمایش **خطای سینتکس (Syntax error)** آماده نماییم، بر همین اساس به  نمونه کد زیر که حاوی دو خطا از نوع Syntax error می‌باشد و خروجی آن در زمان اجرا توجه نمایید:

.. code-block:: python
    :linenos:
    
    def sum_int(a, b)
        return a + b
    
    res = sum_int(2, 3)
    print(res)

    res = sum_int(3, 'C')
    print(res)
    
    
    '

::

    File "sample.py", line 1
        def sum_int(a, b)
                        ^
    SyntaxError: invalid syntax

در نخستین بار اجرای اسکریپت ``sample.py``، پایتون متوجه یک خطای ``SyntaxError`` در سطر یکم می‌شود و جلوی مراحل تبدیل به بایت‌کد و در نهایت اجرای برنامه را در همان نقطه می‌گیرد. طبق توضیحات چاپ شده، خطا مربوط به عدم رعایت سینتکس درست برای تعریف تابع می‌باشد. کاراکتر ``^`` به جایگاه نادرست اشاره می‌کند. در انتهای تعریف سرآیند تابع اشکالی وجود دارد که با کمی دقت می‌توان دریافت که علت به عدم وجود کاراکتر انتهایی سرآیند تابع در پایتون یعنی ``:`` می‌باشد. این مورد را اصلاح کرده و دوباره اقدام به اجرای اسکریپت ``sample.py`` می‌نماییم:


.. code-block:: python
    :linenos:
    
    def sum_int(a, b):
        return a + b
    
    res = sum_int(2, 3)
    print(res)

    res = sum_int(3, 'C')
    print(res)
    
    
    '

::

    File "sample.py", line 11
        '
        ^
    SyntaxError: EOL while scanning string literal

این‌بار فرآیند اجرای برنامه در نقطه‌ای دیگر متوقف می‌گردد، سطر یازدهم از ``sample.py``. این خطا نیز از نوع ``SyntaxError`` می‌باشد ولی با توضیحی متفاوت. متن خطا می‌گوید که نحوه قرار گرفتن کاراکتر ``'`` اشتباه است. سطر یازدهم با یک کاراکتر کوتیشن پایان یافته که جفت آن و نیز عبارت یا دستوری مرتبط با آن در سطر مذکور موجود نمی‌باشد. 

با اصلاح این مشکل، برنامه از حالت ``SyntaxError`` خارج شده و کد اسکریپت ``sample.py`` با موفقیت به بایت‌کد ترجمه و  به اجرا درمی‌آید. اکنون در زمان اجرا، با ``TypeError`` که پیش‌تر بررسی کردیم برخورد خواهیم کرد!


این نکته را نیز در نظر بگیرید - همانطور که اگر به خروجی‌های دقت کرده باشید حتما متوجه شده‌اید در دو حالت مربوط به گزارش خطای مربوط به ``SyntaxError`` خبری از سطر زیر  که در حالت خطای زمان اجرای ``TypeError`` مشاهده کردیم، نمی‌باشد::

     Traceback (most recent call last):


در واقع این سطر تنها در گزارش خطاهایی که پس از اجرای برنامه رخ دهند (Runtime errors)، نمایش داده خواهد شد. در زمان بررسی و ترجمه کد پایتون به بایت‌کد هرجا مشکلی باشد عملیات در همان نقطه متوقف می‌شود و صرفا گزارشی مبنی بر ابراز آن نقطه به برنامه‌نویس ارايه می‌گردد و نه چیزی که بتوان آن را یک گزارش ردیابی با Traceback نامید چرا که هنوز برنامه به اجرا درنیامده و اصلا نیازی به این کار نیست!


.. _python-exception-handling: 

مدیریت خطا (Exception Handling)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

در زبان‌های برنامه‌نویسی صدای اعتراض یک Exception قابل درک و تشخیص است و می‌توان برای آن‌ها فرآیندی را پیش‌بینی کرد که بروز آن‌ها نه تنها باعث اتمام برنامه نشود بلکه برنامه بتواند در مسیر درست به اجرای خود ادامه دهد.

در زبان برنامه‌نویسی پایتون دستور ``try/except`` برای همین منظور فراهم دیده شده است [`اسناد پایتون <https://docs.python.org/3/reference/compound_stmts.html#the-try-statement>`__] و در ادامه به بررسی انواع ساختار قابل پیاده‌سازی از این دستور خواهیم پرداخت.

``try/except``
------------------------


ساختار این دستور به شکل زیر است::

    try:
        pass

    except:
        pass

در این ساختار آن قطعه کدی که محتمل بروز Exception می‌باشد، داخل بدنه ``try`` و قطعه کدی که می‌بایست پس از وقوع Exception به اجرا درآید (بخش handler)، داخل بدنه ``except`` قرار می‌گیرند::

    >>> def print_int_sum(a, b):
    ...     try:
    ...         print(a + b)
    ...     except:
    ...         print(f'ERROR: {a}+{b}')
    ... 
    >>> print_int_sum(2, 3)
    5
    >>> print_int_sum(9, 3)
    12
    >>> print_int_sum(5, 'D')
    ERROR: 5+D

حالت فعلی از دستور ``except`` هر نوع Exceptionای که در داخل بدنه ``try`` رخ دهد را تشخیص و ادامه اجرای برنامه را به دست می‌گیرد، به اصطلاح یک expression-less except است. ولی می‌توان دستور ``except`` را محدود به تشخیص نوع خاصی از Exception کرد. در این صورت می‌بایست نوع Exception مورد نظر خود را در کنار دستور ``except`` درج نماییم:


.. code-block:: python
    :linenos:

    def print_int_sum(a, b):

        try:
            print(a + b)

        except TypeError:
            print(f'ERROR: {a}+{b}')


می‌توان با استفاده از یک دستور  ``try`` چندین Exception را تشخیص دهیم. برای این منظور کافی است از یک دستور ``try`` به همراه چندین دستور ``except`` استفاده کنیم:

.. code-block:: python
    :linenos:

    def print_sum_div_first(a, b):

        try:
            sum = a + b
            div = sum / a
            print(div)

        except TypeError:
            print(f'TypeError: ({a}+{b!r})/{a}')

        except:
            print(f'OTHER ERROR: ({a}+{b!r})/{a}')


    print_sum_div_first(5, 6)
    print_sum_div_first(3, 'G')
    print_sum_div_first(0, 8)

::

    2.2
    TypeError: (3+'G')/3
    OTHER ERROR: (0+8)/0


ساختار ``try/except`` این مثال شامل دو دستور ``except`` می‌باشد، دستور نخست تنها ``TypeError`` و دستور دوم هر Exception دیگری به جز موارد بالای خود (در اینجا: ``TypeError``) را تشخیص می‌دهند، چرا که مفسر پایتون از بالا به پایین به دنبال handler مربوطه می‌گردد و پس از یافتن، عملیات جستجوی handler متوقف می‌شود.

در مثال قبل، دستور موجود در سطر ۱۷ باعث بروز خطای «تقسیم بر صفر» [`ویکی‌پدیا <https://en.wikipedia.org/wiki/Division_by_zero>`__] یا Exceptionای با نام ``ZeroDivisionError`` در پایتون شده است - که می‌توان به صورت زیر آن را بازنویسی نمود:

.. code-block:: python
    :linenos:

    def print_sum_div_first(a, b):

        try:
            sum = a + b
            div = sum / a
            print(div)

        except TypeError:
            print(f'TypeError: ({a}+{b!r})/{a}')

        except ZeroDivisionError:
            print(f'ZeroDivisionError: ({a}+{b!r})/{a}')


    print_sum_div_first(5, 6)
    print_sum_div_first(3, 'G')
    print_sum_div_first(0, 8)

::

    2.2
    TypeError: (3+'G')/3
    ZeroDivisionError: (0+8)/0


چنانچه مکانیزم مدیریت خطای شما برای چندین نوع Exception مشخص یکسان است می‌توانید آن دستورهای ``except`` را با یکدیگر ترکیب کرد و تنها از یک دستور ``except`` استفاده نمایید. برای این منظور تنها کافی است نام تمام Exceptionهای مورد نظر خود را در قالب یک شی توپِل به دستور ``except`` بسپرید:

.. code-block:: python
    :linenos:

    def print_sum_div_first(a, b):

        try:
            sum = a + b
            div = sum / a
            print(div)

        except (TypeError, ZeroDivisionError):
            print(f'Error: ({a}+{b!r})/{a}')


    print_sum_div_first(5, 6)
    print_sum_div_first(3, 'G')
    print_sum_div_first(0, 8)

::

    2.2
    Error: (3+'G')/3
    Error: (0+8)/0


هر چیزی در پایتون یک شی است، حتی Exceptionها! مفسر پایتون در ازای هر Exceptionای که رخ می‌دهد یک شی نیز در اختیار برنامه‌نویس قرار می‌دهد و این شی در صورت تمایل از طریق دستور ``except`` قابل دسترس می‌باشد. برای این منظور تنها کافی است از دستور ``as`` برای انتساب آن Exception به یک متغییر با نام دلخواه استفاده نماییم:

.. code-block:: python
    :linenos:

    def print_sum_div_first(a, b):

        try:
            sum = a + b
            div = sum / a
            print(div)

        except TypeError as te:
            print(f'{te.__class__.__name__}: ({a}+{b!r})/{a}')

        except ZeroDivisionError as zde:
            print(f'{zde.__class__.__name__}: ({a}+{b!r})/{a}')


    print_sum_div_first(5, 6)
    print_sum_div_first(3, 'G')
    print_sum_div_first(0, 8)


.. code-block:: python
    :linenos:

    def print_sum_div_first(a, b):

        try:
            sum = a + b
            div = sum / a
            print(div)

        except (TypeError, ZeroDivisionError) as err:
            print(f'{err.__class__.__name__}: ({a}+{b!r})/{a}')

    print_sum_div_first(5, 6)
    print_sum_div_first(3, 'G')
    print_sum_div_first(0, 8)

::

    2.2
    TypeError: (3+'G')/3
    ZeroDivisionError: (0+8)/0

البته چنانچه مایل هستید شی Exception را از طریق یک دستور ``except`` کلی (یعنی بدون ذکر نام Exception خاصی) دریافت کنید، می‌توانید از نوع یا کلاس ``Exception`` که در واقع supperclass اکثر Exceptionهای پایتون می‌باشد، استفاده نمایید:

.. code-block:: python
    :linenos:

    def print_sum_div_first(a, b):

        try:
            sum = a + b
            div = sum / a
            print(div)

        except Exception as err:
            print(f'{err.__class__.__name__}: ({a}+{b!r})/{a}')

    print_sum_div_first(5, 6)
    print_sum_div_first(3, 'G')
    print_sum_div_first(0, 8)

::

    2.2
    TypeError: (3+'G')/3
    ZeroDivisionError: (0+8)/0


.. tip:: 

  به صورت کلی وقتی در زمان اجرای دستورات داخل بدنه ``try`` یک Exception رخ می‌دهد، مفسر پایتون اجرای برنامه را در آن نقطه متوقف و شروع به جستجو برای یافتن یک handler یا همان دستور ``except`` متناسب با آن Exception می‌کند. در صورت پیدا کردن ``except`` مناسب، ادامه روند اجرای برنامه را از آن سر می‌گیرد و در غیر این صورت Exception بدون handler باعث توقف اجرای کل برنامه می‌گردد.

.. tip:: 

  چنانچه از چندین دستور ``except`` بهره می‌گیرید باید توجه داشته باشید که دستور ``except`` کلی یا همان expression-less except - در صورت وجود - می‌بایست به عنوان آخرین دستور ``except`` قرار بگیرد، در غیر این صورت دیگر دستورهای ``except`` که نوع Exception در آن‌ها مشخص شده است، فرصت اجرا پیدا نخواهند کرد.

.. tip:: 

  به صورت کلی دستور ``try`` پایتون فاقد یک حوزه یا Scope مجزا می‌باشد، بنابراین تمامی متغیرهایی که در بدنه دستور ``try`` تعریف می‌گردند جزیی از حوزه بیرونی خود هستند و در تمام بخش‌های داخل آن حوزه در دسترس خواهند بود. البته نباید فراموش کرد که اگر در هنگام انتساب به نام یک متغیر خطایی رخ داده باشد، بدیهی است که آن متغیر ایجاد نشده و اساسا در دسترس نیز نخواهد بود.

.. tip:: 

  شی Exception که توسط دستور ``except`` دریافت می‌گردد تنها در داخل بدنه همان دستور ``except`` در دسترس خواهد بود، چرا که بلافاصله پس از اتمام دستورات داخل بدنه آن ``except``، شی مذکور نیز به صورت خودکار حذف می‌گردد.


``try/except/else``
------------------------

در کنار دستور ``try/except`` می‌توان دستور ``else`` را نیز استفاده کرد. با این کاربرد که می‌توان قطعه کدی را برای مواقعی که اجرای بخش ``try`` به پایان رسیده و هیچ Exception رخ نداده باشد، به اجرا درآوریم:


.. code-block:: python
    :linenos:

    def print_sum_div_first(a, b):

        try:
            sum = a + b
            div = sum / a

        except Exception as err:
            print(f'{err.__class__.__name__}: ({a}+{b!r})/{a}')

        else:
            print(f'result: ({a}+{b!r})/{a} = {div}')

    print_sum_div_first(5, 6)
    print_sum_div_first(3, 'G')
    print_sum_div_first(0, 8)

::

    result: (5+6)/5 = 2.2
    TypeError: (3+'G')/3
    ZeroDivisionError: (0+8)/0

به یک مثال دیگر نیز توجه نماید (مرتبط با مبحث فایل‌ها - درس دهم):

.. code-block:: python
    :linenos:

    def write_to_log(text, write_mode):
        try:
            output = open('log_file.txt', write_mode)
            output.write(text)

        except FileNotFoundError as fnfe:
            print('File Not Found!!!')

        else:
            output.close()
            print('Successful, closed!')


    write_to_log('A text to insert in the log file', 'r') # WRONG mode!
    print('*' * 30)
    write_to_log('A text to insert in the log file', 'a')

::

    File Not Found!!!
    ******************************
    Successful, closed!


**توجه داشته باشید،** چنانچه بدنه ``try`` شامل دستور ``return`` باشد، آنگاه بدنه دستور ``else`` اجرا نخواهد شد!:


.. code-block:: python
    :linenos:

    def print_sum_div_first(a, b):
        try:
            sum = a + b
            div = sum / a
            return 'Successful'

        except Exception as err:
            return 'Failed'

        else:
            return 'Successful, from else!'

    result = print_sum_div_first(5, 6)   # Successful
    print(result)

    result = print_sum_div_first(3, 'G') # Failed
    print(result)

::

    Successful
    Failed



``try/finally``  ``try/except/finally``  ``try/except/else/finally``
---------------------------------------------------------------------------------------------

دستور ``finally`` نیز یک دستور اختیاری مشابه با ``else`` می‌باشد که می‌توان از آن در کنار دستور ``try`` بهره گرفت. با استفاده از این دستور می‌توان یک قطعه کد را مهیا کرد که در هر حالتی اجرا گردد یعنی چه در حالتی که Exceptionای داخل ``try`` رخ دهد و چه ندهد! بدنه دستور ``finally`` اجرا می‌شود.

اکنون می‌توان روند کلی فرآیند اجرای دستورات پایتون در یک بلاک ``try`` را به این صورت شرح داد:

**۱) در صورت عدم بروز Exception** داخل بدنه دستور ``try``: پس از پایان اجرای دستورات داخل بدنه دستور ``try``، نقطه اجرای برنامه به دستور ``else`` - در صورت وجود - سپرده می‌شود، پس از پایان اجرای دستورات داخل بدنه ``else``، نقطه اجرای برنامه به دستور ``finally`` - در صورت وجود - سپرده می‌شود.

**۲) در صورت بروز Exception** داخل بدنه دستور ``try``: نقطه اجرای برنامه بلافاصله به دستور ``except`` مناسب سپرده می‌شود، پس از پایان اجرای دستورات داخل بدنه ``except``، نقطه اجرای برنامه به دستور ``finally`` - در صورت وجود - سپرده می‌شود.




.. code-block:: python
    :linenos:

    def print_sum_div_first(a, b):
        try:
            print('----> try')
            sum = a + b
            div = sum / a

        except Exception as err:
            print('----> except')

        else:
            print('----> else')

        finally:
            print('----> finally')


    print_sum_div_first(5, 6)
    print('*' * 20)
    print_sum_div_first(3, 'G')

::

    ----> try
    ----> else
    ----> finally
    ********************
    ----> try
    ----> except
    ----> finally

حتی اگر زمانی داخل بدنه دستور ``except`` نیز یک Exception دیگر رخ دهد، مفسر پایتون اعلام اعتراض آن Exception را موقتا نگه‌می‌دارد تا بدنه دستور ``finally`` به صورت کامل اجرا گردد. در واقع کاربرد اصلی دستور ``finally`` - که تحت هر شرایطی اجرا می‌گردد - تمیزکاری یا Cleaning Up کردن کد پس از انجام کاری مشخص است (پاک کردن فایل‌های موقت، آزادسازی منابع، حذف اشیایی که دیگر مورد نیاز نیستند و...) که از آن معمولا به عنوان Cleanup Handler نیز یاد می‌شود:


.. code-block:: python
    :linenos:

    def print_sum_div_first(a, b):
        try:
            sum = a + b
            div = sum / a

        except TypeError as err:
            print(f'{err.__class__.__name__}: ({a}+{b!r})/{a} =', (a+b)/a)

        finally:
            print('----> finally')


    print_sum_div_first(5, 6)
    print('*' * 20)
    print_sum_div_first(3, 'G')

::

    ----> finally
    ********************
    ----> finally
    Traceback (most recent call last):
      File "sample.py", line 3, in print_sum_div_first
        sum = a + b
    TypeError: unsupported operand type(s) for +: 'int' and 'str'

    During handling of the above exception, another exception occurred:

    Traceback (most recent call last):
      File "sample.py", line 15, in <module>
        print_sum_div_first(3, 'G')
      File "sample.py", line 7, in print_sum_div_first
        print(f'{err.__class__.__name__}: ({a}+{b!r})/{a} =', (a+b)/a)
    TypeError: unsupported operand type(s) for +: 'int' and 'str'

همانطور که از خروجی نمونه کد بالا مشاهده می‌شود، داخل بدنه دستور ``except``، یک Exception دیگر رخ داده است. نکته قابل توجه این است که حتی در این وضعیت نیز بدنه دستور ``finally`` اجرا شده و سپس وقوع Exception بدنه ``except`` باعث توقف برنامه شده است.

اگر به گزارش Traceback پایتون در این وضعیت دقت نمایید، مشاهده خواهید کرد که این گزارش چقدر کامل است چرا که حتی به ما می‌گوید در هنگام handle کردن یک Exception بوده که Exception دیگری رخ داده است!


**توجه داشته باشید،** چنانچه بدنه ``try`` و ``except`` و ``finally`` شامل دستور ``return`` باشند، آنگاه این دستور ``return`` از بدنه دستور ``finally`` است که اجرا خواهد شد!:


.. code-block:: python
    :linenos:

    def print_sum_div_first(a, b):
        try:
            sum = a + b
            div = sum / a
            return 'Successful'

        except Exception as err:
            return 'Failed'

        else:
            return 'Successful, from else!'

        finally:
            return '---------->finally!'

    result = print_sum_div_first(5, 6)   # Successful
    print(result)

    result = print_sum_div_first(3, 'G') # Failed
    print(result)

::

    ---------->finally!
    ---------->finally!


گاهی تنها از دستور ``finally`` در کنار ``try`` استفاده می‌گردد، یعنی بدون حضور هیچ‌گونه دستور ``except`` به صورت ``try/finally``. می‌توان از این قالب برای زمانیکه رخداد Exception و مدیریت آن برایمان اهمیتی نداشته باشد، بهره بگیریم. با این حال به نمونه کد زیر توجه نمایید:


.. code-block:: python
    :linenos:

    def print_sum_div_first(a, b):
        try:
            sum = a + b
            div = sum / a
            print(f'----> Result: {div}')

        finally:
            print('--------> Finished!')


    print_sum_div_first(5, 6)
    print('*' * 30)
    print_sum_div_first(3, 'G')

::

    ----> Result: 2.2
    --------> Finished!
    ******************************
    --------> Finished!
    Traceback (most recent call last):
      File "sample.py", line 13, in <module>
        print_sum_div_first(3, 'G')
      File "sample.py", line 3, in print_sum_div_first
        sum = a + b
    TypeError: unsupported operand type(s) for +: 'int' and 'str'

به هر حال Exception بدون handler باعث توقف اجرای برنامه می‌شود اما اگر داخل بدنه ``finally`` شامل دستور ``return`` باشد، آنگاه مفسر پایتون از اعلام Exception رخ داده که در حال حاظر به صورت موقت نگه‌داشته است تا اجرای بدنه ``finally`` به پایان برسد، صرف نظر خواهد کرد!:

.. code-block:: python
    :linenos:

    def print_sum_div_first(a, b):
        try:
            sum = a + b
            div = sum / a
            print(f'----> Result: {div}')

        finally:
            print('--------> Finished!')
            return None


    print_sum_div_first(5, 6)
    print('*' * 30)
    print_sum_div_first(3, 'G')

::

    ----> Result: 2.2
    --------> Finished!
    ******************************
    --------> Finished!


روند انتشار Exception
----------------------------

در تمام مثال‌هایی که در این بخش ارائه شد، برای ساده‌سازی مطلب تنها به بررسی مدیریت خطا داخل یک تابع پرداختیم. ولی باید این مورد را در نظر داشته باشید، زمانی که یک Exception رخ می‌دهد، این Exception به ترتیب مراحل فراخوانی را به ابتدای اجرا در برنامه طی می‌کند و هر بار چنانچه یک handler (دستور ``try`` با ``except`` مناسب) پیدا نشود، این Exception به مرحله پیش‌تر تحویل داده می‌شود تا شاید یک handler برای آن پیدا شود. این روند تا رسیدن به اسکریپت (فایل py. اصلی برنامه) ادامه می‌یابد و در صورت عدم پیش‌بینی handler آنگاه Exception در این نقطه بروز و منجر به توقف کل برنامه می‌گردد. به عنوان مثال نمونه کد زیر را در نظر بگیرید:


.. code-block:: python
    :linenos:

    def print_sum_div_first(a, b):
        sum = a + b
        div = sum / a
        print(div)


    def action(a, b):
        try:
            if isinstance(a, int):
               print_sum_div_first(a, b)

        except ZeroDivisionError as err:
            print(f'[action function ERROR!!!] {err.__class__.__name__}')


    try:
        action(5, 6)    # Successfully
        action(0, 8)    # raise ZeroDivisionError
        action(3, 'G')  # raise TypeError

    except Exception as err:
        print(f'[module ERROR!!!] {err.__class__.__name__}')

::

    2.2
    [action function ERROR!!!] ZeroDivisionError
    [module ERROR!!!] TypeError

در نمونه کد بالا همانطور که مشخص است تمام Exceptionها در داخل تابع ``print_sum_div_first`` رخ می‌دهد ولی از آنجا که این تابع فاقد handler می‌باشد، Exceptionها به یک مرحله قبل‌تر یعنی تابع ``action`` تحویل می‌گردند، ولی این تابع تنها یک handler برای ``ZeroDivisionError`` داشته پس تمامی Exceptionهای احتمالی دیگر از جمله ``TypeError`` به یک مرحله قبل‌تر تحویل و خوشبختانه در آن‌جا handle می‌شوند!


مدیریت خطای تودرتو (Nested Exception Handling)
---------------------------------------------------

به صورت کلی بدنه هر یک از دستورهای ``try`` ، ``except`` ، ``else`` ، ``finally`` به خودی‌خود می‌توانند شامل یک دستور ``try/except/else/finally`` دیگر باشد. هر جا که کدی نوشته شود آنجا نیز احتمال بروز Exception وجود دارد و هر جا که احتمال بروز Exception وجود داشته باشد به یک handler برای آن نیاز است.

البته از آنجا که در یکی از بندهای فلسفه پایتون آمده: `PEP 20: Flat is better than nested <https://www.python.org/dev/peps/pep-0020/>`__ انجام این‌کار چندان پایتونی نمی‌باشد و برنامه‌نویس احتمالا می‌تواند با کمی دقت بیشر از ساختار تودرتو پرهیز کند و کدی به مراتب خواناتر توسعه دهد. به هر حال امکان این کار در زبان برنامه‌نویسی پایتون برای برنامه‌نویس محفوظ نگه‌داشته شده است.



مدیریت خطا و دستور ``with``
--------------------------------------

از درس بیست و یکم با مفهوم Context Manager و ارتباط آن با دستور ``with`` آشنا هستیم. اینکه مدیریت خطا برای این ساختار چگونه باشد به این بستگی دارد که می‌خواهیم در کدام نقطه Exception احتمالی را handle کنیم. بر اساس مفهوم Context Manager، در چند نقطه زیر احتمال بروز Exception وجود دارد:

* داخل متد ``__init__`` کلاس ContextManager
* داخل متد ``__enter__`` کلاس ContextManager
* داخل بدنه دستور ``with``
* داخل متد ``__exit__`` کلاس ContextManager


اگر برایمان مهم نباشد می‌توانیم به صورت زیر یک handler برای بروز Exceptionهای احتمالی در تمام حالات بالا پیاده‌سازی نماییم::


    try:
        with ContextManager():
            do_something()
    except Exception as err:
        pass


در غیر این صورت می‌توانید مشابه نمونه کد زیر عمل نمایید::

    try:
        context_manager = ContextManager()

    except Exception as err:
        # Handler for: '__init__'

    else:
        try:
            with context_manager:
                try:
                    do_something()

                except Exception as err:
                    # Handler for: 'with' body

        except Exception as err:
            # Handler for: '__enter__' and '__exit__'


[`PEP 343 - Specification: The 'with' Statement <https://www.python.org/dev/peps/pep-0343/#specification-the-with-statement>`__]


کارایی (Performance)
----------------------------

همیشه این سوال مطرح می‌شود که آیا بهتر است با کنترل شرط و پیاده‌سازی چندین دستور ``if`` از بروز Exception جلوگیری کنیم یا خیلی ساده این وظیفه را به یک ساختار handler بسپاریم. کدام روش کارایی بهتری دارد؟

زبان برنامه‌نویسی پایتون از نظریه «درخواست بخشش راحت‌تر از کسب اجازه است» پیروی می‌کند [`EAFP: Easier to ask for forgiveness than permission <https://docs.python.org/3/glossary.html?highlight=eafp#term-eafp>`__]. بر همین اساس پایتون به صورت پیش‌فرض تمام مقادیر را صحیح فرض می‌کند و زمانی اگر خلاف این فرض رخ دهد، آنگاه برای عرض پوزش به دنبال یک handler مناسب می‌گردد!

مطمئنا سربار handle کردن یک Exception از یک دستور ``if`` بیشتر است ولی تنها وقتی یک Exception به handler نیاز پیدا می‌کند که رخ بدهد! پیشنهاد پایتونی برای این مسئله ترجیح بر استفاده از دستور ``try/except`` می‌باشد تا دستور ``if``، چرا که هم خوانایی کد بیشتر می‌شود و هم از آنجایی که در صورت استفاده از دستور ``if`` روند اجرای کنترل و بررسی شرط هربار در برنامه رخ می‌دهد ولی عمل جستجو برای یافتن ``except`` مناسب تنها در زمان رخ دادن Exception انجام خواهد شد، کارایی بهتری کسب می‌گردد.


[`مطالعه بیشتر:‌ پرسش و پاسخ مرتبط در StackOverflow <https://stackoverflow.com/q/7604636>`__]



Exception Hierarchy
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

در زبان برنامه‌نویسی پایتون تمامی Exceptionهای از پیش آماده در قالب کلاس‌هایی در یک سلسله مراتب از وراثت ارايه شده است. برای مشاهده این کلاس‌ها و ساختار وراثت آن‌ها می‌توانید به اسناد پایتون مراجعه نمایید:‌ `Exception hierarchy <https://docs.python.org/3/library/exceptions.html#exception-hierarchy>`__ - این ساختار توسط تصویر پایین نمایش داده شده است:


.. image:: /_static/lessons/l23-python-exception-hierarchy.png
    :align: center
    :alt: Exception Hierarchy در پایتون

کلاس ``BaseException`` در بالاترین سطح وراثت برای این دست کلاس‌ها قرار دارد و تمامی Exceptionها به صورت مستقیم یا غیر مستقیم از آن ارث‌بری دارند. از این بین تنها چهار کلاس هستند که مستقیم از ``BaseException`` ارث‌بری دارند:

* کلاس ``SystemExit`` [`اسناد پایتون <https://docs.python.org/3/library/exceptions.html#SystemExit>`__]: هرگاه به برنامه پایتونی با اراده برنامه‌نویس و با استفاده از تابع ``exit`` از ماژول ``sys`` [`اسناد پایتون <https://docs.python.org/3/library/sys.html#sys.exit>`__] فرمان توقف صادر شود، این Exception رخ خواهد داد.

* کلاس ``KeyboardInterrupt`` [`اسناد پایتون <https://docs.python.org/3/library/exceptions.html#KeyboardInterrupt>`__]: هرگاه با استفاده از صفحه‌کلید (Keyboard) اقدام به توقف ناگهانی برنامه پایتون نماییم - معمولا با استفاده از کلیدهای ترکیبی:‌ ``Control+C``، این Exception رخ خواهد داد.

* کلاس ``GeneratorExit`` [`اسناد پایتون <https://docs.python.org/3/library/exceptions.html#GeneratorExit>`__]: این Exception در زمانی که یک Generator (درس سیزدهم) بسته (Close) می‌شود [`اسناد پایتون <https://docs.python.org/3/reference/expressions.html#generator.close>`__]، رخ می‌دهد.

* کلاس ``Exception`` [`اسناد پایتون <https://docs.python.org/3/library/exceptions.html#Exception>`__]: می‌توان این‌گونه شرح داد که این کلاس، supperclass تمام Exceptionها به غیر از سه مورد قبلی است!



.. tip:: 

  زمانی که یک نوع Exception در دستور ``except`` ذکر می‌گردد، آن دستور ``except`` به عنوان یک handler برای آن نوع Exception و تمامی subclassهایی خواهد بود که از آن Exception ارث‌بری دارند.


.. tip:: 

  دو دستور ``except`` زیر معادل یکدیگر بوده و از نظر مفسر پایتون به عنوان یک handler برای تمام انواع Exceptionها می‌باشند و تنها تفاوت آن‌ها در امکان دریافت شی Exception می‌باشد. برای ایجاد یک handler برای ``KeyboardInterrupt`` ،``SystemExit`` و ``GeneratorExit`` یا می‌بایست نام آن‌ها به صورت مستقیم در ``except`` قرار داده شود یا یکی از فرم‌های پایین از دستور ``except`` را استفاده نماییم:

  ::

      except:

  ::

      except BaseException as error:


  در واقع ``BaseException`` نوع Exception پیش‌فرض برای دستور ``except`` می‌باشد.



|

----

:emoji-size:`😊` امیدوارم مفید بوده باشه



