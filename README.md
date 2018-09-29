# Русскоязычные NLP датасеты

В этом репозитории выложены толко датасеты, которые я создавал (обычно автоматически, иногда с ручной правкой)
для решения разных задач с текстами на русском языке.

## Ударения

[Упакованный tsv файл](https://github.com/Koziev/NLP_Datasets/blob/master/Stress/all_accents.zip).

Данные собраны для решения задачи конкурса [ClassicAI](https://classic.sberbank.ai/description).
Использованы открытые данные - Википедия и Викисловарь. В случаях, когда ударение
известно только для одной нормальной формы слова (леммы), я использовал таблицы словоизменения
в [грамматическом словаре](https://github.com/Koziev/GrammarEngine) и генерировал записи с отметкой ударности.
При этом подразумевается, что позиция ударения в слове не меняется при его склонении или спряжении. Для
некоторого количества слов в русском языке это не так, например:

*р^еки* (именительный падеж множественное число)  
*рек^и* (родительный падеж единственное число)  

В таких случаях в датасете будет один из вариантов ударения.

## Диалоги и обмены репликами

[Автоматически собранные русскоязычные диалоги](https://github.com/Koziev/NLP_Datasets/blob/master/Conversations/Data/ru.conversations.txt)


## Статистика употребляемости слов в группах по 2, 3 и 4 слова

Датасеты содержат числовые оценки того, насколько слова чаще употребляются вместе, чем порознь.
Подробности о содержимом и способе получения датасетов см. на [отдельной странице]().


## Короткие предложения

[Датасеты](https://github.com/Koziev/NLP_Datasets/tree/master/Samples) используются для тренировки чат-бота.
Они содержат короткие предложения, извлеченные из большого текстового корпуса.
Для удобства тренировки диалоговых моделей данные разбиты на 3 группы:

### Предложения с глаголом в 1-м лице единственного числа

```
Я только продаю!
Я не курю.
Я НЕ ОТПРАВЛЯЮ!
Я заклеил моментом.
Ездил только я.
```

### Предложения с глаголом в 2-м лице единственного числа

```
Как ты поступишь?
Ты это читаешь?
Где ты живешь?
Док ты есть.
Ты видишь меня.
```

### Предложения с подлежащим-существительным и глаголом в 3-м лице

```
Фонарь имел металлическую скобу.
Щенок ищет добрых хозяев.
Массажные головки имеют встроенный нагрев
Бусины переливаются очень красиво!
```

Предложения в датасетах facts4_1s.txt, facts5_1s.txt, facts5_2s.txt, facts4.txt,
facts6_1s.txt, facts6_2s.txt отсортированы с помощью кода [sort_facts_by_LSA_tSNE.py](https://github.com/Koziev/NLP_Datasets/blob/master/Samples/sort_facts_by_LSA_tSNE.py).
Идея сортировки следующая. Для предложений в файле сначала выполняем [LSA](http://scikit-learn.org/stable/modules/generated/sklearn.decomposition.TruncatedSVD.html),
получая векторы длиной 60 (см. константу LSA_DIMS в коде). Затем эти векторы встраиваются
в одномерное пространство с помощью [t-SNE](http://scikit-learn.org/stable/modules/generated/sklearn.manifold.TSNE.html),
так что в итоге для каждого предложения получается действительное число, такое, что
декартово-близкие в LSA-пространстве предложения имеют небольшую разность этих tsne-чисел. Далее
сортируем предложения согласно t-SNE значения и сохраняем получающийся список.

Предложения в остальных файлах отсортированы программой [sort_samples_by_kenlm.py](https://github.com/Koziev/NLP_Datasets/blob/master/Samples/sort_samples_by_kenlm.py)
в порядке убывания вероятности. Вероятность предложения получается с помощью предварительно
обученной 3-грамной языковой модели [KenLM](https://github.com/kpu/kenlm).

## Сэмплы со сменой грамматического лица

Пары предложений [в этих сэмплах](https://github.com/Koziev/NLP_Datasets/tree/master/ChangePerson) могут быть полезны для тренировки моделей в составе
чат-бота. Данные выглядят так:

```
Я часто захожу !	ты часто заходишь !
Я сам перезвоню .	ты сам перезвонишь .
Я Вам перезвоню !	ты Вам перезвонишь !
Я не пью .	ты не пьешь .
```

В каждой строке находятся два предложения, отделенные символом табуляции.



## Вопросы и ответы для чат-ботов

Датасеты сгенерированы автоматически из большого корпуса предложений.

[Триады "предпосылка-вопрос-ответ" для предложений длиной 3 слова](https://github.com/Koziev/NLP_Datasets/blob/master/QA/premise_question_answer4.txt)  
[Триады "предпосылка-вопрос-ответ" для предложений длиной 4 слова](https://github.com/Koziev/NLP_Datasets/blob/master/QA/premise_question_answer5.txt)  

Пример данных в вышеуказанных файлах:

```
T: Собственник заключает договор аренды
Q: собственник заключает что?
A: договор аренды

T: Спереди стоит защитное бронестекло
Q: где защитное бронестекло стоит?
A: спереди
```

Каждая группа предпосылка-вопрос-ответ отделена пустыми строками. Перед предпосылкой стоит
метка T:, перед вопросом метка Q:, перед ответом метка A:


## Прочее

[Перестановочные перефразировки](https://github.com/Koziev/NLP_Datasets/tree/master/ParaphraseDetection)

[Частоты слов с учетом частей речи](https://github.com/Koziev/NLP_Datasets/tree/master/WordformFrequencies)

[Леммы](https://github.com/Koziev/NLP_Datasets/blob/master/Lemmas/Data/word2lemma.7z)

[Приведение слов к нейтральной форме "штучка-штука"](https://github.com/Koziev/NLP_Datasets/blob/master/Lemmas/Data/lemma2normal.dat)



