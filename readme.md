# Dyktowanie do Excela (Voice-to-Excel Web App)

Prosta, lekka aplikacja webowa stworzona z myślą o szybkiej pracy mobilnej poprzez dyktowanie. Aplikacja automatycznie przetwarza mowę na tekst (zamieniając słowne liczby na cyfry), wyłapuje z tekstu konkretne jednostki (np. kartony, sztuki, wagę) za pomocą wyrażeń regularnych (Regex) i wysyła je w czytelnym formacie JSON do Make.com, który zapisuje dane wiersz po wierszu w Microsoft 365 Excel.

## Funkcjonalności

* **Normalizacja mowy:** Automatyczna zamiana słownych liczb (np. „dwa”, „pięć”) na cyfry („2”, „5”), co ułatwia pracę z klawiaturą ekranową w telefonie.
* **Elastyczny system reguł (Regex):** Łatwe w konfiguracji reguły wyszukiwania pozwalają na szybkie dopisywanie nowych jednostek (kartony, sztuki, kg itp.).
* **Integracja z Make.com:** Wysyłanie paczki danych przez Webhook (`fetch` API) w strukturze tablicowej, idealnej do obsługi przez moduł *Iterator*.
* **Wszystko w jednym pliku:** Lekki kod HTML/JS bez zewnętrznych bibliotek, gotowy do natychmiastowego uruchomienia.

## Jak to działa?

1. Użytkownik dyktuje lub wpisuje tekst (np. *"Mam dwa kartony i pięć sztuk"*).
2. Skrypt normalizuje słowa na cyfry: *"Mam 2 kartony i 5 sztuk"*.
3. Silnik Regex analizuje tekst zgodnie ze zdefiniowanymi regułami.
4. Po kliknięciu przycisku wysyłania, aplikacja pakuje dane w tablicę obiektów i wysyła je metodą POST na adres Webhooka w Make.com.

## Konfiguracja w Make.com

Aby dane lądowały w Excelu jedna pod drugą (w osobnych wierszach):
1. Odbierz dane za pomocą modułu **Webhooks**.
2. Użyj modułu **Flow Control -> Iterator** i jako tablicę wskaż zmienną `items`.
3. Podłącz moduł **Microsoft 365 Excel -> Add a Row**.
4. Zmapuj pola z Iteratora:
   - Kolumna kategorii/nazwy -> `category`
   - Kolumna wartości/ilości -> `value`

## Jak uruchomić?

1. Pobierz plik HTML z aplikacją.
2. Otwórz kod i wklej swój unikalny adres webhooka z Make.com w zmiennej `webhookUrl`.
3. Uruchom plik w dowolnej przeglądarce (najlepiej na telefonie z włączonym dyktowaniem).