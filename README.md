# Травицкий Сергей
# Домашнее задание к занятию «Репликация и масштабирование. Часть 2»

### Инструкция по выполнению домашнего задания

1. Сделайте fork [репозитория c шаблоном решения](https://github.com/netology-code/sys-pattern-homework) к себе в Github и переименуйте его по названию или номеру занятия, например, https://github.com/имя-вашего-репозитория/gitlab-hw или https://github.com/имя-вашего-репозитория/8-03-hw).
2. Выполните клонирование этого репозитория к себе на ПК с помощью команды `git clone`.
3. Выполните домашнее задание и заполните у себя локально этот файл README.md:
   - впишите вверху название занятия и ваши фамилию и имя;
   - в каждом задании добавьте решение в требуемом виде: текст/код/скриншоты/ссылка;
   - для корректного добавления скриншотов воспользуйтесь инструкцией [«Как вставить скриншот в шаблон с решением»](https://github.com/netology-code/sys-pattern-homework/blob/main/screen-instruction.md);
   - при оформлении используйте возможности языка разметки md. Коротко об этом можно посмотреть в [инструкции по MarkDown](https://github.com/netology-code/sys-pattern-homework/blob/main/md-instruction.md).
4. После завершения работы над домашним заданием сделайте коммит (`git commit -m "comment"`) и отправьте его на Github (`git push origin`).
5. Для проверки домашнего задания преподавателем в личном кабинете прикрепите и отправьте ссылку на решение в виде md-файла в вашем Github.
6. Любые вопросы задавайте в чате учебной группы и/или в разделе «Вопросы по заданию» в личном кабинете.

Желаем успехов в выполнении домашнего задания.

---

### Задание 1

Опишите основные преимущества использования масштабирования методами:

- активный master-сервер и пассивный репликационный slave-сервер; 
- master-сервер и несколько slave-серверов;


*Дайте ответ в свободной форме.*

<details>
<summary>ОТВЕТ</summary>

**активный master-сервер и пассивный репликационный slave-сервер**

1. Резервная копия хранящаяся на slave-сервер.
2. Отказоустойчивость: В случае выхода из строя master-сервера, возможночть настройки slave на на мастер, в случае необходимости внесения изменений в БД, минимизировав время простоя.
3. Снижает нагрузку на основной сервер при обработке запросов.

**master-сервер и несколько slave-серверов.**

1. Высокая отказоустойчивость: Возможность настроить любой slave-сервер на работу в качестве мастер.
2. Горизонтальная масштабируемость: Возможность создания неограниченного количества реплик.
3. Балансировка: Возможность распределения нагрузки при запросах между серверами. При грамотных настройках возможность прохождения пиковых нагрузок не заметно для пользователей.

</details>

---

### Задание 2


Разработайте план для выполнения горизонтального и вертикального шаринга базы данных. База данных состоит из трёх таблиц: 

- пользователи, 
- книги, 
- магазины (столбцы произвольно). 

Опишите принципы построения системы и их разграничение или разбивку между базами данных.

*Пришлите блоксхему, где и что будет располагаться. Опишите, в каких режимах будут работать сервера.* 

<details>
<summary>ОТВЕТ</summary>

**При горизонтальном, я бы распределил по серверам на базе ID пользователей, остаток от деления, ка это реализовано в дополнительном задрнии со звездочкой. В данном варианте, это было бы более равномерное распределение таблиц по серверам.**

**Вертикальный шардинг используется реже чем горизонтальный, так как он более сложен в реализации, и соответственно более сложные заппросы при извлечении данных. в данной ситуации я бы разделил по таблицам. Полбзователей со всеми данными на отдельный сервер, книги на другой. Магазины я бы отдельно не выносил на отдельный сервер. Магазины я бы оставил на сервере книги.  Но если список магазинов очень юольшой то теоритически можно вынести на от дельный сервер. В особых случаях таблицы конесно можно разнести по столбцам, но это очень сложно в реализации и дпльнейшкео администрировании**

|MAIN SERVER |          |         | 
|------------|----------|---------|
| 1          | Саша     | 118     |
| 2          | Юля      | 92      |
| 3          | Даниил   | 36      |


</details>
## Дополнительные задания (со звёздочкой*)
Эти задания дополнительные, то есть не обязательные к выполнению, и никак не повлияют на получение вами зачёта по этому домашнему заданию. Вы можете их выполнить, если хотите глубже шире разобраться в материале.

---
### Задание 3*

Выполните настройку выбранных методов шардинга из задания 2.

*Пришлите конфиг Docker и SQL скрипт с командами для базы данных*.

<details>
<summary>ОТВЕТ</summary>

**За основу взят пример из презентации, и лекции. Соответственно доработан. Структура таблици из презентации. Шаринг горизонтальный, по id, остаток от деления.**

*Скрины выполнения*
 
![img](https://github.com/travickiy67/Replication-and-Scaling-Part-2/blob/main/img/1.1.png)

---

![img](https://github.com/travickiy67/Replication-and-Scaling-Part-2/blob/main/img/1.2.png)

---

![img](https://github.com/travickiy67/Replication-and-Scaling-Part-2/blob/main/img/1.3.png)

---

![img](https://github.com/travickiy67/Replication-and-Scaling-Part-2/blob/main/img/1.4.png)

---

**Файлы**

[files](https://github.com/travickiy67/Replication-and-Scaling-Part-2/tree/main/files)

*Команды*

```
docker compose up -d
docker exec -it postgres_b1 psql -U postgres -d books -f /scripts/shards.sql -a /* создание таблиц */
docker exec -it postgres_b1 psql -U postgres -d books -c "select * from books" /* запрос */
docker exec -it postgres_d -U postgres /* Подключение к postgres */
\c books  /* Подключение к базе для запроса */
docker exec -it postgres_b1 psql -U postgres -d books -c "select * from books" /* запрос */

```
 
 
</details>
