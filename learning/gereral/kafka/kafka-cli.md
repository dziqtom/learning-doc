#Komendy CLI dla kafki 

##Topic
* zakladanie topica o nazwie _first_topic_\
`kafka-topics --bootstrap-server localhost:9092 --topic first_topic --create`
* wyswietlanie wszystkich topicow\
`kafka-topics --bootstrap-server localhost:9092 --list`
* wyswietlanie info o topicu _first_topic_\
`kafka-topics --bootstrap-server localhost:9092 --topic first_topic --describe`
* usuwanie topica _first_topic_\
`kafka-topics --bootstrap-server localhost:9092 --delete --topic first_topic`

##Consumer
* wlaczanie kafka consumer'a na czytanie z kolejki _first_topic_\
`kafka-console-consumer --bootstrap-server localhost:9092 --topic first_topic`\
* wlaczanie kafka consumera na czytanie z kolejki _first_topic_ w grupie _tweeter-app_\
`kafka-console-consumer --bootstrap-server localhost:9092 --topic first_topic --group tweeter-app`
* wlacznie konsumera od poczatku dla _first_topic_ w grupie _tweeter-app_\
`kafka-console-consumer --bootstrap-server localhost:9092 --topic first_topic --group tweeter-app --from-beginning`