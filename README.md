## project_crypto__fen_2023
Репозиторий для проекта по анализу данных на ФЭН 2023. 

# Тема проекта: **"Классификация криптовалют на основе их рыночных показателей"**

## Состав группы: Виктория Карпейкина, Юлия Щучкина, Максим Бочаров

# Данные : 

В рамках нашего проекта мы проанализировали котировки топ-68 криптовалют за период с 01.01.2020 по 10.05.2023, полученные с криптовалютной
биржи Binance

# Первичный анализ данных:

На основе первичного анализа данных были сделаны выводы о динамике криптовалют за рассматриваемый период. В течение последних 3 динамика рынка криптовалют была довольно неодназначной. Однако можно сказать, что с начала 2020 года к маю 2023 года цены криптовалют выросли (хорошо видно на примере 3 из 5 рассмотренных криптовалют: BTC, ETH, BNB). 

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
   (https://data.nasdaq.com/data/USTREASURY/YIELD-treasury-yield-curve-rates).

   Однако в отличии от криптовалютной биржи Binance, с которой взяты данные о котировках криптовалют, биржа NASDAQ, где торгуются ценные бумаги, собирает      статистику только в будние дни, так как по входным торги не идут. Поэтому далее в отношении доходностей и прочих показателей были рассмотрены только        рабочие дни.

   Поскольку ранее мы рассматривали ежедневную доходность криптовалют, для подсчета коэффициента Шарпа были рассмотрены ежедневные колебания доходности,      связанные с колебаниями стоимости treasury (купонную доходность здесь не учитывали), самых краткосрочных US TREASURY, то есть со сроком обращения 1        месяц.
  
### Прочие показатели

   Также для боллее наглядного представления динамики рынка криптовалют были рассмотрены такие показатели, как:
   - логарифмированные цены
   - накопленная доходность
   - Average True Range (средний истинный диапозон)
















