#Log Compaction

Log Compaction to sposób na optymalizcję danych przetwarzanych przez kafkę. 
Log to jest opis partycji (_partition_) gdzie pojawiają się message.
Chodzi o to że każda wiadomość może być wysłana względem klucza, 
a to oznacza że jeśli mamy klucz to każda wiadomość z tym samym kluczem trafi zawsze na tę samą
partycję. To powoduje że można zrobić po pewnym czasie optymalizację wiadomości i pozbyć sie 
nadmiarowych informacji, które już są nam niepotrzebne/nieaktualne. Przykład:
Mamy wiadomości składające sie z klucza i wartości:\
```
Mark, salary: 1000
Tom,  salary: 3000
Mark, salary: 5000
```
gdzie `,` rozdziela klucz i wartość. \
Po optymalizacji kafka może usunąć stary klucz,wartość żeby zostawić tylko ostatnią wartość najbardziej
aktualną. Po takim kompaktowaniu przy wyświetleniu wszystkich wiadomości wynik będzie następujący:
```
Tom, salary: 3000
Mark, salary: 5000
```
Jest to rodzaj snapshotu, czyli olewamy wcześniejsze wiadomości i skupiamy się na ostatniej wiadomości 
która reprezentuje ostatnią aktualną wartość.