# FuturesAnalyzer


## Общее Описание
**FuturesAnalyzer** – это комплексный аналитический инструмент, предназначенный для трейдеров и аналитиков рынка криптовалютных фьючерсов. 
Автоматизирует процесс выявления эффективности точек для входа в позицию.

## Ключевые Функции
- **Анализ данных Binance Futures**: Интеграция с API Binance для получения реальных торговых данных.
- **Анализ эффективности точек входа**: Анализ рыночных данных для определения наиболее перспективных точек входа в сделки.
- **Расчет технических тндикаторов**: Вычисление ключевых технических индикаторов, таких как RSI.
- **Визуализация Данных**: Графики  для наглядного отображения рыночных тенденций.
  
## Структура проекта

- `utils/`: Модули с утилитами и вспомогательными функциями.
  - `time_utils.py`: Функции для работы со временем.
  - `finance_utils.py`: Финансовые расчеты, такие как RSI.
  - `data_utils.py`: Общие функции для работы с данными.
- `api/`: Модули для взаимодействия с внешними API.
  - `binance_api.py`: Функции для работы с Binance API.
  - `other_api.py`: Модули для работы с другими API.
- `visualization/`: Модуль для визуализации данных.
  - `plot_utils.py`: Функции для создания графиков и диаграмм.
- `main.py`: Основной скрипт, координирующий работу модулей.
- `notebooks/`: Jupyter notebooks для анализа и тестирования.
  - `data_analysis.ipynb`: Ноутбук для анализа данных.


## Начало работы

1. **Клонирование репозитория**

```bash
git clone https://github.com/RomanV2/FuturesAnalyzer.git

cd FuturesAnalyzer
pip install -r requirements.txt
```

## Использование

### main.py
Файл `main.py` является точкой входа в приложение. 

```bash
    symbol = 'ARUSDT'
    alert_price = 'alert price: 8.006'
    start_time = '2023-11-09 18:23:54.181000'

    clear_price = extract_price(alert_price)
    clear_time = convert_time_to_utc_millis(start_time)

    # Десериализация строки JSON обратно в словарь
    result = asyncio.run(get_signal_performance_data(symbol, clear_price, clear_time, interval='1m',
                         n_intervals=7, deviation_threshold=3, check_rise=False))
    # Десериализация строки JSON обратно в словарь
    result_dict = json.loads(result)
    print(result_dict)

    price_data = result_dict["data"]
    visualize_entry_point(symbol, price_data, clear_price)
```

![Candlestick Chart Visualization](https://github.com/RomanV2/FuturesAnalyzer/blob/master/visualization/visualization.JPG)

## Использование `data_analysis.ipynb`

### Описание
`data_analysis.ipynb` – Jupyter Notebook для детального анализа торговых сигналов криптовалют. Он включает в себя несколько ключевых шагов, начиная от инициализации и до анализа данных.

### Структура Notebook
1. **Инициализация**: Импорт необходимых библиотек и методов из `main.py`.
2. **Загрузка данных**: Чтение данных из CSV-файла с сигналами (`alert_from_algo.csv`).
3. **Предобработка данных**: Преобразование типов данных.
4. **Отображение данных**: Показ обработанного DataFrame.
5. **Типы данных**: Показ типов данных каждого столбца DataFrame.
6. **Асинхронный анализ данных**: Обработка сигналов с использованием асинхронных функций и их объединение с исходным DataFrame.
7. **Показ результатов**: Отображение итогового DataFrame с состоянием сигналов и изменением цены.
8. **Подсчет статусов**: Группировка по столбцу 'status' для подсчета их количества.
9. **Подсчет успешных сигналов**: Отображение количества успешных сигналов.
10. **Расчет и добавление RSI**: Асинхронный расчет индекса относительной силы (RSI) и добавление его к DataFrame.

### Использование
- Запустите каждую ячейку последовательно, начиная с ячейки инициализации.
- Убедитесь, что путь к CSV-файлу корректен и файл доступен.
- Итоговый DataFrame может быть использован для соритровки по столбцам, дальнейшего анализа или визуализации.

### Примечание
- Notebook содержит как синхронный, так и асинхронный код Python.
- Для выполнения специфических операций используются пользовательские функции из `main.py`.
- Этот ноутбук специально разработан для анализа данных сигналов криптовалют.

