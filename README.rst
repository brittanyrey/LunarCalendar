LunarCalendar: 一个农历-阳历转换器
==================================

.. image::
  https://img.shields.io/pypi/v/LunarCalendar.svg
  :target: https://pypi.python.org/pypi/LunarCalendar
  :alt: Last stable version (PyPI)

LunarCalendar 是一个农历-阳历的转换器, 包含了一些在中国常见的农历和国历的节假日。
由于韩国、日本的农历与中国是相同的，只是节假日有所不同，所以支持对韩国、日本节假日和语言的扩展。

转换器支持时间段从1900-2100, 如果需要更长的时间段，利用generate.htm生成的数据即可。转换器的实现，参考自 `Lunar-Solar-Calendar-Converter <https://github.com/isee15/Lunar-Solar-Calendar-Converter>`_.


特点
--------

* 支持的时间范围非常容易扩展
* 包含了农历节假日, 如: 中秋节
* 包含了每年不固定的节假日, 如: 母亲节(每年5月第2个星期日)
* 农历+国历的合法性检查


Install
--------

LunarCalendar can be installed from the PyPI with easy_install::

   $ easy_install LunarCalendar

Or pip::

   $ pip install LunarCalendar


Quickstart
----------

国历转农历:

.. code-block:: python

    import datetime
    from lunarcalendar import Converter, Solar, Lunar, DateNotExist

    solar = Solar(2018, 1, 1)
    print(solar)
    lunar = Converter.Solar2Lunar(solar)
    print(lunar)
    solar = Converter.Lunar2Solar(lunar)
    print(solar)
    print(solar.to_date(), type(solar.to_date()))

农历转国历:

.. code-block:: python

    lunar = Lunar(2018, 2, 30, isleap=False)
    print(lunar)
    solar = Converter.Lunar2Solar(lunar)
    print(solar)
    lunar = Converter.Solar2Lunar(solar)
    print(lunar)
    print(lunar.to_date(), type(lunar.to_date()))
    print(Lunar.from_date(datetime.date(2018, 4, 15)))

日期合法性检查, 农历和国历都起作用, 如: 农历闰月2018-2-15是不存在的:

.. code-block:: python

    try:
        lunar = Lunar(2018, 2, 15, isleap=True)
    except DateNotExist:
        print(traceback.format_exc())

打印内置节假日, 目前支持中文、英文输出:

.. code-block:: python

    from lunarcalendar.festival import festivals

    # print festivals, using English or Chinese
    print("----- print all festivals on 2018 in chinese: -----")
    for fest in festivals:
        print(fest.get_lang('zh'), fest(2018))

    print("----- print all festivals on 2017 in english: -----")
    for fest in festivals:
        print(fest.get_lang('en'), fest(2017))

输出:

.. code-block:: shell

    ......
    母亲节 2018-05-13
    父亲节 2018-06-17
    中秋节 2018-09-24
    感恩节 2018-11-22
    重阳节 2018-10-17
    春节 2018-02-16
    中元节 2018-08-25
    七夕节 2018-08-17
    腊八节 2019-01-13
    清明节 2018-04-05
    除夕 2019-02-04
    寒衣节 2018-11-08
    元宵节 2018-03-02
    龙抬头 2018-03-18
    端午节 2018-06-18
    ......


贡献
-----

目前，LunarCalendar支持的节假日只包含了在中国常见的节日，包括国历节假日(如: 国庆节、母亲节)和农历节假日(如: 中秋节、重阳节)。
内置了中文和英文两种语言，如果要支持韩文、日文的节假日，只需要在`festival.py`中添加对应的语言和节假日。

查看所有节假日的方法:

.. code-block:: shell

    from lunarcalendar.festival import festivals

    print("contain {} festivals".format(len(festivals)))
    print("----- print all festivals on 2018 in chinese: -----")
    for fest in festivals:
        print(fest.get_lang('zh'), fest(2018))


关于
----

* `Homepage <http://github.com/wolfhong/LunarCalendar>`_
* `PyPI <https://pypi.python.org/pypi/LunarCalendar>`_
* `Issue tracker <https://github.com/wolfhong/LunarCalendar/issues?status=new&status=open>`_