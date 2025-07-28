# dbops-project
Исходный репозиторий для выполнения проекта дисциплины "DBOps"

Как создан пользователь и какие права ему выданы:

CREATE USER autotest WITH PASSWORD 'password';

GRANT CONNECT ON DATABASE store TO autotest;

GRANT ALL PRIVILEGES ON ALL TABLES IN SCHEMA public TO autotest;

ALTER DEFAULT PRIVILEGES IN SCHEMA public GRANT ALL PRIVILEGES ON TABLES TO autotest;

GRANT ALL PRIVILEGES ON ALL SEQUENCES IN SCHEMA public TO autotest;

ALTER DEFAULT PRIVILEGES IN SCHEMA public GRANT ALL PRIVILEGES ON SEQUENCES TO autotest;

GRANT USAGE ON SCHEMA public TO autotest;

GRANT CREATE ON SCHEMA public TO autotest;




sudo docker exec -it 93a6a597a482 psql -U user -d store -c "GRANT USAGE ON SCHEMA public TO autotest;"

sudo docker exec -it 93a6a597a482 psql -U user -d store -c "GRANT CREATE ON SCHEMA public TO autotest;"



Запрос, который покажет, какое количество сосисок было продано за каждый день предыдущей недели.


SELECT orders.date_created,
       SUM(order_product.quantity) AS sausages_quantity
FROM orders JOIN order_product ON orders.id = order_product.order_id
WHERE orders.status in ('shipped') AND orders.date_created > NOW() - INTERVAL '7 DAY'
GROUP BY orders.date_created;
