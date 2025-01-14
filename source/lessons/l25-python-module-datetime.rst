.. role:: emoji-size

.. meta::
   :description: پایتون به پارسی - کتاب آنلاین و آزاد آموزش زبان برنامه‌نویسی پایتون - درس بیست و پنجم: زمان در پایتون: ماژول‌ datetime


.. _lesson-25: 


درس ۲۵: زمان در پایتون: ماژول‌ datetime 
===========================================

.. figure:: /_static/pages/25-python-date-time-calendar.jpg
    :align: center
    :alt: زمان در پایتون: ماژول‌ datetime و timezone, timedelta, tzinfo
    :class: page-image

    Photo by `Niloofar Kanani <https://unsplash.com/photos/a-dep2gUeRI>`__
  

  
  

برای کار با زمان سه ماژول در کتابخانه استاندارد زبان برنامه‌نویسی پایتون آماده شده است؛ time ،datetime و calendar. این درس به شرح کامل ماژول datetime پایتون اختصاص یافته است. ماژول datetime پایتون انواع یا کلاس‌های زیادی را برای ایجاد اشیا مرتبط با زمان و دستکاری (manipulating) آن‌ها فراهم آورده است، همچون ``time`` ،``date`` ،``timezone`` ،``timedelta`` و ``datetime`` که همگی در این درس بررسی خواهند شد.


:emoji-size:`✔` سطح: متوسط

----


.. contents:: سرفصل‌ها
    :depth: 2

----


.. _python-datetime-module: 

ماژول datetime
~~~~~~~~~~~~~~~~~~~~~~~~~~~

این ماژول [`اسناد پایتون <https://docs.python.org/3/library/datetime.html>`__] از کتابخانه استاندارد زبان برنامه‌نویسی پایتون چند نوع یا کلاس برای کار با زمان (ساعت و تاریخ) را در اختیار برنامه‌نویس قرار می‌دهد:

* **کلاس** ``date``: مناسب برای ایجاد شی تاریخ در پایتون می‌باشد که اشیا آن هیچ آگاهی نسبت به ساعت و منطقه زمانی (Time zone) [`ویکی‌پدیا <https://en.wikipedia.org/wiki/Time_zone>`__] نخواهند داشت و تنها مربوط به روزی خاص بر اساس گاه‌شماری میلادی (Gregorian calendar) [`ویکی‌پدیا <https://en.wikipedia.org/wiki/Gregorian_calendar>`__] می‌باشند.

* **کلاس** ``time``: مناسب برای ایجاد شی ساعت در پایتون می‌باشد و اشیا این کلاس هیچ آگاهی نسبت به تاریخ یا روز خاصی ندارند و تنها حاوی یک ساعت مشخص از شبانه‌روز خواهند بود.

* **کلاس** ``datetime``: ترکیبی از دو کلاس ``date`` و ``time`` که اشیای آن می‌توانند نسبت به یک زمان (تاریخ و ساعت) مشخص آگاهی کامل داشته باشند.

در ادامه به بررسی این سه کلاس خواهیم پرداخت، اما پیش از این کار لازم است با دو کلاس دیگر از ماژول datetime آشنا شویم،  ``timedelta`` و ``tzinfo``.


کلاس ``datetime.timedelta``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

در زبان برنامه‌نویسی پایتون از اشیای کلاس ``timedelta`` [`اسناد پایتون <https://docs.python.org/3/library/datetime.html#timedelta-objects>`__] برای بیان «مدت زمان» (duration) مشخص یا اختلاف بین دو تاریخ یا زمان استفاده می‌شود. الگوی نمونه‌سازی از این کلاس به شکل زیر است::

    td = timedelta(days=0, 
                   seconds=0, 
                   microseconds=0, 
                   milliseconds=0, 
                   minutes=0, 
                   hours=0, 
                   weeks=0)

با نمونه‌سازی از این کلاس و ارسال آرگومان‌های دلخواه، براساس تمام واحدهای پرتکرار از زمان یا حتی ترکیبی از آن‌ها می‌توانیم یک مدت‌زمان در سیستم زمانی پایتون ایجاد کنیم؛ هفته (weeks)، روز (days)، ساعت (hours)، دقیقه (minutes)، ثانیه (seconds)، میلی‌ثانیه (milliseconds یا همان 0.001 ثانیه) و میکروثانیه (microseconds یا همان 0.000001 ثانیه). تمامی این مقادیر اختیاری و با مقدار پیش‌فرض ``0`` هستند که می‌توانند از نوع ``int`` یا ``float``، مثبت یا منفی باشند:

::

    >>> from datetime import timedelta


::

    >>> no_duration = timedelta()
    >>> no_duration
    datetime.timedelta(0)

    >>> no_duration.total_seconds()
    0.0

::

    >>> delta = timedelta(
    ...     days=50,
    ...     seconds=27,
    ...     microseconds=10,
    ...     milliseconds=29000,
    ...     minutes=5,
    ...     hours=8,
    ...     weeks=2
    ... )
    >>> # Only days, seconds, and microseconds remain
    >>> delta
    datetime.timedelta(days=64, seconds=29156, microseconds=10)

    >>> delta.total_seconds()
    5558756.00001

::

    >>> one_half_days = timedelta(days=1.5)
    >>> one_half_days
    datetime.timedelta(days=1, seconds=43200)

    >>> one_half_days.total_seconds()
    129600.0



توجه داشته باشید که از تمام انواع آرگومانی که ارسال می‌کنید این تنها ``seconds`` ،``days`` و ``microseconds`` هستند که دارای attribute متناظر بوده و قابل دسترس می‌باشند. در واقع تمامی مقادیر ارسالی در زمان نمونه‌سازی با یکدیگر ترکیب شده و در نهایت به این سه attribute تبدیل می‌شوند. به مقداردهی در زمان نمونه‌سازی و نیز به خروجی مقادیر از نمونه کدهای بالا توجه نمایید.

همچنین از نسخه 3.2 پایتون می‌توانید با استفاده از متد ``total_seconds`` [`اسناد پایتون <https://docs.python.org/3/library/datetime.html#datetime.timedelta.total_seconds>`__] کل مدت زمان ذخیره شده در شی timedelta را در واحد ثانیه دریافت نمایید::

    >>> delta = timedelta(microseconds=1)
    >>> delta.total_seconds()
    1e-06

دو شی ``datetime.timedelta`` پایتون قابلیت شرکت در محاسبات ریاضی را دارند::


    >>> from datetime import timedelta

    >>> year = timedelta(days=365)

    >>> ten_years = 10 * year
    >>> ten_years
    datetime.timedelta(days=3650)

    >>> ten_years.days // 365
    10

    >>> nine_years = ten_years - year
    >>> nine_years
    datetime.timedelta(days=3285)

    >>> three_years = nine_years // 3
    >>> three_years
    datetime.timedelta(days=1095)

    >>> three_years.days // 365
    3

::

    >>> day = timedelta(days=1)
    >>> negative_day = timedelta(days=-1)

    >>> negative_day
    datetime.timedelta(days=-1)

    >>> day + negative_day
    datetime.timedelta(0)

    >>> day - negative_day
    datetime.timedelta(days=2)



همچنین دو شی ``datetime.timedelta`` پایتون قابلیت مقایسه با یکدیگر را دارند::

    >>> from datetime import timedelta
    >>> year = timedelta(days=365)
    >>> three_years = timedelta(days=1095)

    >>> year == year
    True
    >>> year == three_years
    False
    >>> year > three_years
    False
    >>> year < three_years
    True
    >>> year * 3  == three_years
    True

در ادامه به همراه بخش‌های بعدی این درس با کاربرد اصلی اشیای ``datetime.timedelta`` آشنا خواهیم شد.



کلاس ``datetime.tzinfo``
~~~~~~~~~~~~~~~~~~~~~~~~~~~

هر وقت که صحبت از ساعت و زمان باشد، «منطقه زمانی» (Time zone) نیز جزئی از گفتگو خواهد بود. در زبان برنامه‌نویسی پایتون کلاس ``tzinfo`` از ماژول ``datetime`` امکان ایجاد منطقه زمانی را فراهم آورده است [`اسناد پایتون <https://docs.python.org/3/library/datetime.html#datetime.tzinfo>`__]. ``tzinfo`` در واقع یک کلاس Abstract (درس نوزدهم) می‌باشد که نمی‌توان از آن نمونه‌سازی و شی ایجاد کرد ولی می‌توان به کمک آن، کلاس منطقه زمانی دلخواه خود را ایجاد نماییم. برای مشاهده اجزا و نکات مربوط به پیاده‌سازی منطقه زمانی دلخواه می‌توانید به مستندات زبان برنامه‌نویسی پایتون مراجعه نمایید. 

اشتباه نکنید، در اکثر مواقع نیازی به پیاده‌سازی یک کلاس منطقه زمانی در پایتون نمی‌باشد. چرا که از قبل کلاس ``timezone`` از ماژول ``datetime`` [`اسناد پایتون <https://docs.python.org/3/library/datetime.html#timezone-objects>`__] توسط این زبان فراهم آورده شده است. این کلاس یک subclass از ``datetime.tzinfo`` بوده و مبنای محاسبه منطقه زمانی در آن UTC [`ویکی‌پدیا <https://en.wikipedia.org/wiki/Coordinated_Universal_Time>`__] می‌باشد. UTC یک قرارداد جهانی است و این کلاس به تنهایی تمامی نیازهای معمول ما نسبت به ثبت منطقه زمانی در پایتون را برطرف می‌سازد. برای مثال، در سراسر ایران منطقه زمانی یکسان می‌باشد و به صورت استاندارد از مبنای UTC محاسبه می‌گردد؛ به این صورت که در شش ماه نخست سال برابر ``UTC+4:30``  - با شمارش ساعت تابستانی [`ویکی‌پدیا <https://en.wikipedia.org/wiki/Daylight_saving_time>`__] - و در شش ماه دوم از سال این مقدار برابر ``UTC+3:30`` خواهد بود [`ویکی‌پدیا Iran Standard Time (IRST) <https://en.wikipedia.org/wiki/Iran_Standard_Time>`__].


.. note::

  در زبان برنامه‌نویسی پایتون اشیای مرتبط با زمان براساس توانایی آگاهی آن‌ها از منطقه زمانی (Time zone) به دو دسته **«آگاه» (aware)** و **«ساده» (naive)** تقسیم‌بندی می‌شوند. بر همین اساس اشیای کلاس ``date`` از نوع naive و اشیای دو کلاس ``time`` و ``datetime`` می‌توانند برحسب شرایط  aware یا naive باشند.



کلاس ``datetime.timezone``
------------------------------

الگوی نمونه‌سازی از این کلاس به صورت زیر است::


    timezone(offset, name=None)

که در آن پارامتر ``offset`` یک شی از نوع ``datetime.timedelta`` می‌باشد که می‌بایست حاوی فاصله زمانی منطقه مورد نظر ما از مبدا UTC باشد (مثبت (جلوتر) یا منفی (عقب‌تر)) و ``name`` نیز یک نام دلخواه و اختیاری برای شناسایی منطقه زمانی ایجاد شده می‌باشد::

    >>> from datetime import timedelta, timezone

    >>> tz = timezone(timedelta(hours=4, minutes=30), 'Asia/Tehran')

    >>> tz
    datetime.timezone(datetime.timedelta(seconds=16200), 'Asia/Tehran')

    >>> type(tz)
    <class 'datetime.timezone'>

شی ``tz`` ایجاد شده در نمونه کد بالا، بیانگر منطقه زمانی ``UTC+4:30`` (Asia/Tehran، با شمردن ساعت تابستانی) می‌باشد. به عنوان مثالی دیگر، ایجاد شی برای منطقه زمانی ``UTC-05:00`` (EST، بدون شمردن ساعت تابستانی) [`ویکی‌پدیا <https://en.wikipedia.org/wiki/Eastern_Time_Zone>`__] به صورت زیر می‌باشد::


    >>> tz = timezone(timedelta(hours=-5), 'Eastern Time Zone')

.. note::

  به منظور شفاف‌سازی بیشتر و درک اهمیت منطقه زمانی، اگر فرض کنیم ساعت در یک لحظه به وقت ``UTC`` برابر ``12:00`` است آنگاه همان لحظه ساعت به وقت ``UTC-05:00`` برابر ``07:00`` و به وقت ``UTC+04:30`` برابر ``16:30`` خواهد بود.



از طریق شی ``datetime.timezone`` چهار متد زیر در دسترس خواهد بود، در واقع  این‌ها متدهایی هستند که توسط ``datetime.timezone`` از کلاس ``datetime.tzinfo`` ارث‌برده و Override شده‌اند:

* **متد** ``utcoffset(dt)`` [`اسناد پایتون <https://docs.python.org/3/library/datetime.html#datetime.timezone.utcoffset>`__]: ورودی نادیده گرفته می‌شود و خروجی یک شی ``datetime.timedelta`` برابر اختلاف فاصله زمانی از مبنا UTC می‌باشد.

* **متد** ``tzname(dt)`` [`اسناد پایتون <https://docs.python.org/3/library/datetime.html#datetime.timezone.tzname>`__]: نام منطقه زمانی ارسال شده در زمان نمونه‌سازی را برمی‌گرداند. چنانچه در زمان نمونه‌سازی مقداری ارسال نشده و نام برابر ``None`` باشد، یک نام به صورت خودکار تولید خواهد شد. ورودی می‌تواند ``None`` یا یک شی aware از نوع ``datetime.datetime`` باشد.

* **متد** ``dst(dt)`` [`اسناد پایتون <https://docs.python.org/3/library/datetime.html#datetime.timezone.dst>`__]: خروجی این متد برای اشیا ``datetime.timezone`` همواره برابر ``None`` خواهد بود.

* **متد** ``fromutc(dt)`` [`اسناد پایتون <https://docs.python.org/3/library/datetime.html#datetime.timezone.fromutc>`__]: ورودی می‌بایست یک شی aware از نوع ``datetime.datetime`` باشد و خروجی نیز برابر ``dt + offset`` خواهد بود. در واقع این متد یک شی ``datetime.datetime`` دریافت و منطقه زمانی آن را بر اساس اطلاعات خود تغییر و برمی‌گرداند.

این کلاس حاوی یک Class attribute نیز می‌باشد. ``utc`` [`اسناد پایتون <https://docs.python.org/3/library/datetime.html#datetime.timezone.utc>`__] که برابر یک شی ``datetime.timezone`` جدید براساس منطقه زمانی UTC می‌باشد. یعنی:‌ ``timezone(timedelta(0))``


::

    >>> from datetime import timedelta, timezone
    >>> tz = timezone(timedelta(hours=4, minutes=30), 'Asia/Tehran')

    >>> tz.utcoffset(None)
    datetime.timedelta(seconds=16200)
    
    >>> tz.tzname(None)
    'Asia/Tehran'
    
::

    >>> from datetime import timedelta, timezone
    >>> tz = timezone(timedelta(hours=4, minutes=30))
    >>> tz.tzname(None)
    'UTC+04:30'


::

    >>> from datetime import timezone
    >>> type(timezone.utc)
    <class 'datetime.timezone'>


کلاس ``datetime.date``
~~~~~~~~~~~~~~~~~~~~~~~~~~~

این کلاس [`اسناد پایتون <https://docs.python.org/3/library/datetime.html#date-objects>`__] نمایش ایجاد یک شی تاریخ بر اساس گاه‌شماری میلادی (Gregorian calendar) در زبان برنامه‌نویسی پایتون می‌باشد. در واقع کاربرد این شی، نگهداری از اطلاعات مربوط به یک تاریخ مشخص خواهد بود (همچون:‌ سال، ماه و روز). در ادامه این بخش به بررسی چگونگی ایجاد این شی و اجزای آن خواهیم پرداخت.


.. _python-create-date-objects: 

ایجاد شی ``date``
------------------

به پنج شیوه زیر می‌توان یک شی از نوع ``datetime.date`` ایجاد کرد:

::

     >>> import datetime

     >>> # Wednesday, April 7, 2021

     >>> d = datetime.date(2021, 4, 7)
     >>> d = datetime.date.fromisoformat('2021-04-07')  # Python 3.7
     >>> d = datetime.date.fromordinal(737887)
     >>> d = datetime.date.fromtimestamp(1617737400)
     >>> d = datetime.date.fromisocalendar(2021, 14, 3) # Python 3.8

     >>> d
     datetime.date(2021, 4, 7)
     >>> type(d)
     <class 'datetime.date'>

     >>> d.year
     2021
     >>> d.month
     4
     >>> d.day
     7



**۱- با استفاده از نمونه‌سازی**::

    >>> import datetime
    >>> d = datetime.date(2021, 4, 7)


::


    >>> import datetime
    >>> d = datetime.date(year=2021, month=4, day=7)


برای نمونه‌سازی از کلاس ``datetime.date`` می‌بایست سه Instance attribute آن را مقداردهی نماییم. این سه attribute عبارتند از:

* ``year``: از نوع ``int`` می‌باشد و مقداری برابر با سال مورد نظر خواهد داشت. این مقدار می‌بایست کمتر یا برابر ``datetime.MAXYEAR`` [`اسناد پایتون <https://docs.python.org/3/library/datetime.html#datetime.MAXYEAR>`__] و همچنین بیشتر یا برابر ``datetime.MINYEAR`` [`اسناد پایتون <https://docs.python.org/3/library/datetime.html#datetime.MINYEAR>`__] باشد::

    MINYEAR <= year <= MAXYEAR

* ``month``: از نوع ``int`` می‌باشد و مقداری برابر با ماه مورد نظر خواهد داشت که می‌بایست عددی از بین اعداد ``1`` تا ``12`` باشد.

* ``day``: از نوع ``int`` می‌باشد و مقداری برابر با روزی مشخص در ماه ذکر شده خواهد داشت.



  ::

      >>> datetime.MINYEAR
      1
      >>> datetime.MAXYEAR
      9999

      >>> datetime.MINYEAR <= d.year <= datetime.MAXYEAR
      True
      >>> 1 <= d.month <= 12
      True
      >>> 1 <= d.day <= 31
      True

  باید توجه داشت که مقدار این سه attribute پس از نمونه‌سازی قابل تغییر نخواهد بود و به اصطلاح read-only هستند::

    >>> d.year = 2022
    Traceback (most recent call last):
      File "<stdin>", line 1, in <module>
    AttributeError: attribute 'year' of 'datetime.date' objects is not writable

|

**۲- با استفاده از کلاس متد** ``fromisoformat(date_string)`` [`اسناد پایتون <https://docs.python.org/3/library/datetime.html#datetime.date.fromisoformat>`__] از کلاس ``datetime.date`` (البته از نسخه 3.7 پایتون به بعد)، در تعریف این متد یک پارامتر از نوع ``str`` قرار داده شده است و این متد یک تاریخ را بر اساس قالب استاندارد ISO 8601 [`ویکی‌پدیا <https://en.wikipedia.org/wiki/ISO_8601>`__] دریافت و یک شی معادل از کلاس ``datetime.date`` را برمی‌گرداند. این قالب برابر ``YYYY-MM-DD`` می‌باشد که از سمت چپ معرف چهار رقم سال، یک خط تیره، دو رقم ماه، یک خط تیره و دو رقم روز ماه می‌باشد؛ همانند: ``07-04-2020``::

    >>> import datetime
    >>> d = datetime.date.fromisoformat('2021-04-07')

::

    >>> from datetime import date
    >>> d = date.fromisoformat('2021-04-07')

|

**۳- با استفاده از کلاس متد** ``(ordinal)fromordinal`` [`اسناد پایتون <https://docs.python.org/3/library/datetime.html#datetime.date.fromordinal>`__] از کلاس ``datetime.date``، در تعریف این متد یک پارامتر از نوع ``int`` قرار داده شده است که در واقع این متد معادل یک proleptic Gregorian ordinal [`ویکی‌پدیا <https://en.wikipedia.org/wiki/Proleptic_Gregorian_calendar>`__] یک تاریخ مشخص را دریافت و یک شی معادل از کلاس ``datetime.date`` را برمی‌گرداند. این مقدار برابر شمارش تعداد روزها از تاریخ یکم ژانویه سال یک میلادی تا تاریخ مورد نظر می‌باشد::


    >>> import datetime
    >>> d = datetime.date.fromordinal(737887)

::

    >>> from datetime import date
    >>> d = date.fromordinal(737887)



|

**۴- با استفاده از کلاس متد** ``(timestamp)fromtimestamp`` [`اسناد پایتون <https://docs.python.org/3/library/datetime.html#datetime.date.fromtimestamp>`__] از کلاس ``datetime.date``، در تعریف این متد یک پارامتر از نوع ``int`` قرار داده شده است که در واقع این متد معادل POSIX timestamp [`ویکی‌پدیا <https://en.wikipedia.org/wiki/Unix_time>`__] یک تاریخ مشخص را دریافت و یک شی معادل از کلاس ``datetime.date`` را برمی‌گرداند. این مقدار برابر شمارش تعداد ثانیه‌ها به منطقه زمانی UTC از ساعت ۰۰:۰۰:۰۰ یکم ژانویه سال ۱۹۷۰ میلادی تا تاریخ مورد نظر می‌باشد::


    >>> import datetime
    >>> d = datetime.date.fromtimestamp(1617737400)

::

    >>> from datetime import date
    >>> d = date.fromtimestamp(1617737400)

توجه داشته باشید استفاده از این متد تنها محدود به سال‌های مابین ۱۹۷۰ تا ۲۰۳۸ می‌باشد. چرا که این متد از تابع localtime یا gmtime در زبان برنامه‌نویسی C استفاده می‌کند که از سال ۲۰۳۸ به بعد مقدار timestamp از نوع signed 32-bit integer در این زبان، Overflow خواهد داشت! [`ویکی‌پدیا: Year 2038 problem <https://en.wikipedia.org/wiki/Year_2038_problem>`__]


|

**۵- با استفاده از کلاس متد** ``fromisocalendar`` [`اسناد پایتون <https://docs.python.org/3/library/datetime.html#datetime.date.fromisocalendar>`__] از کلاس ``datetime.date`` (البته از نسخه 3.8 پایتون به بعد)، در تعریف این متد سه پارامتر از نوع ``int`` قرار داده شده است که از سمت چپ به ترتیب معرف سال، شماره هفته در سال و شماره روز از هفته مورد نظر می‌باشند. در واقع این متد معادل ISO calendar [`ویکی‌پدیا <https://en.wikipedia.org/wiki/ISO_week_date>`__] یک تاریخ مشخص را دریافت و یک شی معادل از کلاس ``datetime.date`` را برمی‌گرداند. در این استاندارد، یک سال تقریبا شامل ۵۲ هفته می‌باشد که روزهای هر هفته نیز از روز دوشنبه (Monday) با شماره یک محاسبه می‌گردد (دوشنبه:۱، سه‌شنبه:۲، ... یکشنبه:۷)::

     fromisocalendar(year, week, day)

::


    >>> import datetime
    >>> d = datetime.date.fromisocalendar(2021, 14, 3) # Wednesday, April 7, 2021

::

    >>> from datetime import date
    >>> d = date.fromisocalendar(2021, 14, 3) # Wednesday, April 7, 2021



.. _python-comparing-date-objects: 

مقایسه دو شی ``date``
----------------------------
دو شی ``datetime.date`` پایتون قابلیت مقایسه با یکدیگر را دارند. همچنین می‌توان با استفاده از یک شی ``datetime.timedelta`` مقدار یک شی ``date`` را به جلو یا عقب هدایت کرد:

 
::

    >>> from datetime import date, timedelta

    >>> today = date(2021, 4, 9)

    >>> yesterday = today - timedelta(days=1)
    >>> yesterday
    datetime.date(2021, 4, 8)

    >>> today > yesterday
    True
    >>> today == today
    True
    >>> today < yesterday
    False
    >>> today == yesterday + timedelta(days=1)
    True

    >>> today - yesterday
    datetime.timedelta(days=1)

توجه داشته باشید حاصل تفاضل دو شی تاریخ پایتون یک شی از نوع ``datetime.timedelta`` خواهد بود!


.. _python-date-methods: 

متدهای شی ``date``
----------------------------

برخی از Instance methodهای یک شی ``datetime.date`` پایتون به شرح زیر هستند:


* **متد** ``toordinal`` [`اسناد پایتون <https://docs.python.org/3/library/datetime.html#datetime.date.toordinal>`__]: معادل proleptic Gregorian ordinal از مقدار تاریخ شی را برمی‌گرداند::

    >>> from datetime import date

    >>> today = date(2021, 4, 9)
    >>> today.toordinal()
    737889



* **متد** ``isoformat`` [`اسناد پایتون <https://docs.python.org/3/library/datetime.html#datetime.date.isoformat>`__]: معادل مقدار تاریخ شی را در قالب استاندارد ISO 8601 برمی‌گرداند::

    >>> from datetime import date

    >>> today = date(2021, 4, 9)
    >>> today.isoformat()
    '2021-04-09'


* **متد** ``isocalendar`` [`اسناد پایتون <https://docs.python.org/3/library/datetime.html#datetime.date.isocalendar>`__]: معادل ISO calendar از مقدار تاریخ شی را برمی‌گرداند::

    >>> from datetime import date

    >>> today = date(2021, 4, 9) # Friday, April 9, 2021
    >>> today.isocalendar()
    (2021, 14, 5)

  از پایتون نسخه 3.9 نوع خروجی این متد به صورت زیر تغییر کرده است::


    >>> today.isocalendar()
    datetime.IsoCalendarDate(year=2021, week=14, weekday=5)



* **متد** ``weekday`` [`اسناد پایتون <https://docs.python.org/3/library/datetime.html#datetime.date.isocalendar>`__]: شماره روز از هفته جاری را برمی‌گرداند. دوشنبه:صفر، سه‌شنبه:۱ ... یک‌شنبه:۶::

    >>> from datetime import date

    >>> today = date(2021, 4, 9) # Friday, April 9, 2021
    >>> today.weekday()
    4



* **متد** ``isoweekday`` [`اسناد پایتون <https://docs.python.org/3/library/datetime.html#datetime.date.isoweekday>`__]: شماره روز از هفته جاری را بر اساس استاندارد ISO calendar برمی‌گرداند. دوشنبه:۱، سه‌شنبه:۲ ... یک‌شنبه:۷::

    >>> from datetime import date

    >>> today = date(2021, 4, 9) # Friday, April 9, 2021
    >>> today.isoweekday()
    5




* **متد** ``replace`` [`اسناد پایتون <https://docs.python.org/3/library/datetime.html#datetime.date.replace>`__]: با استفاده از این متد می‌توان یک شی ``date`` جدید همانند شی جاری ایجاد کرد ولی با کمی تغییرات::

    replace(year, month, day)

  ::

    >>> from datetime import date

    >>> today = date(2021, 4, 9)

    >>> another_day = today.replace(day=22)
    >>> another_day
    datetime.date(2021, 4, 22)



* **متد** ``today`` [`اسناد پایتون <https://docs.python.org/3/library/datetime.html#datetime.date.today>`__]: جدا از اینکه شی موجود حاوی چه تاریخی است، یک شی تاریخ جدید بر اساس تاریخ روز جاری - با توجه به تنظیمات سیستم‌ - برمی‌گرداند::

    >>> from datetime import date

    >>> d = date(2021, 4, 9)
    >>> d.today()
    datetime.date(2021, 4, 10)


* **متد** ``(format)strftime`` [`اسناد پایتون <https://docs.python.org/3/library/datetime.html#datetime.date.strftime>`__]: این متد بسیار پرکاربرد است و عملکرد آن به این صورت می‌باشد که یک قالب (format) را دریافت و معادل ``str`` از شی مورد نظر را بر اساس ساختار آن قالب برمی‌گردادند. ساختار قالب در اینجا با آنچه توسط استاندارد ISO 8601 مطرح شده است کمی متفاوت می‌باشد که در انتهای این درس مورد بررسی قرار خواهد گرفت.





کلاس ``datetime.time``
~~~~~~~~~~~~~~~~~~~~~~~~~~~

این کلاس [`اسناد پایتون <https://docs.python.org/3/library/datetime.html#time-objects>`__] نمایش ایجاد یک شی ساعت در لحظه‌ای مشخص از شبانه‌روز در زبان برنامه‌نویسی پایتون می‌باشد. در واقع کاربرد این شی، نگهداری از اطلاعات مربوط به یک ساعت مشخص خواهد بود (همچون: ساعت، دقیقه، ثانیه و...). در ادامه این بخش به بررسی چگونگی ایجاد این نوع شی و اجزای آن خواهیم پرداخت.


.. _python-create-time-objects: 

ایجاد شی ``time``
------------------

به دو شیوه زیر می‌توان یک شی از نوع ``datetime.time`` ایجاد کرد:

::

     >>> import datetime

     >>> t = datetime.time(hour=10, minute=4, second=30)
     >>> t = datetime.time.fromisoformat('10:04:30')  # Python 3.7

     >>> t
     datetime.time(10, 4, 30)
     >>> type(t)
     <class 'datetime.time'>

     >>> t.hour
     10
     >>> t.minute
     4
     >>> t.second
     30
     >>> t.microsecond
     0
     >>> print(t.tzinfo)
     None
     >>> t.fold
     0



**۱- با استفاده از نمونه‌سازی**::

    time(hour=0, minute=0, second=0, microsecond=0, tzinfo=None, *, fold=0)

::


    >>> import datetime
    >>> t = datetime.time(22, 4, 30)



همانطور که از تعریف این کلاس مشخص است، برای نمونه‌سازی از کلاس ``datetime.time`` می‌توان  شش Instance attribute آن را مقداردهی نماییم. این شش attribute که همگی اختیاری و دارای مقدار پیش‌فرض هستند عبارتند از:

* ``hour``: از نوع ``int`` می‌باشد و مقداری برابر با ساعت مورد نظر خواهد داشت. این مقدار می‌بایست  عددی از بین اعداد ``0`` تا ``24`` باشد : range(24)

* ``minute``: از نوع ``int`` می‌باشد و مقداری برابر با دقیقه مورد نظر خواهد داشت که می‌بایست عددی از بین اعداد ``0`` تا ``60`` باشد : range(60)

* ``second``: از نوع ``int`` می‌باشد و مقداری برابر با ثانیه مورد نظر خواهد داشت که می‌بایست عددی از بین اعداد ``0`` تا ``60`` باشد : range(60)

* ``microsecond``: از نوع ``int`` می‌باشد و مقداری برابر با میکروثانیه مورد نظر خواهد داشت که می‌بایست عددی از بین اعداد ``0`` تا ``1000000`` باشد : range(1000000) - هر میکروثانیه برابر با 0.000001 ثانیه می‌باشد.

* ``tzinfo``: معرف منطقه زمانی (Time zone) است که مقدار پیش‌فرض آن ``None`` می‌باشد و می‌تواند یک شی از  زیرکلاس‌های (subclass) کلاس ``tzinfo`` [`اسناد پایتون <https://docs.python.org/3/library/datetime.html#datetime.tzinfo>`__] را بپذیرد.

* ``fold``: از نسخه 3.6 پایتون به بعد اضافه شده است و تنها با استفاده از شیوه **نام=مقدار** قابل مقداردهی می‌باشد. این پارامتر در واقع یک نشانگر برای ابهام‌زدایی در بیان ساعت می‌باشد. برای مثال از کاربرد این پارامتر وضعیت «ساعت تابستانی» [`ویکی‌پدیا <https://en.wikipedia.org/wiki/Daylight_saving_time>`__] را تصور کنید. ساعت رسمی ایران هر سال در ساعت ۲۴ روز اول فروردین ماه یک ساعت به جلو کشیده می‌شود و در ساعت ۲۴ روز سی‌ام شهریور ماه به حالت قبلی برگردانده می‌شود، اکنون در روز سی‌ام شهریور ماه ساعت ۲۳ تا ۲۴ دوبار تکرار می‌شود، در این مواقع می‌توان از این پارامتر برای مشخص کردن وضعیت ساعت استفاده کرد. به این صورت که مقدار ``0`` بیانگر وضعیت قبل از تغییر و ``1`` بیانگر وضعیت پس از تغییر می‌تواند باشد.

  باید توجه داشت که مقدار این شش attribute پس از نمونه‌سازی قابل تغییر نخواهد بود و به اصطلاح read-only هستند::

    >>> t.hour = 14
    Traceback (most recent call last):
      File "<stdin>", line 1, in <module>
    AttributeError: attribute 'hour' of 'datetime.time' objects is not writable


|

**۲- با استفاده از کلاس متد** ``(time_string)fromisoformat`` [`اسناد پایتون <https://docs.python.org/3/library/datetime.html#datetime.time.fromisoformat>`__] از کلاس ``datetime.time`` (البته از نسخه 3.7 پایتون به بعد)، در تعریف این متد یک پارامتر از نوع ``str`` قرار داده شده است که در واقع این متد یک ساعت را براساس قالب کلی استاندارد ISO 8601 [`ویکی‌پدیا <https://en.wikipedia.org/wiki/ISO_8601>`__] دریافت و یک شی معادل از کلاس ``datetime.time`` را برمی‌گرداند. این قالب معمولا برابر ``hh:mm:ss`` می‌باشد که از سمت چپ معرف دو رقم ساعت، دونقطه (colon)، دو رقم دقیقه، دونقطه (colon) و دو رقم ثانیه می‌باشد؛ همانند: ``04:23:01`` - قالب‌های قابل پذیرش به صورت زیر خواهند بود::

    >>> import datetime
    
::

    >>> t = datetime.time.fromisoformat('04') # 'HH'
    >>> t
    datetime.time(4, 0)

::

    >>> t = datetime.time.fromisoformat('04:23') # 'HH:MM'
    >>> t
    datetime.time(4, 23)

::


    >>> t = datetime.time.fromisoformat('04:23:01') # 'HH:MM:SS'
    >>> t
    datetime.time(4, 23, 1)
    
::

    >>> t = datetime.time.fromisoformat('04:23:01.000384') # 'HH:MM:SS.ffffff'
    >>> t
    datetime.time(4, 23, 1, 384)

::

    >>> t = datetime.time.fromisoformat('04:23:01+04:30') # 'HH:MM:SS+HH:MM'
    >>> t
    datetime.time(4, 23, 1, tzinfo=datetime.timezone(datetime.timedelta(seconds=16200)))

::

    >>> t = datetime.time.fromisoformat('04:23:01.000384+04:30') # 'HH:MM:SS.ffffff+HH:MM'
    >>> t
    datetime.time(4, 23, 1, 384, tzinfo=datetime.timezone(datetime.timedelta(seconds=16200)))

::

    >>> t = datetime.time.fromisoformat('04+04:30') # 'HH+HH:MM'
    >>> t
    datetime.time(4, 0, tzinfo=datetime.timezone(datetime.timedelta(seconds=16200)))


.. _python-comparing-time-objects: 

مقایسه دو شی ``time``
----------------------------

دو شی ``datetime.time`` پایتون قابلیت مقایسه با یکدیگر را دارند اگر هر دو naive یا هر دو aware باشند:


::

    >>> from datetime import time

    >>> t_22 = time(22, 0, 0)
    >>> t_20 = time(20, 0, 0)

    >>> t_22 > t_20
    True
    >>> t_22 == t_22
    True
    >>> t_22 < t_20
    False

به مثالی دیگر توجه نمایید (دو شی aware)::

    >>> from datetime import timedelta, timezone, time

    >>> tz_et = timezone(timedelta(hours=-5), 'Eastern Time Zone')
    >>> tz_ir = timezone(timedelta(hours=4, minutes=30), 'Asia/Tehran')

    >>> t_et = time(12, 0, 0, tzinfo=tz_et)
    >>> t_ir = time(12, 0, 0, tzinfo=tz_ir)

    >>> t_et == t_ir
    False
    >>> t_et > t_ir
    True
    >>> t_et < t_ir
    False

    >>> t_ir_new = time(21, 30, 0, tzinfo=tz_ir)

    >>> t_et == t_ir_new
    True


در کد بالا درست است که هر دو شی ``t_et`` و ``t_ir`` حاوی ساعت دوازده می‌باشند ولی باید به این نکته توجه داشت، در حالی ``t_et`` ساعت دوازده را نمایش می‌دهد که نسبت به منطقه زمانی مبنا (UTC) پنج ساعت عقب‌تر است؛ در واقع نه ساعت و سی دقیقه بعد، ``t_ir`` به زمانی خواهد رسید که ``t_et`` اکنون آن را نمایش می‌دهد!

همچنین توجه داشته باشید که نمی‌توان از عملگرهایی همچون ``-`` یا ``+`` برای اشیای ``datetime.time`` استفاده کرد.


.. _python-time-methods:

متدهای شی ``time``
----------------------------

برخی از Instance methodهای یک شی ``datetime.time`` پایتون به شرح زیر هستند:



* **متد** ``replace`` [`اسناد پایتون <https://docs.python.org/3/library/datetime.html#datetime.time.replace>`__]: با استفاده از این متد می‌توان یک شی ``time`` جدید همانند شی جاری ایجاد کرد ولی با کمی تغییرات::

    replace(hour, minute, second, microsecond, tzinfo, *, fold)

  ::

    >>> from datetime import time

    >>> t_22 = time(hour=22, minute=22, second=22)

    >>> t_20 = t_22.replace(hour=20, minute=20)
    >>> t_20
    datetime.time(20, 20, 22)

  به مثالی دیگر توجه نمایید::

      >>> from datetime import timedelta, timezone, time

      >>> tz = timezone(timedelta(hours=-5), 'Eastern Time Zone')
      >>> t = time(hour=22, minute=22, second=22, tzinfo=tz)
      >>> t
      datetime.time(22, 22, 22, tzinfo=datetime.timezone(datetime.timedelta(days=-1, seconds=68400), 'Eastern Time Zone'))


      >>> tz_teh = timezone(timedelta(hours=4, minutes=30), 'Asia/Tehran')
      >>> t.replace(tzinfo=tz_teh)
      datetime.time(22, 22, 22, tzinfo=datetime.timezone(datetime.timedelta(seconds=16200), 'Asia/Tehran'))

  باید توجه داشت که با تغییر منطقه زمانی یک شی ``datetime.time``، اطلاعات مربوط به ساعت، در آن تغییری نخواهند داشت. چرا که وظیفه این متد تنها جایگزینی مقادیر می‌باشد و با جایگزینی منطقه زمانی، تغییری در زمان ثبت شده ایجاد نمی‌گردد. 


* **متد** ``isoformat`` [`اسناد پایتون <https://docs.python.org/3/library/datetime.html#datetime.time.isoformat>`__]: معادل مقدار ساعت شی را در قالب استاندارد ISO 8601 برمی‌گرداند::

    
    isoformat(timespec='auto')

  این متد یک پارامتر اختیاری دارد که می‌تواند یکی از مقادیر ``milliseconds`` ``minutes`` ``hours`` ``auto`` ``microseconds`` را دریافت کند. مقدار این پارامتر قالب خروجی را مشخص می‌کند:

  ::

    >>> from datetime import time

    >>> t = time(hour=22, minute=4, second=30, microsecond=300)

    >>> t.isoformat()
    '22:04:30.000300'

    >>> t.isoformat('auto')
    '22:04:30.000300'

    >>> t.isoformat('hours')
    '22'

    >>> t.isoformat('minutes')
    '22:04'

    >>> t.isoformat('milliseconds')
    '22:04:30.000'

    >>> t.isoformat('microseconds')
    '22:04:30.000300'

* **متد** ``utcoffset`` [`اسناد پایتون <https://docs.python.org/3/library/datetime.html#datetime.time.utcoffset>`__]: اگر پارامتر ``tzinfo`` برابر ``None`` باشد، مقدار ``None`` و در غیر این صورت مقدار زیر را برمی‌گرداند::

        self.tzinfo.utcoffset(None)

* **متد** ``tzname`` [`اسناد پایتون <https://docs.python.org/3/library/datetime.html#datetime.time.tzname>`__]: اگر پارامتر ``tzinfo`` برابر ``None`` باشد، مقدار ``None`` و در غیر این صورت مقدار زیر را برمی‌گرداند::

     self.tzinfo.tzname(None)

::

    >>> from datetime import timedelta, timezone, time

    >>> tz = timezone(timedelta(hours=4, minutes=30), 'Asia/Tehran')
    >>> t = time(hour=22, minute=4, second=30, tzinfo=tz)

    >>> t.utcoffset()
    datetime.timedelta(seconds=16200)

    >>> t.tzname()
    'Asia/Tehran'


* **متد** ``(format)strftime`` [`اسناد پایتون <https://docs.python.org/3/library/datetime.html#datetime.time.strftime>`__]: این متد بسیار پرکاربرد است و عملکرد آن به این صورت می‌باشد که یک قالب (format) را دریافت و معادل ``str`` از شی مورد نظر را بر اساس ساختار آن قالب برمی‌گردادند. ساختار قالب در اینجا با آنچه توسط استاندارد ISO 8601 مطرح شده است کمی متفاوت می‌باشد که در انتهای این درس مورد بررسی قرار خواهد گرفت.


.. _python-time-naive-aware:

naive / aware
----------------------------

یک شی ``datetime.time`` (به عنوان مثال متغیر:‌ ``t``) از نوع aware خواهد بود اگر دو شرط زیر برای آن درست باشد:


* مقدار پارامتر ``t.zinfo`` مخالف ``None`` باشد.
* حاصل ``t.tzinfo.utcoffset(None)`` مخالف ``None`` باشد.




کلاس ``datetime.datetime``
~~~~~~~~~~~~~~~~~~~~~~~~~~~

اشیای این کلاس پرکاربردترین و رایج‌ترین نوع از ماژول datetime هستند چرا که به طور هم زمان نسبت به ساعت (Time) و تاریخ (Date) آگاهی دارند [`اسناد پایتون <https://docs.python.org/3/library/datetime.html#datetime-objects>`__]. اساس محاسبه تاریخ در این کلاس نیز همانند ``datetime.date`` بر اساس گاه‌شماری میلادی (Gregorian calendar) و اساس محاسبه ساعت نیز همانند کلاس ``datetime.time`` به ازای هر شبانه‌روز دقیقا برابر ``24*3600`` ثانیه می‌باشد.


.. _python-create-datetime-objects:

ایجاد شی ``datetime``
---------------------------

به یازده شیوه زیر می‌توان یک شی از نوع ``datetime.datetime`` ایجاد کرد که بنابر شرایط می‌توانید از آن‌ها بهره بگیرید:



**۱- با استفاده از نمونه‌سازی**:

الگوی ایجاد شی از این کلاس به صورت زیر است که پارامترهای موجود آن دقیقا برابر پارامترهای دو کلاس ``datetime.date`` و ``datetime.time`` می‌باشند::

        datetime(year, 
                 month, 
                 day, 
                 hour=0, 
                 minute=0, 
                 second=0, 
                 microsecond=0, 
                 tzinfo=None, *, fold=0)


یک نمونه استفاده::


    >>> import datetime
    >>> dt = datetime.datetime(year=2021, month=4, day=7, hour=23, minute=18)
    >>> dt
    datetime.datetime(2021, 4, 7, 23, 18)

تنها پارامترهای مربوط به تاریخ اجباری هستند و تمامی پارامترهای مربوط به ساعت همگی دارای مقدار پیش‌فرض هستند::

   >>> import datetime
   >>> dt = datetime.datetime(year=2021, month=4, day=7)
   >>> dt
   datetime.datetime(2021, 4, 7, 0, 0)

|

**۲- با استفاده از کلاس متد** ``today`` [`اسناد پایتون <https://docs.python.org/3/library/datetime.html#datetime.datetime.today>`__]، این متد زمان لحظه جاری سیستم را بدون امکان ثبت منطقه زمانی (``tzinfo=None``) در قالب یک شی از کلاس ``datetime.datetime`` برمی‌گرداند::


    >>> import datetime

    >>> datetime.datetime.today()
    datetime.datetime(2021, 4, 13, 21, 2, 0, 485083)

|

**۳- با استفاده از کلاس متد** ``(tz=None)now`` [`اسناد پایتون <https://docs.python.org/3/library/datetime.html#datetime.datetime.now>`__]، عملکرد این متد نیز همانند ``today`` می‌باشد با این تفاوت که می‌توان یک شی منطقه زمانی نیز به صورت آرگومان به آن ارسال و ثبت نمود::


    >>> import datetime

    >>> datetime.datetime.now()
    datetime.datetime(2021, 4, 13, 21, 2, 0, 485083)

::

    >>> import datetime
 
    >>> tz = datetime.timezone(datetime.timedelta(hours=4, minutes=30))
    >>> datetime.datetime.now(tz)
    datetime.datetime(2021, 4, 13, 21, 2, 0, 485083, tzinfo=datetime.timezone(datetime.timedelta(seconds=16200)))


توجه داشته باشید ارسال شی منطقه زمانی (``tz``) در نمونه کد بالا باعث تغییر در زمان نشد. علت این امر نیز مربوط به منطقه زمانی سیستمی است که برنامه بر روی آن اجرا می‌شود، در این سیستم منطقه زمانی بر روی ``04:30+UTC`` (وقت ساعت تابستانی، تهران) تنظیم بوده که کاملا برابر با مقدار ``tz`` ارسال شده می‌باشد.


|

**۴- با استفاده از کلاس متد** ``utcnow`` [`اسناد پایتون <https://docs.python.org/3/library/datetime.html#datetime.datetime.utcnow>`__]، خروجی این متد همانند خروجی ``datetime.now(timezone.utc)`` می‌باشد. یعنی زمان لحظه جاری سیستم را بر اساس منطقه زمانی UTC برمی‌گرداند ولی با این تفاوت که مقدار پارامتر ``tzinfo`` آن برابر ``None`` خواهد بود::


    >>> import datetime

    >>> datetime.datetime.now()
    datetime.datetime(2021, 4, 13, 21, 15, 33, 635410)

    >>> datetime.datetime.now(datetime.timezone.utc)
    datetime.datetime(2021, 4, 13, 16, 45, 33, 635410, tzinfo=datetime.timezone.utc)

::

    >>> import datetime

    >>> datetime.datetime.utcnow()
    datetime.datetime(2021, 4, 13, 16, 45, 33, 635410)



|

**۵- با استفاده از کلاس متد** ``fromtimestamp`` [`اسناد پایتون <hhttps://docs.python.org/3/library/datetime.html#datetime.datetime.fromtimestamp>`__]، در تعریف این متد یک پارامتر اختیاری (tz) از نوع ``tzinfo`` و یک پارامتر اجباری (timestamp) از نوع ``int`` قرار داده شده است. این متد معادل POSIX timestamp [`ویکی‌پدیا <https://en.wikipedia.org/wiki/Unix_time>`__] یک تاریخ مشخص را دریافت و یک شی معادل از کلاس ``datetime.datetime`` را برمی‌گرداند. این مقدار برابر شمارش تعداد ثانیه‌ها به منطقه زمانی UTC از ساعت ۰۰:۰۰:۰۰ یکم ژانویه سال ۱۹۷۰ میلادی تا تاریخ مورد نظر می‌باشد. ::


      fromtimestamp(timestamp, tz=None)


::


    >>> import datetime
    >>> datetime.datetime.fromtimestamp(1617737400)
    datetime.datetime(2021, 4, 7, 0, 0)

::

    >>> import datetime
    >>> datetime.datetime.fromtimestamp(1617737400, datetime.timezone.utc)
    datetime.datetime(2021, 4, 6, 19, 30, tzinfo=datetime.timezone.utc)

توجه داشته باشید استفاده از این متد تنها محدود به سال‌های مابین ۱۹۷۰ تا ۲۰۳۸ می‌باشد. چرا که این متد از تابع localtime یا gmtime در زبان برنامه‌نویسی C استفاده می‌کند که از سال ۲۰۳۸ به بعد مقدار timestamp از نوع signed 32-bit integer در این زبان، Overflow خواهد داشت! [`ویکی‌پدیا: Year 2038 problem <https://en.wikipedia.org/wiki/Year_2038_problem>`__]




|

**۶- با استفاده از کلاس متد** ``(timestamp)utcfromtimestamp`` [`اسناد پایتون <https://docs.python.org/3/library/datetime.html#datetime.datetime.utcfromtimestamp>`__]، خروجی این متد نیز همانند خروجی کلاس متد زیر بوده و معادل POSIX timestamp یک تاریخ مشخص را دریافت و یک شی معادل از کلاس ``datetime.datetime`` را بر مبنای منطقه زمانی UTC برمی‌گرداند. ولی با این تفاوت که مقدار پارامتر ``tzinfo`` آن برابر ``None`` خواهد بود::


      fromtimestamp(timestamp, datetime.timezone.utc)

::


    >>> import datetime
    >>> datetime.datetime.utcfromtimestamp(1617737400)
    datetime.datetime(2021, 4, 6, 19, 30)

توجه داشته باشید استفاده از این متد تنها محدود به سال‌های مابین ۱۹۷۰ تا ۲۰۳۸ می‌باشد. چرا که این متد از تابع localtime یا gmtime در زبان برنامه‌نویسی C استفاده می‌کند که از سال ۲۰۳۸ به بعد مقدار timestamp از نوع signed 32-bit integer در این زبان، Overflow خواهد داشت! [`ویکی‌پدیا: Year 2038 problem <https://en.wikipedia.org/wiki/Year_2038_problem>`__]


|

**۷- با استفاده از کلاس متد** ``(ordinal)fromordinal`` [`اسناد پایتون <https://docs.python.org/3/library/datetime.html#datetime.datetime.fromordinal>`__]، در تعریف این متد یک پارامتر از نوع ``int`` قرار داده شده است که در واقع این متد معادل یک proleptic Gregorian ordinal [`ویکی‌پدیا <https://en.wikipedia.org/wiki/Proleptic_Gregorian_calendar>`__] یک تاریخ مشخص را دریافت و یک شی معادل از کلاس ``datetime.datetime`` را برمی‌گرداند. این مقدار برابر شمارش تعداد روزها از تاریخ یکم ژانویه سال یک میلادی تا تاریخ مورد نظر می‌باشد. باید توجه داشت مقادیر مربوط به ساعت همانند minute ،hour یا ``tzinfo`` شی ایجاد شده برابر ``None`` خواهد بود::


    >>> import datetime
    >>> datetime.datetime.fromordinal(737887)
    datetime.datetime(2021, 4, 7, 0, 0)


|

**۸- با استفاده از کلاس متد** ``fromisocalendar`` [`اسناد پایتون <https://docs.python.org/3/library/datetime.html#datetime.datetime.fromisocalendar>`__] (البته از نسخه 3.8 پایتون به بعد)، در تعریف این متد سه پارامتر از نوع ``int`` قرار داده شده است که از سمت چپ به ترتیب معرف سال، شماره هفته در سال و شماره روز از هفته مورد نظر می‌باشند. در واقع این متد معادل ISO calendar [`ویکی‌پدیا <https://en.wikipedia.org/wiki/ISO_week_date>`__] یک تاریخ مشخص را دریافت و یک شی معادل از کلاس ``datetime.datetime`` را برمی‌گرداند. در این استاندارد، یک سال تقریبا شامل ۵۲ هفته می‌باشد که روزهای هر هفته نیز از روز دوشنبه (Monday) با شماره یک محاسبه می‌گردد (دوشنبه:۱، سه‌شنبه:۲، ... یکشنبه:۷). باید توجه داشت مقادیر مربوط به ساعت همانند minute ،hour یا ``tzinfo`` شی ایجاد شده برابر ``None`` خواهد بود::


      fromisocalendar(year, week, day)

::

    >>> import datetime
    >>> datetime.datetime.fromisocalendar(2021, 14, 3) # Wednesday, April 7, 2021
    datetime.datetime(2021, 4, 7, 0, 0)


|

**۹- با استفاده از کلاس متد** ``combine(date, time, tzinfo)`` [`اسناد پایتون <https://docs.python.org/3/library/datetime.html#datetime.datetime.combine>`__]، در تعریف این متد سه پارامتر قرار داده شده است که از سمت چپ به ترتیب از نوع ``datetime.time`` ،``datetime.date`` و ``datetime.tzinfo`` می‌باشند. در واقع این متد یک شی ``datetime.date`` و ``datetime.time`` جداگانه را دریافت و با یکدیگر ترکیب و یک شی ``datetime.datetime`` تولید می‌کند. پارامتر ``tzinfo`` اختیاری بوده و از نسخه 3.6 پایتون به این متد اضافه گردیده است که در صورت ارسال آرگومان متناظر به آن، این مقدار به عنوان منطقه زمانی شی خروجی در نظر گرفته خواهد شد؛ در غیر این صورت از منطقه زمانی شی ``datetime.time`` استفاده خواهد شد::

    >>> import datetime

    >>> d = datetime.date(2021, 4, 7)
    >>> t = datetime.time(hour=22, minute=4, second=30, tzinfo=datetime.timezone.utc)

    >>> datetime.datetime.combine(d, t)
    datetime.datetime(2021, 4, 7, 22, 4, 30, tzinfo=datetime.timezone.utc)

|

**۱۰- با استفاده از کلاس متد** ``fromisoformat(date_string)`` [`اسناد پایتون <https://docs.python.org/3/library/datetime.html#datetime.datetime.fromisoformat>`__] (البته از نسخه 3.7 پایتون به بعد)، در تعریف این متد یک پارامتر از نوع ``str`` قرار داده شده است و این متد یک زمان مشخص را بر اساس قالب استاندارد ISO 8601 [`ویکی‌پدیا <https://en.wikipedia.org/wiki/ISO_8601>`__] دریافت و یک شی معادل از کلاس ``datetime.datetime`` را برمی‌گرداند::

    YYYY-MM-DD[*HH[:MM[:SS[.fff[fff]]]][+HH:MM[:SS[.ffffff]]]]

الگوی بالا حالت‌های قابل پذیرش از قالب استاندارد ISO 8601 را برای این متد نمایش می‌دهد که در این الگو به جای ``*`` هر کاراکتری می‌تواند قرار بگیرد و بخش‌های داخل براکت (``[]``) اختیاری هستند. به چند نمونه کد زیر نیز توجه نمایید: 

::

    >>> from datetime import datetime

    >>> datetime.fromisoformat('2011-11-04T00:05:23') # YYYY-MM-DDTHH:MM:SS
    datetime.datetime(2011, 11, 4, 0, 5, 23)

    >>> datetime.fromisoformat('2011-11-04 00:05:23') # YYYY-MM-DD HH:MM:SS
    datetime.datetime(2011, 11, 4, 0, 5, 23)

    >>> datetime.fromisoformat('2011-11-04 00:05:23.283+00:00') # YYYY-MM-DD HH:MM:SS.fff+HH:MM
    datetime.datetime(2011, 11, 4, 0, 5, 23, 283000, tzinfo=datetime.timezone.utc)

    >>> datetime.fromisoformat('2011-11-04 00:05:23.283+04:30') # YYYY-MM-DD HH:MM:SS.fff+HH:MM
    datetime.datetime(2011, 11, 4, 0, 5, 23, 283000, tzinfo=datetime.timezone(datetime.timedelta(seconds=16200)))



|

**۱۱- با استفاده از کلاس متد** ``strptime`` [`اسناد پایتون <https://docs.python.org/3/library/datetime.html#datetime.datetime.strptime>`__]، تعریف این متد به صورت زیر می‌باشد::

    datetime.strptime(date_string, format)

این متد بسیار پرکاربرد بوده و عملکرد آن به این صورت می‌باشد که یک زمان مشخص را از نوع ``str`` به همراه قالب آن زمان دریافت و یک شی از کلاس ``datetime.datetime`` برمی‌گرداند. ساختار قالب در اینجا با آنچه توسط استاندارد ISO 8601 مطرح شده است کمی متفاوت می‌باشد که در انتهای این درس مورد بررسی قرار خواهد گرفت.


.. _python-comparing-datetime-objects:

مقایسه دو شی ``datetime``
----------------------------
دو شی ``datetime.datetime`` پایتون قابلیت مقایسه با یکدیگر را دارند اگر هر دو naive یا هر دو aware باشند. همچنین می‌توان با استفاده از یک شی ``datetime.timedelta`` مقدار یک شی ``datetime`` را به جلو یا عقب هدایت کرد:

 
::

    >>> from datetime import datetime, timedelta

    >>> today = datetime(2021, 4, 15, 8, 20)

    >>> yesterday = today - timedelta(days=1)
    >>> yesterday
    datetime.datetime(2021, 4, 14, 8, 20)

    >>> today == today
    True
    >>> today > yesterday
    True
    >>> today < yesterday
    False
    >>> today == yesterday + timedelta(days=1)
    True

    >>> today - yesterday
    datetime.timedelta(days=1)

توجه داشته باشید حاصل تفاضل دو شی ``datetime`` پایتون یک شی از نوع ``datetime.timedelta`` خواهد بود!

به مثالی دیگر توجه نمایید::

    >>> from datetime import timedelta, timezone, datetime

    >>> tz_et = timezone(timedelta(hours=-5), 'Eastern Time Zone')
    >>> tz_ir = timezone(timedelta(hours=4, minutes=30), 'Asia/Tehran')

    >>> dt_et = datetime(2021, 4, 15, 12, 0, 0, tzinfo=tz_et)
    >>> dt_ir = datetime(2021, 4, 15, 12, 0, 0, tzinfo=tz_ir)

    >>> dt_et == dt_ir
    False
    >>> dt_et > dt_ir
    True
    >>> dt_et < dt_ir
    False

    >>> dt_ir_new = datetime(2021, 4, 15, 21, 30, 0, tzinfo=tz_ir)

    >>> dt_et == dt_ir_new
    True


در کد بالا درست است که هر دو شی ``t_et`` و ``t_ir`` حاوی یک تاریخ و یک ساعت (``12:00:00 15-04-2021``) می‌باشند ولی باید به این نکته توجه داشت، در حالی ``t_et`` ساعت دوازده را نمایش می‌دهد که نسبت به منطقه زمانی مبنا (UTC) پنج ساعت عقب‌تر است؛ در واقع نه ساعت و سی دقیقه بعد، ``t_ir`` به زمانی خواهد رسید که ``t_et`` اکنون آن را نمایش می‌دهد!


.. _python-datetime-methods:

متدهای شی ``datetime``
----------------------------

برخی از Instance methodهای یک شی ``datetime.datetime`` پایتون به شرح زیر هستند:


* **متد** ``date`` [`اسناد پایتون <https://docs.python.org/3/library/datetime.html#datetime.datetime.date>`__]: بخش تاریخ از شی مورد نظر را در قالب یک شی ``datetime.date`` برمی‌گرداند::

    >>> import datetime
    >>> dt = datetime.datetime(2021, 4, 15, 12, 0, 0, tzinfo=datetime.timezone.utc)
    >>> dt.date()
    datetime.date(2021, 4, 15)


* **متد** ``time`` [`اسناد پایتون <https://docs.python.org/3/library/datetime.html#datetime.datetime.time>`__]: بخش ساعت از شی مورد نظر را در قالب یک شی ``datetime.time``، بدون مقدار ``tzinfo`` برمی‌گرداند::

    >>> import datetime
    >>> dt = datetime.datetime(2021, 4, 15, 12, 0, 0, tzinfo=datetime.timezone.utc)
    >>> dt.time()
    datetime.time(12, 0)

    >>> print(dt.time().tzinfo)
    None


* **متد** ``timetz`` [`اسناد پایتون <https://docs.python.org/3/library/datetime.html#datetime.datetime.timetz>`__]: بخش ساعت از شی مورد نظر را در قالب یک شی ``datetime.time``، به همراه مقدار ``tzinfo`` برمی‌گرداند::

    >>> import datetime
    >>> dt = datetime.datetime(2021, 4, 15, 12, 0, 0, tzinfo=datetime.timezone.utc)
    >>> dt.timetz()
    datetime.time(12, 0, tzinfo=datetime.timezone.utc)

    >>> print(dt.timetz().tzinfo)
    UTC



* **متد** ``astimezone(tz=None)`` [`اسناد پایتون <https://docs.python.org/3/library/datetime.html#datetime.datetime.astimezone>`__]: با استفاده از این متد می‌توان منطقه زمانی شی مورد نظر را تغییر و به صورت یک شی جدید ``datetime.datetime`` دریافت کرد::

    >>> import datetime
    >>> dt = datetime.datetime(2021, 4, 15, 12, 0, 0, tzinfo=datetime.timezone.utc)
    >>> dt
    datetime.datetime(2021, 4, 15, 12, 0, tzinfo=datetime.timezone.utc)

    >>> tz_ir = datetime.timezone(timedelta(hours=4, minutes=30), 'Asia/Tehran')
    >>> dt.astimezone(tz_ir)
    datetime.datetime(2021, 4, 15, 16, 30, tzinfo=datetime.timezone(datetime.timedelta(seconds=16200), 'Asia/Tehran'))


* **متد** ``utcoffset`` [`اسناد پایتون <https://docs.python.org/3/library/datetime.html#datetime.datetime.utcoffset>`__]: اگر پارامتر ``tzinfo`` برابر ``None`` باشد، مقدار ``None`` و در غیر این صورت مقدار ``self.tzinfo.utcoffset(self)`` را برمی‌گرداند.

* **متد** ``tzname`` [`اسناد پایتون <https://docs.python.org/3/library/datetime.html#datetime.datetime.tzname>`__]: اگر پارامتر ``tzinfo`` برابر ``None`` باشد، مقدار ``None`` و در غیر این صورت مقدار ``self.tzinfo.tzname(self)`` را برمی‌گرداند.

::

    >>> from datetime import timedelta, timezone, datetime

    >>> tz = timezone(timedelta(hours=4, minutes=30), 'Asia/Tehran')
    >>> dt = datetime(year=2021, month=4, day=15, hour=12, minute=0, tzinfo=tz)

    >>> dt.utcoffset()
    datetime.timedelta(seconds=16200)

    >>> dt.tzname()
    'Asia/Tehran'



* **متد** ``timestamp`` [`اسناد پایتون <https://docs.python.org/3/library/datetime.html#datetime.datetime.timestamp>`__]: معادل POSIX timestamp از زمان شی مورد نظر را در قالب یک شی ``float`` برمی‌گرداند::

    >>> import datetime

    >>> today = datetime.datetime(2021, 4, 15, 12, 0)
    >>> today.timestamp()
    1618471800.0

  توجه داشته باشید استفاده از این متد تنها محدود به سال‌های مابین ۱۹۷۰ تا ۲۰۳۸ می‌باشد. چرا که این متد از تابع localtime یا gmtime در زبان برنامه‌نویسی C استفاده می‌کند که از سال ۲۰۳۸ به بعد مقدار timestamp از نوع signed 32-bit integer در این زبان، Overflow خواهد داشت! [`ویکی‌پدیا: Year 2038 problem <https://en.wikipedia.org/wiki/Year_2038_problem>`__]


* **متد** ``toordinal`` [`اسناد پایتون <https://docs.python.org/3/library/datetime.html#datetime.datetime.toordinal>`__]: معادل proleptic Gregorian ordinal از شی مورد نظر را برمی‌گرداند::

    >>> import datetime

    >>> today = datetime.datetime(2021, 4, 15, 12, 0)
    >>> today.toordinal()
    737895



* **متد** ``weekday`` [`اسناد پایتون <https://docs.python.org/3/library/datetime.html#datetime.datetime.isocalendar>`__]: شماره روز از هفته جاری را برمی‌گرداند. دوشنبه:صفر، سه‌شنبه:۱ ... یک‌شنبه:۶::

    >>> import datetime

    >>> today = datetime.datetime(2021, 4, 15, 12, 0) # Thursday, April 15, 2021
    >>> today.weekday()
    3



* **متد** ``isoweekday`` [`اسناد پایتون <https://docs.python.org/3/library/datetime.html#datetime.datetime.isoweekday>`__]: شماره روز از هفته جاری را بر اساس استاندارد ISO calendar برمی‌گرداند. دوشنبه:۱، سه‌شنبه:۲ ... یک‌شنبه:۷::

    >>> import datetime

    >>> today = datetime.datetime(2021, 4, 15, 12, 0) # Thursday, April 15, 2021
    >>> today.isoweekday()
    4


* **متد** ``isocalendar`` [`اسناد پایتون <https://docs.python.org/3/library/datetime.html#datetime.datetime.isocalendar>`__]: معادل ISO calendar از مقدار تاریخ شی مورد نظر را برمی‌گرداند::

    >>> import datetime

    >>> today = datetime.datetime(2021, 4, 15, 12, 0) # Thursday, April 15, 2021
    >>> today.isocalendar()
    (2021, 15, 4)



  از پایتون نسخه 3.9 نوع خروجی این متد به صورت زیر تغییر کرده است::


    >>> today.isocalendar()
    datetime.IsoCalendarDate(year=2021, week=14, weekday=5)


* **متد** ``isoformat`` [`اسناد پایتون <https://docs.python.org/3/library/datetime.html#datetime.datetime.isoformat>`__]: معادل مقدار زمان ثبت شده در شی مورد نظر را در قالب استاندارد ISO 8601 برمی‌گرداند::

    >>> import datetime

    >>> today = datetime.datetime(2021, 4, 15, 12, 0)
    >>> today.isoformat()
    '2021-04-15T12:00:00'

  ::

      >>> today = datetime.datetime(2021, 4, 15, 12, 0, tzinfo=datetime.timezone.utc)
      >>> today.isoformat()
      '2021-04-15T12:00:00+00:00'



* **متد** ``replace`` [`اسناد پایتون <https://docs.python.org/3/library/datetime.html#datetime.datetime.replace>`__]: با استفاده از این متد می‌توان یک شی ``datetime.datetime`` جدید همانند شی جاری ایجاد کرد ولی با کمی تغییرات::

     replace(year, 
                 month, 
                 day, 
                 hour=0, 
                 minute=0, 
                 second=0, 
                 microsecond=0, 
                 tzinfo=None, *, fold=0)

  ::

    >>> import datetime
    >>> today = datetime.datetime(2021, 4, 15, 12, 0)

    >>> another_day = today.replace(day=22)
    >>> another_day
    datetime.datetime(2021, 4, 22, 12, 0)


  به مثالی دیگر توجه نمایید::

      >>> from datetime import timedelta, timezone, datetime

      >>> tz = timezone(timedelta(hours=-5), 'Eastern Time Zone')
      >>> dt = datetime(2021, 4, 15, 12, 0, tzinfo=tz)
      >>> dt
      datetime.datetime(2021, 4, 15, 12, 0, tzinfo=datetime.timezone(datetime.timedelta(days=-1, seconds=68400), 'Eastern Time Zone'))


      >>> tz_teh = timezone(timedelta(hours=4, minutes=30), 'Asia/Tehran')
      >>> dt.replace(tzinfo=tz_teh)
      datetime.datetime(2021, 4, 15, 12, 0, tzinfo=datetime.timezone(datetime.timedelta(seconds=16200), 'Asia/Tehran'))


  توجه داشته باشید که وظیفه این متد تنها جایگزینی مقادیر می‌باشد و با جایگزینی منطقه زمانی، تغییری در زمان ثبت شده ایجاد نمی‌گردد. 



* **متد** ``(format)strftime`` [`اسناد پایتون <https://docs.python.org/3/library/datetime.html#datetime.datetime.strftime>`__]: این متد بسیار پرکاربرد است و عملکرد آن به این صورت می‌باشد که یک قالب (format) را دریافت و معادل ``str`` از شی مورد نظر را بر اساس ساختار آن قالب برمی‌گردادند. ساختار قالب در اینجا با آنچه توسط استاندارد ISO 8601 مطرح شده است کمی متفاوت می‌باشد که در انتهای این درس مورد بررسی قرار خواهد گرفت.



.. _python-datetime-naive-aware:

naive / aware
----------------------------

یک شی ``datetime.datetime`` (به عنوان مثال متغیر:‌ ``dt``) از نوع aware خواهد بود اگر دو شرط زیر برای آن درست باشد:


* مقدار پارامتر ``dt.zinfo`` مخالف ``None`` باشد.
* حاصل ``dt.tzinfo.utcoffset(dt)`` مخالف ``None`` باشد.



متدهای ``strftime`` و ``strptime``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

پیش‌تر کمی با این دو متد پرکاربرد آشنا شده‌ایم، ولی به صورت خلاصه می‌توان این دو متد را اینگونه تعریف نمود:



**متد** ``strftime(format)``: یک Instance method بوده و از جانب هر سه نوع شی ``date`` ،``time`` و ``datetime`` پشتیبانی و قابل استفاده می‌باشد. این متد می‌تواند زمان شی مورد نظر را به یک قالب (format) مشخص از شی رشته ``str`` تبدیل نماید. str format time


**متد** ``strptime(date_string, format)``: یک Class method بوده و تنها از جانب کلاس ``datetime`` پشتیبانی و قابل استفاده می‌باشد. این متد می‌تواند زمان درج شده در یک قالب (format) مشخص از شی رشته ``str`` را تجزیه (Parse) و به یک شی ``datetime.datetime`` تبدیل نماید. str parse time

در تعریف این متدها، منظور از format یک رشته متنی است که بر اساس کدهای خاصی تشکیل شده است و همینطور date_string نیز یک رشته متنی حاوی زمان در قالب ارايه شده توسط format می‌باشد. به نمونه کد زیر توجه نمایید::


    >>> import datetime
    >>> today = datetime.datetime(2021, 4, 15, 12, 0, 0)
    >>> today.strftime('%Y-%m-%d %H:%M:%S')
    '2021-04-15 12:00:00'

::

    >>> import datetime
    >>> datetime.datetime.strptime('2021-04-15 12:00:00', '%Y-%m-%d %H:%M:%S')
    datetime.datetime(2021, 4, 15, 12, 0)


برای مشاهده فهرست کدهای قابل استفاده و مفهوم آن‌ها در format می‌توانید به [`اسناد پایتون <https://docs.python.org/3/library/datetime.html#strftime-and-strptime-format-codes>`__] مراجعه نمایید ولی برخی از موارد پر استفاده به شرح زیر می‌باشند:


* ``Y%``: نمایش سال به همراه قرن (چهار رقمی)

* ``y%``: نمایش سال بدون قرن (دو رقمی)

* ``m%``: نمایش شماره ماه به صورت دورقمی: 01 ... 12

* ``b%``: نمایش نام ماه به صورت اختصار: Jan ... Dec

* ``B%``: نمایش نام ماه به صورت کامل: January ... December

* ``d%``: نمایش شماره روز از ماه به صورت دو رقمی: 01 ... 31

* ``a%``: نمایش نام روز هفته به صورت اختصار: Sat ... Fri

* ``A%``: نمایش نام روز هفته به صورت کامل: Saturday ... Friday

* ``H%``: نمایش ساعت (در سیستم شمارش تا 24) به صورت دو رقمی: 00 ... 23

* ``I%``: نمایش ساعت (در سیستم شمارش تا 12) به صورت دو رقمی: 00 ... 12

* ``p%``: نمایش AM یا PM

* ``M%``: نمایش دقیقه به صورت دو رقمی: 00 ... 59

* ``S%``: نمایش ثانیه به صورت دو رقمی: 00 ... 59

* ``Z%``: نمایش نام منطقه زمانی : UTC ،GMT، ....

* ``%%``: نمایش یک کاراکتر ``%``


::

    >>> import datetime
    >>> today = datetime.datetime(2021, 4, 15, 12, 0, 0)
    >>> today.strftime('%b %d %Y %H:%M:%S')
    'Apr 15 2021 12:00:00'


::

    >>> import datetime
    >>> datetime.datetime.strptime('Apr 15 2021 12:00:00', '%b %d %Y %H:%M:%S')
    datetime.datetime(2021, 4, 15, 12, 0)



|

----

:emoji-size:`😊` امیدوارم مفید بوده باشه



