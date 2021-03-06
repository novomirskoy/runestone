..  Copyright (C)  Brad Miller, David Ranum, Jeffrey Elkner, Peter Wentworth, Allen B. Downey, Chris
    Meyers, and Dario Mitchell.  Permission is granted to copy, distribute
    and/or modify this document under the terms of the GNU Free Documentation
    License, Version 1.3 or any later version published by the Free Software
    Foundation; with Invariant Sections being Forward, Prefaces, and
    Contributor List, no Front-Cover Texts, and no Back-Cover Texts.  A copy of
    the license is included in the section entitled "GNU Free Documentation
    License".

Управляющие структуры
~~~~~~~~~~~~~~~~~~~~~

Как мы уже отмечали ранее, алгоритмам требуются две важные управляющие
структуры: для итераций и для выбора. Обе они поддерживаются в Python
в различных формах. Программисты могут выбирать тот способ, который
будет более уместным в данных обстоятельствах.

Для итераций Python предлагает стандартный оператор ``while`` и очень
мощный оператор ``for``. Первый из них повторяет тело кода столько раз,
сколько остаётся истинным его условие. Например:


::

    >>> counter = 1
    >>> while counter <= 5:
    ...     print("Hello, world")
    ...     counter = counter + 1


    Hello, world
    Hello, world
    Hello, world
    Hello, world
    Hello, world

напечатает фразу “Hello, world” пять раз. Условие оператора ``while``
вычисляется каждый раз в начале итерации. Если оно истинно, то будет
выполнено тело оператора. Структуру ``while`` в Python легко
увидеть через обязательные шаблоны отступов, которые навязывает этот язык.

Оператор ``while`` представляет собой итерационную структуру очень
общего назначения, которая может использоваться во многих различных
алгоритмах. Очень часто итерации контролирует составное условие. Код


::

    while counter <= 10 and not done:
    ...

приведёт к тому, что тело оператора будет вычисляться только в случае,
когда будут выполнены обе части условия. Значение переменной ``counter``
должно быть меньше или равно 10, а значение переменной ``done`` - быть равным
``False`` (``not False`` - это ``True``), чтобы результат ``True and True``
тоже был истиной.


Несмотря на то, что этот тип конструкции широко применяется во многих
ситуациях, другая итеративная структура - оператор ``for`` - может быть
использована в связке со многими коллекциями Python. ``for`` можно
пользоваться для итерации по членам коллекции, если она является
последовательной. Например,


::

    >>> for item in [1,3,6,2,5]:
    ...    print(item)
    ...
    1
    3
    6
    2
    5

присваивает переменной ``item`` каждое последующее значение из списка
[1,3,6,2,5], после чего выполняется тело цикла. Этот способ работает
для любой последовательной коллекции (списков, кортежей и строк).

Общее применение оператора ``for`` заключается в том, чтобы реализовывать
определённую итерацию на диапазоне значений. Оператор


::

    >>> for item in range(5):
    ...    print(item**2)
    ...
    0
    1
    4
    9
    16
    >>>

выполнит функцию ``print`` пять раз. Функция ``range`` вернёт диапазон,
представляющий собой последовательность 0, 1, 2, 3, 4, и каждое из этих
значений будет присвоено переменной ``item``. Затем они будут возведены
в квадрат и напечатаны.

Другой очень полезной версией использования этой итерационной структуры
является обработка каждого символа строки. Следующий фрагмент кода проходит
по списку строк, обрабатывая каждый символ в них присоединением его к списку.
Результатом будет список символов из всех слов.


.. activecode:: intro_8
    :caption: Переработка каждого символа в список строк

    wordlist = ['cat','dog','rabbit']
    letterlist = [ ]
    for aword in wordlist:
        for aletter in aword:
            letterlist.append(aletter)
    print(letterlist)

Операторы выбора позволяют программистам задавать вопросы и выполнять
различные действия, основываясь на ответе. Большинство языков
программирования предоставляют две версии полезных конструкций: ``ifelse``
и ``if``. Простой пример бинарного использования оператора ``ifelse``:


::

    if n<0:
       print("Sorry, value is negative")
    else:
       print(math.sqrt(n))

В этом примере объект, ссылающийся на ``n``, проверяется на условие
"меньше нуля". Если это так, то печатается сообщение, что ``n`` -
отрицательное число. В противном случае выполняется ветка else,
в которой вычисляется квадратный корень.

Операторы выбора, как и любые управляющие конструкции, могут быть
вложенными, чтобы результат одного ответа помогал определить, как
ответить на следующий. Например, предположим, что ``score`` - это
переменная, содержащая ссылку на результат теста по информатике.


::

    if score >= 90:
       print('A')
    else:
       if score >=80:
          print('B')
       else:
          if score >= 70:
             print('C')
          else:
             if score >= 60:
                print('D')
             else:
                print('F')

Этот фрагмент будет классифицировать значение переменной ``score``
с помощью вывода на печать буквы заработанной оценки. Если счёт выше
или равен 90, то оператор напечатает ``А``. Если это не так (``else``),
то проверяется следующее условие. Если счёт выше или равен 80, то он
должен лежать между 80 и 89, поскольку ответ на предыдущий вопрос был
ложью. В этом случае печатается ``В``. Вы можете видеть, как шаблоны
отступов в Python помогают ассоциировать ``if`` и ``else`` без
использования дополнительных синтаксических элементов.

Альтернативным синтаксисом для вложенного таким образом выбора является
использование ключевого слова ``elif``. ``else`` и последующий ``if``
комбинируются, исключая дополнительные уровни. Заметьте, 
конечное ``else`` по-прежнему необходимо, чтобы предоставить случай
по умолчанию, если все остальные условия не выполнятся.


::

    if score >= 90:
       print('A')
    elif score >=80:
       print('B')
    elif score >= 70:
       print('C')
    elif score >= 60:
       print('D')
    else:
       print('F')

Python также имеет вариант единичной конструкции выбора - оператор ``if``.
Для него при истинности условия происходит выполнение действия. В
противном случае процесс обработки просто переходит на следующий после
``if`` оператор. Например, в коде ниже сначала проверяется на отрицательность значение ``n``. 
Если условие выполнено, то ``n`` заменяют абсолютным
значением. Но в любом случае следующее действие - это извлечение квадратного корня.


::

    if n<0:
       n = abs(n)
    print(math.sqrt(n))


.. admonition:: Самопроверка

    Проверьте своё понимание изложенного материала, попробовав решить следующее упражнение.
    Измените код из Activecode 8 таким образом, чтобы итоговый список содержал единственную копию каждой буквы.

    .. activecode:: self_check_1

       # ответ: ['c', 'a', 't', 'd', 'o', 'g', 'r', 'b', 'i']




.. video:: list_unique
   :controls:
   :thumb: ../_static/videothumb.png

   http://media.interactivepython.org/pythondsVideos/list_unique.mov
   http://media.interactivepython.org/pythondsVideos/list_unique.webm

Возвращаясь к спискам, приведём альтернативный метод их создания с
использованием итерационных конструкций и конструкций выбора. Он известен,
как **генератор списков**, и позволяет легко создавать списки, основываясь
на неких критериях обработки и выбора. Например, если мы захотим получить
список из первых десяти идеальных квадратов, то можем воспользоваться оператором
``for``:


::

    >>> sqlist=[]
    >>> for x in range(1,11):
             sqlist.append(x*x)

    >>> sqlist
    [1, 4, 9, 16, 25, 36, 49, 64, 81, 100]
    >>>

А с использованием генератора списков это делается одной строкой:

::

    >>> sqlist=[x*x for x in range(1,11)]
    >>> sqlist
    [1, 4, 9, 16, 25, 36, 49, 64, 81, 100]
    >>>

Переменная ``x`` принимает значения от 1 до 10, как это определено для
конструкции ``for``. Затем вычисляется величина ``x*x`` и присоединяется
к создаваемому списку. Общий синтаксис генераторов списков также разрешает
использовать критерий выбора, чтобы добавлялись только подходящие элементы.
Например,


::

    >>> sqlist=[x*x for x in range(1,11) if x%2 != 0]
    >>> sqlist
    [1, 9, 25, 49, 81]
    >>>

Этот генератор создаёт список, содержащий квадраты только нечётных
чисел в диапазоне от 1 до 10. Совместно с генераторами списков можно
использовать любые последовательности, поддерживающие итерации.
Результатом будет новый список.


::

    >>>[ch.upper() for ch in 'comprehension' if ch not in 'aeiou']
    ['C', 'M', 'P', 'R', 'H', 'N', 'S', 'N']
    >>>

.. admonition:: Самопроверка

    Проверьте своё понимание генераторов списков, переделав Activecode 8
    с их использованием. Дополнительное задание: придумайте,
    как можно удалить дубликаты.

    .. activecode:: self_check_2

       # ответ: ['c', 'a', 't', 'd', 'o', 'g', 'r', 'a', 'b', 'b', 'i', 't']


.. video:: listcomp
   :controls:
   :thumb: ../_static/videothumb.png

   http://media.interactivepython.org/pythondsVideos/listcomp.mov
   http://media.interactivepython.org/pythondsVideos/listcomp.webm

.. disqus::
