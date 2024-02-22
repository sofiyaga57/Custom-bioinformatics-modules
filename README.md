# HW 14. OOP 

> *Дисклеймер 1*. Это ДЗ не очень сложное, но достаточно объемное. Помните, что оно на две недели, а не на одну. 

> *Дисклеймер 2*. Как всегда, в описании заданий очень много буков. Не пугайтесь, сами решения иногда гораздо компактнее. Если что делайте задания в том порядке, в котором вам комфортнее.

> *Дисклеймер 3*. Последнее задание связано с терминами Наследование и Абстракция, которые мы пройдем 17.02.24. Остальное можно делать уже сейчас.

## Часть I.

Эта часть выполняется в данном репозитории в скрипте `HW14_OOP.py` и примерами в `HW14_OOP.ipynb` через систему GitHub Classroom (просто клонируете репозиторий, пишете код и делаете пуш). 

### 1. Система бронирования оборудования 

Ваши коллеги по лаборатории пожаловались вам, что вечно кто-то надолго занимает тот или иной прибор и никого не предупреждает. Еще чуть-чуть, и дело дойдет до драк. Вы, как биоинформатик, решили спасти ситуацию и разработать систему для бронирования оборудования. 

Реализуйте классы `LabEquipment`, `Booking` и `User` со следующим функционалом.

**User**
 
- Имеет атрибут `name` (строка).
- Любые другие на ваше усмотрение (если нужны).


**Booking**
 
- Имеет атрибуты `equipment`, `user` (`User`), `start_time` и `end_time`
- Метод `is_intersect` принимает на вход другое бронирование и возвращает булевый результат проверки пересечения временных интервалов
- Любые другие на ваше усмотрение (если нужны).


**LabEquipment**

- Атрибут `equipment` хранит список имеющихся приборов.
- Атрибут `booking_history` хранит список всех бронирований (новые брони добавляются в конец списка).
- Метод `is_available` принимает на вход название прибора и временной интервал, а возвращает булевый результат проверки на отсутсвие конкурирующих бронирований.
- Метод `book` добавляет новое бронирование в историю бронирований, если для данного прибора в данное время нет имеющихся броней других пользователей. Если брони разных пользователей пересекаются, выводится кастомная ошибка (границы интервалов не включаются, т.е могут быть брони *до* 17:00 и *с* 17:00). Придумайте что делать если пересекаются бронирования одного пользователя.
- Если запрошенного прибора нет, то должна выводиться кастомная ошибка.
- Любые другие на ваше усмотрение (если нужны).


Сопроводите это небольшим примером в юпитер-ноутбуке (2-3 бронирования, какое-нибудь успешное и неуспешное).
Для работы со временем советую использовать модуль `datetime`. 


**Баллы**:

- Класс `User` - **1 балл**
- Класс `Booking` - **3 балла**
- Класс `LabEquipment` - **6 баллов**
- Кастомные ошибки - **1 балл** 
- Пример в юпитер-ноутбуке - **1 балл**

Как вы понимаете, в данном случае система довольно игрушечная. Тем не менее, если вдруг вам такая понадобится - довести ее до рабочей не так уж и сложно)). Нам главное чтобы это все хостилось где-то на сервере и непрерывно ожидало команд. А для передачи команд можно написать простейшего ТГ-бота, который будет считывать имя, время и прибор и отправлять в нашу систему. Совсем скоро мы научимся всему этому (в теме "Интернет"). 🙂


### 2. Интерпретатор  генетического кода

Что обычно подразумеваемся под работой с генетическим кодом? Его обычно как-то расшифровывают, транслируют и т.п. Но раз уж это "код", то что нам мешает его интерпретировать? В этом задании буквально в один класс и 2 метода мы напишем новый язык программирования! 

*Постановка задачи может звучать прям жутко, но просто пишите код, отвечаю, по сложности он будет в духе "комплементирование ДНК".*

Наш язык будет довольно элементарный. Он будет состоять из:
- Выделенной памяти (скажем, 5000 ячеек памяти), хранящей информацию в формате целых чисел
- Указателя, который находится в определенной ячейке памяти
- Инструкций для перемещения указателя (влево и вправо)
- Инструкций для изменения значения в ячейке памяти (инкремент и декремент)

Ну а интерпретатор этого языка мы напишем на python. 

Реализуйте класс `GenCodeInterpreter`. При инициализации нового интерпретатора должен создаваться массив из 5000 ячеек памяти (значение по-умолчанию - 0), указатель (по-умолчанию стоит в позиции 0), а также буфер хранящий результат работы программы (результат будет возвращаться в виде строки, поэтому исходно это пустая строка). 

В классе `GenCodeInterpreter` должен быть публичный метод `eval`, который принимает на вход строку с программой на нашем новом языке. При вызове `eval` происходит следующее:
- Буфер очищается
- Интерпретируется переданная программа
- Результат возвращается пользователю

Правила интерпретации следующие: 'A' - перемещение указателя вперед, 'T' - перемещение указателя назад, 'G' - инкремент значения в ячейке памяти, 'C' - декремент значения в ячейке памяти, 'N' - добавление значения в ячейке памяти в буфер на возврат пользователю. Касательно 'N' - мы храним в памяти целые числа, но как можно было бы с помощью этого кодировать какой-то более осмыленный текст? Давайте в нашем языке будем считать, что данные в памяти закодированы в ASCII-формате (нужно сопоставить букву имеющейся цифре на основе ASCII-таблице)

Также создайте две любые ошибки в нашем новом языке (и используйте их в соответствующих подходящих местах). В юпитер-ноутбуке импортируйте свой класс и продемонстрируйте его работу на примере генетического кода, который напечатает вашу фамилию (с заглавной буквы на русском языке).

Пример работы:
```python
interpreter = GenCodeInterpreter()
interpreter.eval('ATGCN')
>>> '\x00' # или пустота
```

```python
interpreter = GenCodeInterpreter()
code = 'G'*72 + 'N' + 'G'*33 + 'N' + 'C'*72 + 'N'
interpreter.eval(code)
>>> 'Hi!'
```

*Совет*: вам могут быть полезны функция `chr` и конструкция `match-case`.  

**Баллы**:

- Написанный и работающий интерпретатор - **6 баллов**
- Кастомные ошибки - **2 балла** (по одному за каждую)
- Пример в юпитер-ноутбуке с печатью фамилии - **1 балл**

**Фанфакт**: по сути то что мы тут сделали называется [эзотерическим языком программирования](https://ru.wikipedia.org/wiki/%D0%AD%D0%B7%D0%BE%D1%82%D0%B5%D1%80%D0%B8%D1%87%D0%B5%D1%81%D0%BA%D0%B8%D0%B9_%D1%8F%D0%B7%D1%8B%D0%BA_%D0%BF%D1%80%D0%BE%D0%B3%D1%80%D0%B0%D0%BC%D0%BC%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%B8%D1%8F). Это такие языки, которые в целом работают и все с ними хорошо, но скудность функционала и бесполезность зашкаливают. Наш язык еще, кажется, [полный по Тьюрингу](https://ru.wikipedia.org/wiki/%D0%9F%D0%BE%D0%BB%D0%BD%D0%BE%D1%82%D0%B0_%D0%BF%D0%BE_%D0%A2%D1%8C%D1%8E%D1%80%D0%B8%D0%BD%D0%B3%D1%83), а потому можно сказать что он попал в [Тьюринговскую трясину](https://ru.wikipedia.org/wiki/%D0%A2%D1%8C%D1%8E%D1%80%D0%B8%D0%BD%D0%B3%D0%BE%D0%B2%D1%81%D0%BA%D0%B0%D1%8F_%D1%82%D1%80%D1%8F%D1%81%D0%B8%D0%BD%D0%B0). В общем, как понимаете, это целая отдельная область программирования, где люди развлекаются как могут. Интересно, что зашифровано ли что-нибудь в человеческом геноме?


### 3. Meet the dunders

Давайте немного отдохнем и повеселимся. Вам дана функция `meet_the_dunders` с некоторым кодом. Эта функция возвращает число 42 (советую это проверить). Но как-то в этой функции маловато dunder'ов. От вас требуется заменить **внутри** функции максимально возможное количество синтаксических конструкций на вызовы dunder методов, dunder атрибутов и dunder переменных.

Замечания 
- Полностью всё заменить невозможно. Например, `function()` можно записать как `function.__call__()`, но скобочки есть скобочки, их ни на что не заменить. 
- Не доводите до абсурда. Например, можно написать `function.__call__.__call__....__call__()` и т.д. до бесконечности. В общем не закапывайтесь в повторы. 
- Чем больше разных методов вы найдете, тем больше будет балл.
- Структуру кода менять нельзя, просто изменяем конструкции на синонимичные.
- Код по итогу дожен работать и печатать число 4420.0, как в примере. 
- Подсказка: заменить точно не получится конструкции `for ... in ...`, `if-else`, `def ... return ... ` и оператор присваивания `=`.

**Баллы**:
- Максимум **5 баллов**

## Часть II.

В этой части мы будем дорабатывать ваш тул, который вы начинали писать в прошлом семестре (HW3 - HW6).

> Задание выполняется в вашем личном репозитории в виде пулл-реквеста. Перед решением ДЗ слейте все имеющиеся PR либо перейдите на самый последний коммит ветки HW6. 
> 0) Начните ветку HW14. 
> 1) Весь код из модулей нужно перенести в главный скрипт
> 2) Папку с модулями **нужно** удалить (`bio_files_processor.py` можно не трогать)
> 3) Все функции переписываем в классы в соотвествии с заданиями ниже
> 4) Делаете PR в main, **ссылку на PR прикладываете в:**
> > - **В Google Class**
> > - **В ноутбуке `HW14_OOP.ipynb`**

*Если вы учились ранее и восстановились, напишите мне*

### 4. FastQ-фильтратор с помощью Biopython

Писать свои классы конечно здорово (а еще полезно в учебных целях), но вообще обычно не советуют изобретать велосипеды. Мы писали целый модуль для работы с FastQ-файлами, хотя все это уже давно написано в библиотеке Biopython. Тогда мы его не трогали, потому что в биопитоне все написано через ООП. Сейчас самое время разобрать с тем как другие люди пишут и организуют свой ООП-код, ну и заодно дополнительно попрактиковаться с Biopython (ну и чтением документаций и исходников в целом).

В вашем скрипте напишите функцию `filter_fastq` (и любой остальной код) для фильтрации FastQ-файлов ровно так, как мы это делали в прошлом семестре (длина, качество, gc-состав), но с использованием классов и методов из библиотеки Biopython. Советую обратить внимание на такие вещи, как `SeqIO`, `SeqUtils`, `SeqRecord`. А еще на сайте биопитона прям есть Cookbook по которому раскиданы примеры работы с качеством, gc-составом и длиной. 

*Совет*: вы уже достаточно прошарены в питоне, иногда может быть проще почитать исходный код той или иной функции на [GitHub](https://github.com/biopython/biopython/tree/master/Bio) (используйте поиск), чем разбираться с документацией на сайте. 

**Баллы**:
- Максимум **5 баллов**

***Проверьте что код работает правильно***

### 5. Biological sequences world

*Соскучились по велосипедам?*

В прошлом семестре мы писали модуль для работы с различными биологическими последовательностями (ДНК, РНК, белки). Тогда это был просто набор функций и вам могло показаться, что все как-то плохо структурировано. Действительно, именно здесь идеально подходит ООП! Самое время заняться объединением данных и методов работы с ними. Особенно мы попрактикуем такие понятия, как *абстракция* и *полиморфизм*.

Напишите абстрактный класс `BiologicalSequence`, который задаёт следующий интерфейс:
+ Работа с функцией `len`
+ Возможность получать элементы по индексу и делать срезы последовательности (аналогично строкам)
+ Вывод на печать в удобном виде и возможность конвертации в строку
+ Возможность проверить алфавит последовательности на корректность

Напишите класс `NucleicAcidSequence`:
+ Данный класс реализует интерфейс `BiologicalSequence`
+ Данный класс имеет новый метод `complement`, возвращающий комплементарную последовательность
+ Данный класс имеет новый метод `gc_content`, возвращающий GC-состав (без разницы, в процентах или в долях)

Напишите классы наследники `NucleicAcidSequence`: `DNASequence` и `RNASequence`
+ `DNASequence` должен иметь метод `transcribe`, возвращающий транскрибированную РНК-последовательность
+ Данные классы не должны иметь <ins>публичных методов</ins> `complement` и метода для проверки алфавита, так как они уже должны быть реализованы в `NucleicAcidSequence`.

Напишите класс `AminoAcidSequence`:
+ Данный класс реализует интерфейс `BiologicalSequence`
+ Добавьте этому классу один любой метод, подходящий по смыслу к аминокислотной последовательности. Можете взять любой из осеннего семестра, желательно не самый большой и не самый маленький (не длина белка, но и не выравниванитель).



Комментарий по поводу метода `NucleicAcidSequence.complement`, так как я хочу, чтобы вы сделали его опредедённым образом:

При вызове `dna.complement()` или условного `dna.check_alphabet()` должны будут вызываться соответствующие методы из `NucleicAcidSequence`. При этом, данный метод должен обладать свойством полиморфизма, иначе говоря, внутри `complement` не надо делать условия а-ля `if seuqence_type == "DNA": return self.complement_dna()`, это крайне не гибко. Данный метод должен опираться на какой-то общий интерфейс между ДНК и РНК. Создание экземпляров `NucleicAcidSequence` не подразумевается, поэтому код `NucleicAcidSequence("ATGC").complement()` не обязан работать, а в идеале должен кидать исключение `NotImplementedError` при вызове от экземпляра `NucleicAcidSequence`. В целом следите чтобы при обработке данных определенного типа (ДНК, белок, ... ) возвращался объект правильного типа (а не просто `str`).

Вся сложность задания в том, чтобы правильно организовать код. Если у вас есть повторяющийся код в сестринских классах или родительском и дочернем, значит вы что-то делаете не так.


Маленькое замечание: По-хорошему, между классом `BiologicalSequence` и классами `NucleicAcidSequence` и `AminoAcidSequence`, ещё должен быть класс-прослойка, частично реализующий интерфейс `BiologicalSequence`, но его писать не обязательно, так как задание и так довольно большое (правда из-за этого у вас неминуемо возникнет повторяющийся код в классах `NucleicAcidSequence` и `AminoAcidSequence`)


**Баллы**:
- За каждый из 5-и классов `BiologicalSequence`, `NucleicAcidSequence`, `DNASequence`, `RNASequence`, `AminoAcidSequence` - по 3 балла (в сумме **15 баллов**).

- За общую логику, структуру и дизайн - до **4 баллов**.


### Общая разбалловка и требования

- Итого - 50 баллов.
- За проблемы с качеством кода можно **потерять до 10 баллов**. Обратите внимание на отступы, пробелы, наименования, аннотации типов - кода очень много, и все это имеет большое значение. Докстринги не обязательны, но могут поднять настроение проверяющим.
- Если импортируются сторонние библиотеки, они должны быть прописаны в `requirements.txt`!
- README не нужен.
- Проверьте свой код линтерами перед отправкой ДЗ. Если что, я приложил скриптик `pre-commit`, вот [тут](https://plausible-cannon-091.notion.site/Code-auto-checks-02b2ea69c1d545fca07b50ce5933ed5f?pvs=74) описано как им пользоваться. 



### **Предполагаемый учебный результат**

Это задание позволит лучше разобраться с ООП на практике. 

1) Система бронирования позволит потреннироваться с более сложными программами, состоящими из нескольких взаимосвязанных классов.
2) Интерпретатор генетического кода покажет, что даже очень простой код может быть большим программистским достижением!
3) Meet the dunders позволит познакомиться с разннобразием дандеров.
4) FastQ-фильтратор позволит почувствовать, как знание ООП упрощает понимание сторонних библиотек и работу с ними, а также даст возможность посмотреть на хорошие и плохие вещи в чужом коде. 
5) Biological sequences world позволит на практике пощупать такие эвфемерные вещи, как 3 кита ООП. 

Удачи! ✨✨