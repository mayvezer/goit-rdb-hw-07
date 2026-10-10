# Homework 7: Advanced PostgreSQL for Machine Learning

## 📋 Опис проєкту
Ця домашня робота присвячена використанню розширених можливостей PostgreSQL для задач машинного навчання (ML Data Engineering):
1. **Time-series агрегація та ML-ознаки** (lag, rolling averages, rolling volatility, expanding cumulative features) із застосуванням віконних функцій та обов'язковим `PARTITION BY`.
2. **Робота з напівструктурованими даними (JSONB)**: генерація подій різного типу, запити на основі containment (`@>`), перевірки ключів (`?`, `?|`) та JSONPath.
3. **Індексація та оптимізація (EXPLAIN ANALYZE, BUFFERS)**: порівняння продуктивності GIN-індексу (path_ops) проти Seq Scan, а також створення та тестування expression B-tree індексу для шлях-орієнтованого пошуку (`->>`).
4. **Порівняння архітектур**: JSONB-підхід проти реляційної (нормалізованої) таблиці для аналітичних запитів.

## 🛠 Джерело даних та середовище
- **База даних**: PostgreSQL (запускається всередині Google Colab через бібліотеку `pgserver`).
- **Датасет (Варіант А)**: NYC Taxi Trip Data (`yellow_tripdata_2024-03.parquet`). За відсутності мережевого підключення передбачено автономний **Stub-schema fallback**.
- **Основні таблиці**:
  - `t7_hw_taxi_daily` — щоденна агрегація поїздках таксі по зонах (`pickup_zone_id`, `ts_day`).
  - `v_t7_hw_taxi_features` — View з повним набором числових ML-ознак.
  - `t7_hw_events` — лог подій користувачів із плаваючим JSONB payload (5 типів подій).
  - `t7_hw_checkouts_norm` — нормалізована таблиця для аналізу транзакцій.

## 🚀 Інструкція з запуску
1. Відкрийте файл `hw7_taxi_events.ipynb` у **Google Colab**.
2. Виконайте послідовно всі клітинки за допомогою команди меню **Runtime -> Run All** (або Restart & Run All).
3. Усі залежності (`pgserver`, `psycopg2-binary`, `pandas`, тощо) встановлюються автоматично в першій комірці.
