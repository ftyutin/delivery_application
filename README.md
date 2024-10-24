### Анализ проведенного A/B-теста приложения доставки
Команда внедрила в приложение умную систему рекомендации товаров – предполагается, что такая система поможет пользователям эффективнее работать с приложением и лучше находить необходимые товары.

Чтобы проверить эффективность системы рекомендаций, был проведен АБ-тест. В группе 1 (экспериментальная группа) оказались пользователи с новой системой рекомендаций, в группе 0 (контрольная группа) пользователи со старой версией приложения, где нет рекомендации товаров.

<u><b>Задача:</u></b><br>
Оценить, смогла ли новая система рекомендаций принести пользу бизнесу и пользователям приложения. Для этого нужно выбрать метрики, которые отвечают за качество сервиса, и статистически сравнить эти метрики в двух группах.

Результат работы – аналитическое заключение с ответом на вопрос, стоит ли включать новую систему рекомендаций на всех пользователей.

Данные с логами заказов пользователей лежат в папке <b>./data</b> и имеют следующую структуру:

* <i>./data/ab_users_data.csv</i> – история заказов пользователей, в этой таблице есть информация о том, какие заказы создавали и отменяли пользователи.

| **user_id** | **order_id** | **action**   | **time**                   | **date**   | **group** |
|:-----------:|:------------:|:------------:|:--------------------------:|:----------:|:---------:|
| 964         | 1255         | create_order | 2022-08-26 00:00:19.000000 | 2022-08-26 | 0         |
| 965         | 1256         | create_order | 2022-08-26 00:02:21.000000 | 2022-08-26 | 1         |
| 964         | 1257         | create_order | 2022-08-26 00:02:27.000000 | 2022-08-26 | 0         |
| 966         | 1258         | create_order | 2022-08-26 00:02:56.000000 | 2022-08-26 | 0         |

<br>

* <i>./data/ab_orders.csv</i> – подробная информация о составе заказа, тут для каждого заказа есть список id тех продуктов, которые были включены в заказ.

| **order_id** | **creation_time**          | **product_ids**    |
|:------------:|:--------------------------:|:------------------:|
| 1255         | 2022-08-26 00:00:19.000000 | "{75, 22, 53, 84}" |
| 1256         | 2022-08-26 00:02:21.000000 | "{56, 76, 39}"     |
| 1257         | 2022-08-26 00:02:27.000000 | "{76, 34, 41, 38}" |
| 1258         | 2022-08-26 00:02:56.000000 | "{74, 6}"          |

<br>

* <i>./data/ab_products.csv</i> – подробная информация о продуктах, их наименование и стоимость.

| **product_id** | **name**                | **price** |
|:--------------:|:-----------------------:|:---------:|
| 1              | сахар                   | 150.0     |
| 2              | чай зеленый в пакетиках | 50.0      |
| 3              | вода негазированная     | 80.4      |
| 4              | леденцы                 | 45.5      |


Не стоит использовать интерактивные графики в итоговом файле – они имеют смысл только в динамических отчётах вроде веб-страницы.