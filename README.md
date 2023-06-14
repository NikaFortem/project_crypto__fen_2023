## project_crypto__fen_2023
Репозиторий для проекта по анализу данных на ФЭН 2023. 

## Структура файлов:
- файлы с кодом: <a href="https://github.com/NikaFortem/project_crypto__fen_2023/blob/main/parcing_binance.ipynb" target="_blank">parcing_binance.ipynb</a>, data_analysis.ipynb
- файлы с данными: <a href="https://github.com/NikaFortem/project_crypto__fen_2023/blob/main/df_price.csv" target="_blank">df_price.csv</a>, <a href="https://github.com/NikaFortem/project_crypto__fen_2023/blob/main/type.txt" target="_blank">type.txt</a>, <a href="https://github.com/NikaFortem/project_crypto__fen_2023/blob/main/USTREASURY-YIELD.csv" target="_blank">USTREASURY-YIELD.csv</a>. 

# Тема проекта: **"Классификация криптовалют на основе их рыночных показателей"**

## Состав группы: Виктория Карпейкина, Юлия Щучкина, Максим Бочаров

# Данные : 

В рамках нашего проекта мы проанализировали котировки топ-68 криптовалют за период с 01.01.2020 по 10.05.2023, полученные помощи  <a href="https://github.com/NikaFortem/project_crypto__fen_2023/blob/main/parcing_binance.ipynb" target="_blank">парсинга</a> с криптовалютной
биржи Binance. Они представлены в таблице <a href="https://github.com/NikaFortem/project_crypto__fen_2023/blob/main/df_price.csv" target="_blank">df_price.csv</a> .

Однако помимо стоимостных показателей, мы посмотрели на тип рассматриваемых криптовалют (категориальный признак). По самой базовой классификации криптовалюты делятся на **монеты (coin)** и **токены (token)**.

**Монеты** – это независимые криптоактивы, которые способны работать автономно от других платформ, так как они обладают собственным блокчейном, используются для совершения сделок купли продажи различных товаров, для инвестирования.

**Токены** - не обладают собственным блокчейном, им необходим посредник для совершения сделок, зачастую используются как расчетное средство внутри криптовалютных стартапов, и в проектах связанных с NFT (play-to-earn), где частой практикой является привязка токенов к каким-то более крупным монетам, таким как Ethereum. 

Мы взяли данные о типе криптовалют с сайта https://coinmarketcap.com . Они представлены в текстовом файле <a href="https://github.com/NikaFortem/project_crypto__fen_2023/blob/main/type.txt" target="_blank">type.txt</a> .

# Первичный анализ данных:

На основе первичного анализа данных были сделаны выводы о динамике криптовалют за рассматриваемый период. В течение последних 3 лет динамика рынка криптовалют была довольно неодназначной. Однако можно сказать, что с начала 2020 года к маю 2023 года цены криптовалют выросли.

<h1 align="center"><img src="https://github.com/NikaFortem/project_crypto__fen_2023/blob/main/pictures/plot_1.png" height="260"/>   <img src="https://github.com/NikaFortem/project_crypto__fen_2023/blob/main/pictures/plot_2.png" height="260"/></h1>

Сперва можно наблюдать довольно успешное восстановление крипторынка после пандемии covid-19 в 2020 году. Затем можно наблюдать значительный спад в конце весны 2021 года, связанный с тем, что: биткоин обвалился более чем на 30% до 30 тысяч, т.к. Илон Маск отказался принимать платежи в виде биткоина в Tesla - отчасти из-за запретов на цифровые активы в Китае и того, что их майнинг вредит окружающей среде, а эфир стал стоить менее $2000, упав на 44%, из-за этого, прикрываясь разными причинами, криптобиржи временно приостанавливали покупку и вывод средств. Далее значимый кризис наблюдался в начале 2022 года, по причине напряженной политической обстановки в Казахстане и началом СВО. Следующий кризис, наблюдаемиый весной 2022, стали называть системным из-за падения доверия инвесторов к крипторынку на фоне скандала вокруг биржи FTX — четвертой среди крупнейших бирж по торговле криптовалютами, связанного с недостаточным риск-менеджментом, что в период борьбы с инфляцией в Америке и повышением ключевой ставки сильно сказалось на котировках криптовалют.

Все эти кризисы отразились на графиках динамики цен рассмотренных криптовалют как резкие скачки в сторону понижения их цен.  

# Рыночные показатели криптовалют:

Для дальнейшего анализа и машинного обучения мы использовали следующие рыночные показатели:

### **Доходность**  

Процентное изменение стоимости за некоторый промежуток времени. Мы будем работать с доходностями за день: 

$$
R_t = \frac{P_t - P_{t-1}}{P_{t-1}}
$$

### **Волатильность** 

Cтандартное отклонение доходности актива. 

### **Value-at-Risk на уровне 5%**

Квантиль доходности уровня 5%, т.е. такое значение доходности, что в 95% случаев дела будут идти лучше.

### **Коэффициент Шарпа**

$$
Sharp Ratio = \frac{R_p - R_f}{σ_p}
$$

- $R_p$ - доходность анализируемого актива

- $R_f$ - доходность безрискового актива

- $σ_p$ - стандартное отклонение доходности анализируемого актива

   Вычисляя коэффициент Шарпа, мы сравниваем поведение актива с альтернативной безрисковой величиной. Поскольку все криптовалюты торгуются в долларах США,    оптимально было взять за подобную безрисковую величину доходность по государственным облигациям США - US TREASURY.

   Доходность US TREASURY за период 01.01.2020 - 10.05.2023 взята с сайта американской биржи NASDAQ 
   (https://data.nasdaq.com/data/USTREASURY/YIELD-treasury-yield-curve-rates). Они представлены в таблице <a href="https://github.com/NikaFortem/project_crypto__fen_2023/blob/main/USTREASURY-YIELD.csv" target="_blank">USTREASURY-YIELD.csv</a> .

   Однако в отличии от криптовалютной биржи Binance, с которой взяты данные о котировках криптовалют, биржа NASDAQ, где торгуются ценные бумаги, собирает      статистику только в будние дни, так как по входным торги не идут. Поэтому далее в отношении доходностей и прочих показателей были рассмотрены только        рабочие дни.

   Поскольку ранее мы рассматривали ежедневную доходность криптовалют, для подсчета коэффициента Шарпа были рассмотрены ежедневные колебания доходности,      связанные с колебаниями стоимости treasury (купонную доходность здесь не учитывали), самых краткосрочных US TREASURY, то есть со сроком обращения 1        месяц.
  
### Прочие показатели

   Также для боллее наглядного представления динамики рынка криптовалют были рассмотрены такие показатели, как:
   - логарифмированные цены
   - накопленная доходность
   - Average True Range (средний истинный диапозон)

# Проверка гипотез:

Для того, чтобы проанализировать влияние типа криптовалюты на ее рыночное поведение, мы проверили серию гипотез о равенстве математических ожиданий и дисперсий между типами криптовалют по рассчитанным для них показателям: доходности, волатильности и VaR. Для их проверки мы использовали 2 основные выборки: криптовалюты типа "coin" и типа "token". В ходе работы мы проверили следующие гипотезы:

   - Гипотеза о равенстве матожиданий по доходности для двух групп криптовалют

   - Гипотеза о равенстве матожиданий по волатильности для двух групп криптовалют

   - Гипотеза о равенстве матожиданий по VaR для двух групп криптовалют

   - Гипотеза о равенстве дисперсий по доходности для двух групп криптовалют

   - Гипотеза о равенстве дисперсий по волатильности для двух групп криптовалют

   - Гипотеза о равенстве дисперсий по VaR для двух групп криптовалют

Все рассмотренные гипотезы на 5% уровне значимости не отвергаются. Это говорит о том, что тип криптовалют не оказывает значительного влияния на их рыночное поведение, поскольку математические ожидания и дисперсии их рыночных показателей не отличаются (в 95% случаев).

# Машинное обучение - Кластеризация

В рамках нашего проекта и блока "Машинное обучение" рассматриваем задачу кластеризации. Мы разбиваем криптовалюты на несколько сегментов, анализируя их рыночные показатели. Обучающей выборки в данной задаче нет. В результате машинного обучения мы получим новый критерий разделения криптовалют на группы - рыночные показатели и проанализируем получившиеся кластеры.

В качестве рыночных показателей мы используем:

- доходность

- волатильность

- Value at Risk

- коэффициент Шарпа

Наиболее распространенные методы кластеризации - K-means и DBSCAN, их мы и будем использовать.

## Кластеризация методом K-means

Кластеризация методом K-means происходит по следующему сценарию:

- Инициализируем центры кластеров случайно (задано количество кластеров).
- Относим точки к соответствующим кластерам (с минимальным расстоянием до их центра).
- Производится пересчет центров кластеров по формуле центра масс всех точек принадлежащих кластеру.
- Пункты 2-3 повторяются до тех пор пока центры кластеров перестанут меняться (сильно).

Для поиска оптимального количества кластеров в модели K-means используется метод локтя: мы обучили модель для разного количества кластеров и для каждого из них подсчитали такой критерий – сумма квадратов расстояний от точек до центроидов кластеров, к которым они относятся - по следующей формуле:

$$ 
J(C) = \sum_{k=1}^K\sum_{i~\in~C_k} ||x_i - \mu_k|| \rightarrow \min\limits_C,
$$

здесь $C$ – множество кластеров мощности $K$, $\mu_k$ – центроид кластера $C_k$.

Это довольно логично, поскольку мы хотим, чтобы точки распологались кучно возле центров своих кластеров. Но минимум такого функционала будет достигаться тогда, когда кластеров столько же, сколько и точек (то есть каждая точка – это кластер из одного элемента), что довольно неэффективно. Поэтому для выбора числа кластеров мы будем воспользовались такой эвристикой: оптимально то число кластеров, начиная с которого описанный функционал $ J(C) $ падает "уже не так быстро". Формально говоря: 


$$
Q(k) = \frac{|J(C_k) - J(C_{k+1})|}{|J(C_{k-1}) - J(C_{k})| } \to \min_{k}
$$

При помощи метода локтя, мы определили, что для метода K-means оптимальное количество кластеров равно 2, так как перегиб происходит в точке k=2 .

<h1 align="center"><img src="https://github.com/NikaFortem/project_crypto__fen_2023/blob/main/pictures/метод%20локтя.png" height="300"/></h1>

И обучили модель кластеризации методом K-means для 2 кластеров. В результате, получилось, что среди 68 криптовалют только одна попала в другой кластер. То есть данная кластеризация получилась недостаточно информативной. Это может быть связано с тем, что метод K-means предпочтителен при работе с кластерами с простой геометрией, более сложные формы он может интерпретировать некорректно. Поэтому мы рассмотрели другой алгоритм, который формирует кластеры в рамках заданнной окрестности, то есть метод **DBSCAN**.

## Кластеризация методом DBSCAN

**DBSCAN (Density-based spatial clustering of applications with noise)** - это алгоритм, основанный на плотности — если дан набор объектов в некотором пространстве, алгоритм группирует вместе объекты, которые расположены близко и помечает как выбросы объекты, которые находятся в областях с малой плотностью (ближайшие соседи которых лежат далеко). Алгоритм имеет два основных гиперпараметра:

- `eps` &mdash; радиус рассматриваемой окрестности
- `min_samples` &mdash; число соседей в окрестности

Метод DBSCAN умеет хорошо искать кластеры сложной формы.

DBSCAN понимает где какая плотность точек. Перед его запуском на наших данных подумали о том, какие параметры выбрать.

**Параметр `min_samples`**, минимальное число чекинов в кластере, мы взяли равным $4$, чтобы избавиться от маргинальных кластеров по 1-2-3 наблюдения, но при этом сохранить осмысленность, так как всего мы рассмотрели 68 разных криптовалют.

**Параметр `eps`**

Проанализировав диаграммы соотношения доходности/волатильности, доходности/VaR, мы определили, что:
- доходность колеблется 0 до 0.007, при этом основное сосредоточение точек в пределах от 0.002 до 0.005
- волатильность колеблется от 0 до 0.14, при этом основное сосредоточение точек в пределах от 0.05 до 0.09
- VaR колеблется от -0.12 до 0, при этом основное сосредоточение точек в пределах от -0.12 до -0.07
- коэффициент Шарпа колеблется от -0.4 до -0.07

Мы обучили модель кластеризации для `eps` от 0.005 до 0.1, чтобы учесть и более мелкие колебания доходности, и более значительные коэффициента Шарпа и выбрали среди них оптимальный.

<h1 align="center"><img src="https://github.com/NikaFortem/project_crypto__fen_2023/blob/main/pictures/epsilon.png" height="300"/></h1>

Чтобы избежать кластеров с минимальным значением криптовалют в них, будем рассматривать не максимальное значение кластеров, а k = 5. Для этого будем считать eps=0.015 .

Итого, мы обучили модель кластеризации методом DBSCAN для `min_samples` = 4 и `eps` = 0.015 . 

Всего получилось 4 кластера:
- метка "0" - 5 криптовалют
- метка "1" - 34 криптовалюты
- метка "2" - 17 криптовалют
- метка "3" - 5 криптовалют
- выбросы (метка "-1") - 7 криптовалют

На графиках довольно легко можно заметить получившиеся кластеры. 

<h1><img src="https://github.com/NikaFortem/project_crypto__fen_2023/blob/main/pictures/clast_1.png" height="260"/>
<img src="https://github.com/NikaFortem/project_crypto__fen_2023/blob/main/pictures/clast_2.png" height="260"/>
<img src="https://github.com/NikaFortem/project_crypto__fen_2023/blob/main/pictures/clast_3.png" height="260"/></h1>

У каждого из них есть свои особенности:

## Криптовалюты первого кластера:
- только монеты
- используются как платежные средства или для проведения транзакций
- доходность [0.0007; 0.003]
- волатильность [0.053; 0.061]
- VaR [-0.094; -0.077]
- коэффициент Шарпа [0.29; 0.32]

## Криптовалюты второго кластера:
- монеты и токены
- используются в основном как платежное средство, технический токен для биржи или трейдинга
- доходность [0.00002; 0.005]
- волатильность [0.06; 0.089]
- VaR [-0.109; -0.07]
- коэффициент Шарпа [-0.29; -0.19]

## Криптовалюты третьего кластера:
- монеты и токены
- используются в основном для обеспечения операций на блокчейне, как смарт-конракты некоторых реальных активов
- доходность [0.003; 0.006]
- волатильность [0.07; 0.094]
- VaR [-0.12; -0.094]
- коэффициент Шарпа [-0.193; -0.153]

## Криптовалюты четвертого кластера:
- монеты и токены
- обеспечивают функционирование платформ для смарт-контрактов и искуственного интеллекта или используются как utlity token
- доходность [0.005; 0.0083]
- волатильность [0.096; 0.11]
- VaR [-0.1046; -0.1219]
- коэффициент Шарпа [-0.1138; -0.1323]

# Выводы:

Проанализировав ситуацию на рынке криптовалют в 2020-2023 годах, мы пришли к следующим выводам:

- тип криптовалюты (coin / token) в 95% случаев не влияет на рыночное поведение криптовалют;
- на основе рыночных показателей можно сформировать сегменты криптовалют с похожим рыночным поведением;
- метод формирования кластеров в рамках заданной окрестности (DBSCAN) в отношении криптовалютного рынка оказывается боллее эффективным, чем метод K-means.

С практической точки зрения, полученная кластеризация может быть эффективна применена для составления криптовалютных портфелей. Поскольку в рамках одного кластера криптовалюты обладают схожим рыночным поведением, для диверсификации портфеля и уменьшения рисков оптимальней включать в портфель криптовалюты из разных кластеров (не является инвестиционной рекомендацией).




















