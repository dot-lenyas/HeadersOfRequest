# Протокол HTTP. Основы работы с консолью разработчика
## Эссе
Проанализировать заголовки решил я за одним делом, которое присуще всем нам, на нашем же любимом сайте. rt.pornhub.com.
p.s пока писал эссе, зашла мама в комнату, и помогла мне его дописать.

### При переходе на сайт отправляется следующий запрос: 
```
:authority: rt.pornhub.com
:method: GET
:path: /
:scheme: https
accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
accept-encoding: gzip, deflate, br
accept-language: ru-RU,ru;q=0.9,en-US;q=0.8,en;q=0.7
cache-control: max-age=0
cookie: ua=27fc5e5ade0b76b1f440c4528a5ad1b3; platform=pc; bs=nnlp7m6r658asoe82usixow37g9qgavp; ss=859634674973549172; fg_ec733c207a91321a9ed22b01850e820e=60024.100000; atatusScript=hide; _ga=GA1.2.931423360.1632972301; _gid=GA1.2.549482546.1632972301; _hjid=63968aa6-7a13-4d44-8aa3-0b95a8443cfb; _hjFirstSeen=1; _hjAbsoluteSessionInProgress=0
sec-ch-ua: "Chromium";v="94", "Google Chrome";v="94", ";Not A Brand";v="99"
sec-ch-ua-mobile: ?0
sec-ch-ua-platform: "Windows"
sec-fetch-dest: document
sec-fetch-mode: navigate
sec-fetch-site: none
sec-fetch-user: ?1
upgrade-insecure-requests: 1
user-agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/94.0.4606.54 Safari/537.36
```
Заголовок accept-encoding объявляет, какие кодировки контента и алгоритмы сжатия поддерживает браузер. В данном случае браузер объявляет о том, что поддерживает методы сжатия gzip, deflate и br.

Заголовок accept-language сообщает серверу, какие языки клиент понимает и какая локаль предпочтительнее. Также в заголовке может указываться параметр q, который устанавливает предпочтение в выборе данной локали.

Заголовок cache-control устанавливает инструкции для кеширования данных. В данном случае задается максимальное время в течение которого ресурс будет считаться актуальным - 0 секунд.

Заголовок upgrade-insecure-requests говорит о том, хотим ли мы получить сайт в защищенном режиме. В данном случае браузер запрашивает сайт именно в защищенном режиме (1).

Заголовок user-agent позволяет идентифицировать браузер. Файл агента пользователя чаще всего включает в себя сведения о браузере, его версии, используемом устройстве, операционной системе и механизме веб-рендеринга.

### В ответ мы же получаем:
```
content-encoding: gzip
content-type: text/html; charset=UTF-8
date: Thu, 30 Sep 2021 03:42:07 GMT
rating: RTA-5042-1996-1400-1577-RTA
server: openresty
vary: User-Agent
x-frame-options: SAMEORIGIN
x-request-id: 6155320F-42FE722901BB3BD9-1C44F65
```
Content-Encoding - это сущность заголовка, используемая для сжатия медиа-типа. При наличии её значение определяет кодировку, применённую к сущности body. Это позволяет клиенту информацию как декодировать body, чтобы получить медиа-тип ссылающийся на  заголовок Content-Type 

Заголовок-сущность Content-Type используется для того, чтобы определить MIME тип ресурса. В ответах сервера заголовок Content-Type сообщает клиенту, какой будет тип передаваемого контента.

Заголовок date содержит дату и время, в которое сообщение было создано.

Заголовок ответа Vary определяет, как сопоставить будущие заголовки запроса, чтобы решить, можно ли использовать кешированный ответ, а не запрашивать новый с исходного сервера. Он используется сервером для указания того, какие заголовки он использовал при выборе представления ресурса в алгоритме согласования контента.

## Далее решил я перейти на видео, на обложки было 2 мужика, ну а я че.
### Внимательно смотрел на запросы, ну и при переходе, увидел я такой запрос:
```
:authority: ev-h.phncdn.com
:method: GET
:path: /hls/videos/201909/25/250733551/,1080P_4000K,720P_4000K,480P_2000K,240P_400K,_250733551.mp4.urlset/seg-30-f2-v1-a1.ts?validfrom=1632970782&validto=1632977982&ipa=217.150.72.220&hdl=-1&hash=LRDOqlXrMNynbbbYVf8ONNGwrps%3D
:scheme: https
accept: */*
accept-encoding: gzip, deflate, br
accept-language: ru-RU,ru;q=0.9,en-US;q=0.8,en;q=0.7
origin: https://rt.pornhub.com
referer: https://rt.pornhub.com/
sec-ch-ua: "Chromium";v="94", "Google Chrome";v="94", ";Not A Brand";v="99"
sec-ch-ua-mobile: ?0
sec-ch-ua-platform: "Windows"
sec-fetch-dest: empty
sec-fetch-mode: cors
sec-fetch-site: cross-site
user-agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/94.0.4606.54 Safari/537.36
```

Заголовок запроса Referer содержит URL исходной страницы, с которой был осуществлён переход на текущую страницу. Заголовок Referer позволяет серверу узнать откуда был осуществлён переход на запрашиваемую страницу. Сервер может анализировать эти данные, записывать их в логи или оптимизировать процесс кеширования.

### Ответ же будет такой:
```
accept-ranges: bytes
access-control-allow-headers: Server,Range,Content-Length,Content-Range
access-control-allow-methods: GET,HEAD,OPTIONS
access-control-allow-origin: https://rt.pornhub.com
access-control-expose-headers: Server,Range,Content-Length,Content-Range
cache-control: max-age=10631119
content-length: 289144
content-type: video/MP2T
date: Thu, 30 Sep 2021 03:59:52 GMT
expires: Tue, 31 Aug 2021 10:34:45 GMT
timing-allow-origin: *
x-cdn-diag: lon1-16029-4-34492-h-0-0---;16035-182-45688----0-0-1
```
HTTP Заголовок ответа Accept-Ranges -- это маркер, который использует сервер, чтобы уведомить клиента о поддержке "запросов по кускам". Его значение указывает единицу измерения, которая может быть использована для определения диапазона чтения. При наличии заголовка Accept-Ranges, браузер может попытаться возобновить прерванную загрузку, а не запускать её с самого начала.

Заголовок Content-Length указывает размер отправленного получателю тела объекта в байтах

Общий заголовок Cache-Control используется для задания инструкций кеширования как для запросов, так и для ответов. Инструкции кеширования однонаправленные: заданная инструкция в запросе не подразумевает, что такая же инструкция будет указана в ответе

# Итог
## Я кончил

писать эссе
