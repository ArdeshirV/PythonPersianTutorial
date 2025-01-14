.. role:: emoji-size

.. meta::
   :description: پایتون به پارسی - کتاب آنلاین و آزاد آموزش زبان برنامه‌نویسی پایتون - چالش کد پایتون، پایه
   :keywords: پایتون, آموزش, آموزش برنامه نویسی, آموزش پایتون, برنامه نویسی, کتاب آموزش, آموزش فارسی, کتاب آزاد 


.. _code-challenges-basic: 

چالش کد پایتون: پایه
==========================

زمان به چالش کشیدن دانش خود از پایتون رسیده است. در این بخش چند مسئله (بدون هیچ ترتیب خاصی) قرار داده شده است که شما می‌بایست برای آن‌ها یک راه حل پایتونی ارایه دهید. البته برای هر کدام، یک پاسخ نیز قرار داده شده است که در صورت تمایل می‌توانید راه حل خود را با آن مقایسه کنید یا از درستی نتیجه نهایی مطمئن گردید. به یاد داشته باشید همواره چندین راه حل برای حل یک مسئله وجود خواهد داشت.

پاسخ‌ها به صورت gist از سرویس GitHub قرار داده شده‌اند. بنابراین این امکان وجود دارد که نظر و یا راه حل خود را در مورد هر یک از مسئله‌ها، با دیگران نیز به اشتراک بگذارید.

موفق باشد :)


----

.. contents:: مسئله‌ها
    :depth: 2

----


.. _area-of-the-circle: 

مساحت دایره
------------------------------------

برنامه‌ای بنویسید که شعاع یک دایره را از کاربر دریافت و مساحت آن را محاسبه نماید.

.. raw:: html

    <div class="gist-container">
        <script src="https://gist.github.com/saeiddrv/dae7126a0bc86f8e4d58e1135e3eba79.js"></script>
    </div>



.. _divisible-by-8: 

اعداد بخش‌پذیر بر هشت
------------------------------------

برنامه‌ای بنویسید که یک عدد صحیح از کاربر دریافت و تمام اعداد صحیح و بخش‌پذیر بر 8 از یک تا آن عدد را چاپ نماید.


.. raw:: html

    <div class="gist-container">
        <script src="https://gist.github.com/saeiddrv/e6bc5fbc1724a0b5828bc6ab1cda3a25.js"></script>
    </div>


.. _female-student-avg: 

میانگین نمره دانش‌آموزان (فایل CSV)
------------------------------------

فایل [`students.csv </_static/practice/students.csv>`__]  را دانلود نمایید. این یک فایل CSV حاوی اطلاعات دانش آموزان یک کلاس است. بدون استفاده از ماژول ``csv`` پایتون، یک برنامه بنویسید که این فایل را پردازش و میانگین نمرات دانش آموزان دختر (Female) این کلاس را محاسبه کند.

.. raw:: html

    <div class="gist-container">
        <script src="https://gist.github.com/saeiddrv/e64a15b66b8b92f4aa27e451fa52aa1b.js"></script>
    </div>


.. _find-common-numbers:

اشتراک دو لیست از اعداد
------------------------------------

برنامه‌ای بنویسید که دو لیست از اعداد صحیح را از کاربر دریافت و سپس اعداد مشترک در هر دو لیست را چاپ نماید. (در هنگام ورود اعداد، آن‌ها را با استفاده از یک فضای خالی جدا نمایید)


نمونه::

    list 1 = [1, 2, 3, 4, 5, 6]
    list 2 = [1, 2, 5, 9, 8, 3, 4, 7]
    
    result = [1, 2, 3, 4, 5]

.. raw:: html

    <div class="gist-container">
        <script src="https://gist.github.com/saeiddrv/a2f022d255fa11bee90ff4997c4ffc9d.js"></script>
    </div>


.. _grade-converter:

تبدیل نمره
------------------------------------

برنامه‌ای بنویسید که نمره کاربر را از ورودی دریافت (مانند 72) و معادل حرفی آن (مانند C) را چاپ نماید.

* نمره‌هایی که بیشتر یا برابر 90 و کمتر یا برابر با 100 هستند: A
* نمره‌هایی که بیشتر یا برابر 80 و کمتر از 90 هستند: B
* نمره‌هایی که بیشتر یا برابر 70 و کمتر از 80 هستند: C
* نمره‌هایی که بیشتر یا برابر 60 و کمتر از 70 هستند: D
* نمره‌هایی که کمتر از 60 هستند: F


.. raw:: html

    <div class="gist-container">
        <script src="https://gist.github.com/saeiddrv/f7f473292a55fb60144c610f5e06cf53.js"></script>
    </div>


.. _max-min-diff:

تفاضل بزرگترین و کوچکترین عضو یک لیست از اعداد
----------------------------------------------------

برنامه‌ای بنویسید که یک لیست از اعداد صحیح را از کاربر دریافت و سپس تفاضل بین بزرگترین و کوچکترین عضو آن را محاسبه و در خروجی چاپ نماید. (در هنگام ورود اعداد، آن‌ها را با استفاده از یک فضای خالی جدا نمایید)

نمونه::

    [1, 5, 3, 2, 8, 16, 20, 18, 3, 0, 4]
    max = 20
    min = 0
    max - min = 20

.. raw:: html

    <div class="gist-container">
        <script src="https://gist.github.com/saeiddrv/2dc69d2172afbee354312568756beff1.js"></script>
    </div>


.. _n-plus-nn-plus-nnn:

محاسبه عبارت n+nn+nnn
----------------------------------------------------

برنامه‌ای بنویسید که یک عدد صحیح مانند n را از کاربر دریافت و سپس حاصل عبارت n+nn+nnn را محاسبه نماید. برای نمونه چنانچه کاربر عدد 2 را وارد کرد، حاصل عبارت 222+22+2 محاسبه و در خروجی نمایش داده شود: 246

.. raw:: html

    <div class="gist-container">
        <script src="https://gist.github.com/saeiddrv/37af43f0ce2b3a72b72a6f53594004e0.js"></script>
    </div>


.. _name-in-reverse-order:

وارونه‌سازی اسم
----------------------------------------------------

برنامه‌ای بنویسید که نام کاربر را از ورودی دریافت و سپس آن را وارونه کرده و در خروجی چاپ نماید. برای نمونه چنانچه کاربر saeid را وارد کرد، در خروجی مقدار dieas چاپ گردد.

.. raw:: html

    <div class="gist-container">
        <script src="https://gist.github.com/saeiddrv/345507e78ca020262609b394d89e8f81.js"></script>
    </div>


.. _palindrome-checker:

پالیندروم 
----------------------------------------------------

برنامه‌ای بنویسید که یک کلمه را از ورودی دریافت و سپس بررسی نماید که آن کلمه پالیندروم  (Palindrome) است یا خیر. کلمه‌ای پالیندروم  خواهد بود که با وارونه خودش برابر باشد مانند: Madam

.. raw:: html

    <div class="gist-container">
        <script src="https://gist.github.com/saeiddrv/3984d5731d1ed62251befba1746dba57.js"></script>
    </div>


.. _student-analysis:

گزارش دانش‌آموزان 
----------------------------------------------------

فایل [`students.csv </_static/practice/students.csv>`__]  را دانلود نمایید. این یک فایل CSV حاوی اطلاعات دانش آموزان یک کلاس است. بدون استفاده از ماژول ``csv`` پایتون، یک برنامه بنویسید که این فایل را پردازش و موارد روبرو را محاسبه نماید و در قالب یک شی دیکشنری بر روی خروجی نمایش دهد: کمترین سن دانش‌آموز، بیشترین سن دانش‌آموز، کمترین نمره و بالاترین نمره 

.. raw:: html

    <div class="gist-container">
        <script src="https://gist.github.com/saeiddrv/91dc2e2a137e92c20885604d36886a82.js"></script>
    </div>


.. _count-vowels:

شمارش حروف صدادار
----------------------------------------------------

برنامه‌ای بنویسید که یک متن از کاربر دریافت کرده، سپس تعداد حروف صدادار انگلیسی (Vowels) را در آن بشمارد و عدد حاصل را در خروجی نمایش دهد. حروف صدادار انگلیسی عبارتند از:  ``'a','e','i','o','u'``

.. raw:: html

    <div class="gist-container">
        <script src="https://gist.github.com/saeiddrv/c9e1480f1062654c53d830891bf4e7d6.js"></script>
    </div>



.. _khayyam-pascal-triangle:


رسم مثلث خیام-پاسکال
----------------------------------------------------

برنامه‌ای بنویسید که یک عدد صحیح از کاربر دریافت و مثلث خیام-پاسکال را تا عمق آن سطر محاسبه و رسم نماید. از طریق منابع مختلف، ویکی‌پدیا یا تصویر پایین (تا سطر 5)، می‌توانید با ساختار مثلث خیام-پاسکال [`ویکی‌پدیا <https://en.wikipedia.org/wiki/Pascal%27s_triangle>`__] آشنا شوید:

.. image:: /_static/practice/PascalTriangleAnimated2.gif
    :align: center

.. raw:: html

    <div class="gist-container">
        <script src="https://gist.github.com/saeiddrv/2b57267f8543089d306d7ea7127df42b.js"></script>
    </div>