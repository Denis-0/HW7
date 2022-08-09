Настройте выполнение контрольной точки раз в 30 секунд.
--можно настроить в postgresql.conf
--![image](https://user-images.githubusercontent.com/45406197/183584170-3438fe82-e8b6-4751-8776-1ffb37fd6801.png)
-- проверим размер кеша
SELECT setting, unit FROM pg_settings WHERE name = 'shared_buffers';
--![image](https://user-images.githubusercontent.com/45406197/183586350-3e08b296-1bc1-4559-b35a-8f0eb3357f7d.png)
     --рестартуем кластер
--![image](https://user-images.githubusercontent.com/45406197/183586762-ab19af8d-4028-498f-a678-b15ea4f0a15c.png)
уменьшим количество буферов для наблюдения
--![image](https://user-images.githubusercontent.com/45406197/183586957-40938a56-1c19-4f25-8e97-93a024acaf2e.png)

создаем таблицу 
--![image](https://user-images.githubusercontent.com/45406197/183666290-a3c098f2-61fc-40ff-8b3b-f9dea5a11ae8.png)

видим стринцу с кешем
--![image](https://user-images.githubusercontent.com/45406197/183667882-57ff9619-e9a0-451f-8b10-dec7404fe491.png)

прогрев кеша
--![image](https://user-images.githubusercontent.com/45406197/183670212-53b06b73-fec6-4898-8c0b-037bf3647b97.png)

посмотрим на wal file
--![image](https://user-images.githubusercontent.com/45406197/183670968-d45276fd-f2d9-49d1-b2b4-293bd73e27d2.png)

10 минут c помощью утилиты pgbench подавайте нагрузку.
--pgbench -P 1 -T 600 buffer_temp

Измерьте, какой объем журнальных файлов был сгенерирован за это время. 
--![image](https://user-images.githubusercontent.com/45406197/183676399-128a8769-3bb7-4f72-bd42-cc17890631c6.png)

Оцените, какой объем приходится в среднем на одну контрольную точку.
Проверьте данные статистики: все ли контрольные точки выполнялись точно по расписанию. Почему так произошло?
Сравните tps в синхронном/асинхронном режиме утилитой pgbench. Объясните полученный результат.
Создайте новый кластер с включенной контрольной суммой страниц. Создайте таблицу. Вставьте несколько значений. Выключите кластер. 
Измените пару байт в таблице. Включите кластер и сделайте выборку из таблицы. Что и почему произошло? как проигнорировать ошибку и продолжить работу?
