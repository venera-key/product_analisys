# Проект - Продуктовый анализ данных в e-commerce  
**Цель**: Анализ продукта, метрик, выявить причины стагнации выручки   
**Стек**: Python (pandas, seaborn, matplotlib, numpy)  

**Задачи**:
- Оценить месячный retention в оформление заказа с помощью когортного анализа;
- Определить product/market fit у маркетплейса;
- Выбрать 5 основных метрик, для максимизации прибыли компании;
- Выбрать основную гипотезу;
- Сформулировать метрики, на которую гипотеза должна повлиять.

**Результат**:
- Медианный retention за первый месяц: 0.03%. Клиенты сильно от нас уходят, ценности для клиента в продукте нет.
- PMF у маркетплейса слабый, масштабировать пока нельзя. Но количество клиентов из месяца в месяц растет, проблем с привлечением нет. Проблема может быть в клиентском опыте
- Рассчитала метрики GMV, MAU, ARPPU. Значения метрик в состоянии стагнации. Нужно повышать.
- С помощью фреймворка ICE, выбрала гипотезу о вероятности роста доставленных заказов, при исправлении бага в системе процессинга заказов.
-  Для этой гипотезы выбрала метрики "Количество доставленных заказов", "Конверсия в доставку товара", "Конверсия в оформление заказа", которые должны повлиять на бизнес.


  
**Дано**   
Таблицы:

#### olist_customers_dataset.csv — таблица с уникальными идентификаторами пользователей
customer_id — позаказный идентификатор пользователя  
customer_unique_id — уникальный идентификатор пользователя (аналог номера паспорта)  
customer_zip_code_prefix — почтовый индекс пользователя  
customer_city — город доставки пользователя  
customer_state — штат доставки пользователя  

#### olist_orders_dataset.csv —  таблица заказов  
order_id — уникальный идентификатор заказа (номер чека)  
customer_id — позаказный идентификатор пользователя  
order_status — статус заказа  
order_purchase_timestamp — время создания заказа  
order_approved_at — время подтверждения оплаты заказа  
order_delivered_carrier_date — время передачи заказа в логистическую службу  
order_delivered_customer_date — время доставки заказа  
order_estimated_delivery_date — обещанная дата доставки  

#### olist_order_items_dataset.csv — товарные позиции, входящие в заказы  
order_id — уникальный идентификатор заказа (номер чека)  
order_item_id — идентификатор товара внутри одного заказа  
product_id — ид товара (аналог штрихкода)  
seller_id — ид производителя товара  
shipping_limit_date — максимальная дата доставки продавцом для передачи заказа партнеру по логистике  
price — цена за единицу товара  
freight_value — вес товара   

Пример структуры данных можно визуализировать по order_id == 00143d0f86d6fbd9f9b38ab440ac16f5  

Уникальные статусы заказов в таблице olist_orders_dataset:  
created — создан;  
approved — подтверждён;  
invoiced — выставлен счёт;  
processing — в процессе сборки заказа;  
shipped — отгружён со склада;  
delivered — доставлен пользователю;  
unavailable — заказ отменён по причине недоступности товара;;  
canceled — отменён.  
