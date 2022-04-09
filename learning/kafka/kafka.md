#Kafka
https://learning.oreilly.com/videos/apache-kafka-series
##Podstawowa struktura
* kafka jest uruchamiana jako klaster
  * klaster zawiera brokery _(brokers)_, ktore sa fizycznymi serverami
  * brokery posiadaja wiedze o sobie w obrebie klastra
  * zawsze jest jeden broker leader, jak padnie to inny broker jest wybierany na leadera za pomoca _zookeeper'a_
  * brokery replikuja dane pomiedzy soba, tak ze jak jeden padnie to drugi ma dane u siebie i moze byc uzyty 
  zamiast tego co padl
  * do zarzadzania brokerami jest _Zookeeper_: 
    * trzyma liste wszystkich brokerow
    * wybiera leadera dla partycji
    * wysyla do kafki informacje jesli powstnie jakis nowy topic, albo jakis broker umrze lub pojawi sie nowy

* Kafka na brokerze tworzy _topiki(topics)_  _partycje(partitions)_
  * kazdy _topic_ posiada partycje, moze ich posiadac kilka
  * kazda partycja przechowuje strumien danych, strumien danych jest podzielony na offsety, czyli dane ktore przychodza
  w kolejnosci do strumienia.
    * strumien danych jest przechowywany w porzadku w jakim trafil do partycji
    * dane wysylane do kafki laduja w dowolnej partycji, o ile nie zostal uzyty klucz, ktory moze przyporzadkowac do 
    ktorej partycji powinien trafic strumien danych
    * dane wysylane do kafki _(producer)_ moga byc potwierdzone jako odebrane na trzy sposby (3 strategie potwierdzenia):
      * acks = 0 - traktowane ze wyslane od razu ale potwierdzenia ze zostaly odebrane nie ma wiec jak cos sie nie zapisze 
      to potem nie ma opcji zeby operacja odczytu wiadomosci zostala powtorzona _(data lost)_
      * acks = 1 - traktowane jako odebrane tylko wtedy kiedy broker leader da acknowledge - potencjalnie dane zapisane 
      ale tylko w brokerze czyli jak sie po odebraniu wiadomosci ale przed replikacja broker wywroci to wciaz jest to 
      _data lost_
      * acks = all -  traktowane jako odebrane tylko wtedy kiedy broker leader i repliki daja aknowledge ze zapisane
    * dane odbierane przez konsumera _(consumer)_ sa pobierane takze w kolejnosci ich wystepowania
    * consumer komituje do kafki ze przetworzyl konkretną daną, zapisujac tym samym do ktorego ofestu w prtycji dane 
    juz zostaly przetworzone. 
    W ten sposob jak padnie consumer przed zakonczeniem procesowania danego ofsetu to inny konsumer bedzie mogl zaczac od 
    tego momentu jeszcze raz.
      * sa 3 typy komitowania ofsetu _(commit offset)_
        * at most once -commit idzie od razu kiedy message jest odebrany przez consumera
        * at least once (preferowany sposob) - commit offestu jest robiony kiedy consumer przetworzy dany offset
        * exactly once - commit ktory idzie pomiedzy kafkami
    * consumery pracuja w grupach, kazda partycja moze pracowac tylko z jednym konsumerem z danej grupy, jesli w grupie
    jest wiecej consumerow niz partycji to nadwyzkowy consumer bedzie nieaktywny