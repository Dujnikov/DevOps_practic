GET /_cat/indices?v - просмотр достпуных индексов
DELETE /name_index - удаление индекса
PUT /PUT /name_index - создание индекса
GET /index_name?pretty - посмотреть содержимое индекса
GET /index_name/_search?pretty - - посмотреть все данные под этим индексом

То же самое, но напрямую через ElasticSearch
curl -X PUT 'localhost:9200/name_index - создание индекса (name_index - имя индекса)
curl -X DELETE 'localhost:9200/name_index - удаление индекса (name_index - имя индекса)
curl -H 'Content-Type: application/json' -X GET https://localhost:9200/index_name?pretty - посмотреть содержимое индекса
curl -H 'Content-Type: application/json' -X GET https://localhost:9200/index_name/_search?pretty - посмотреть все данные под этим индексом


path.repo: ["/tmp"]

В кибане зарегить хранилище

curl -XPUT 'http://localhost:9200/_snapshot/tmp?pretty=true' -d '{"type":"fs","settings":{"compress":true,"location":"/tmp"}}'

создать снапшот

curl -XPUT 'http://localhost:9200/_snapshot/tmp/snapshot_$dt? -d '{"indices":"logstash-2022.08.08"}'

проверить снэпшот

curl -XPUT http://localhost:9200/_snapshot/tmp/logstash-2022.08.08?wait_for_completion=false -d '{"indices":"logstash-2022.08.08"}'

проверить статус снэпшота

curl -XGET 'http://localhost:9200/_snapshot/tmp/logstash-2022.08.08/_status?pretty=true'

закрыть индекс

curl -XPOST 'localhost:9200/logstash-2022.08.08/_close'

ресторить

curl -XPOST 'http://localhost:9200/_snapshot/tmp/logstash-2022.08.08/_restore'