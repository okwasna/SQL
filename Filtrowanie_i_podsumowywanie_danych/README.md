

## Wyjaśnienie komend użytych w przykładowych symulacjach problemów biznesowych

### Problem biznesowy 1: 
Szef chce wynagrodzić TOP 10 klientów, którzy wydali najwięcej w naszym sklepie.

### Zapytanie SQL:
```sql
SELECT customer_id, SUM(amount) AS total_spent
FROM payment
GROUP BY customer_id
ORDER BY total_spent DESC
LIMIT 10;
```

### Opis działania:
Zapytanie to ma na celu wyselekcjonowanie dziesięciu klientów, którzy łącznie wydali najwięcej pieniędzy w naszym sklepie. Do realizacji tego zadania stosuje się następujące kroki:

- `SELECT customer_id, SUM(amount) AS total_spent`: Wybieram identyfikator klienta (`customer_id`) oraz sumuję wszystkie jego płatności (`amount`), tworząc alias `total_spent` dla tej sumy.
- `FROM payment`: Dane są pobierane z tabeli `payment`, która zawiera informacje o transakcjach dokonanych przez klientów.
- `GROUP BY customer_id`: Dane są grupowane według `customer_id`, co umożliwia sumowanie wydatków dla każdego klienta indywidualnie.
- `ORDER BY total_spent DESC`: Wyniki są sortowane od największej do najmniejszej sumy wydatków, dzięki czemu na górze listy znajdą się klienci, którzy wydali najwięcej.
- `LIMIT 10`: Na końcu zapytania ustalamy limit na 10 rekordów, aby wyświetlić tylko dziesięciu klientów z największymi wydatkami.


### Problem biznesowy 2: 
Firma chce wystartować z akcją marketingową i potrzebuje adresy mailowe wszystkich naszych klientów wraz z imieniem i nazwiskiem.

### Zapytanie SQL:
```sql
SELECT first_name, last_name, email
FROM customer;
```

### Opis działania:
Zapytanie to ma na celu wyświetlenie wszystkich adresów mailowych naszych klientów, wraz z imieniem i nazwiskiem, aby wysłać e-mail:

- `SELECT first_name, last_name, email `: Wybieram imię (`first_name`), nazwisko (`last_name`), adres mailowy klienta (`email`).
- `FROM customer`: Dane są pobierane z tabeli `customer`, która zawiera informacje o klientach.


### Problem biznesowy 3:
Chcemy się upewnić, że wszyscy nasi klienci podali adres e-mailowy, co jest wymaganym polem w naszym formularzu rejestracyjnym, aby akcja marketingowa przebiegła poprawnie.

#### Zapytanie SQL:
```sql
SELECT first_name, last_name, email
FROM customer
WHERE email IS NULL OR email = '';
```

### Opis działania:
Celem tego zapytania jest identyfikacja klientów, którzy nie wypełnili obowiązkowego pola adresu e-mail w formularzu rejestracyjnym. Proces ten składa się z następujących kroków:

- `SELECT first_name, last_name, email`: Polecenie to wybiera imiona, nazwiska oraz adresy e-mail klientów z tabeli `customer`.
- `FROM customer`: Tabela `customer` jest miejscem, z którego pobierane są dane o klientach.
- `WHERE email IS NULL OR email = ''`: Warunek w klauzuli `WHERE` filtruje wyniki w celu znalezienia rekordów, w których pole adresu e-mailowego nie zostało wypełnione (jest `NULL`) lub jest puste (`email = ''`).

### Problem biznesowy 4:
**Analiza dostępności filmów z określonym kosztem zastępczym**

Celem jest określenie liczby filmów z kategorii ratingu 'R', dostępnych w przedziale cenowym od 5 do 15 dolarów, aby można było zarządzać zapasami filmów oraz planować promocje.

#### Zapytanie SQL:
```sql
SELECT COUNT(rating) FROM film
WHERE rating='R'
AND replacement_cost BETWEEN 5 AND 15;
``` 
### Opis działania:
Zapytanie SQL służy do określenia liczby filmów z kategorii ratingu 'R', które mają określony zakres kosztów zastępczych. Wykorzystuje ono następującą logikę:

- `SELECT COUNT(rating)`: Polecenie to wylicza liczbę wystąpień kolumny `rating` w tabeli, co w efekcie da nam liczbę filmów spełniających podane kryteria.
- `FROM film`: Określa tabelę `film` jako źródło danych do analizy.
- `WHERE rating='R'`: Filtruje filmy tak, aby brane pod uwagę były jedynie te z oceną 'R', czyli przeznaczone dla widzów dorosłych.
- `AND replacement_cost BETWEEN 5 AND 15`: Dodatkowo, warunek ten ogranicza wyniki do filmów, których koszt zastępczy mieści się w przedziale od 5 do 15 dolarów. 


### Problem biznesowy 5:
**Premiowanie pracownika z największą liczbą przetworzonych płatności**

#### Zapytanie SQL:
```sql
SELECT staff_id, COUNT(*) AS number_of_payments
FROM payment
GROUP BY staff_id
ORDER BY number_of_payments DESC
LIMIT 1;
```

### Opis działania:
Celem zapytania jest identyfikacja pracownika, który przetworzył największą liczbę płatności. Wyróżnienie tego pracownika premią ma na celu podkreślenie znaczenia liczby transakcji, a nie ich wartości. Oto jak zapytanie osiąga ten cel:

- `SELECT staff_id, COUNT(*) AS number_of_payments`: Wybieramy identyfikator pracownika (`staff_id`) i liczymy całkowitą liczbę płatności (`COUNT(*)`), które przypisane są do każdego pracownika, tworząc sumaryczną liczbę jako `number_of_payments`.
- `FROM payment`: Tabela `payment` jest używana jako źródło danych, zawierająca informacje o wszystkich transakcjach.
- `GROUP BY staff_id`: Grupowanie według `staff_id` umożliwia zliczenie płatności dla każdego pracownika oddzielnie.
- `ORDER BY number_of_payments DESC`: Sortowanie wyników w porządku malejącym po liczbie płatności sprawia, że na górze znajdą się pracownicy z największą liczbą transakcji.
- `LIMIT 1`: Ograniczamy wyniki do jednego rekordu, aby wybrać pracownika z najwyższą liczbą przetworzonych płatności.


### Problem biznesowy 6:
**Identyfikacja klientów kwalifikujących się do promocji za wydatki przekraczające 110 USD u pracownika o identyfikatorze 2**

#### Zapytanie SQL:
```sql
SELECT customer_id, SUM(amount) 
FROM payment
WHERE staff_id=2
GROUP BY customer_id
HAVING SUM(amount) > 110;
```

### Opis działania:
Celem zapytania jest znalezienie klientów, którzy wydali łącznie więcej niż 110 USD u pracownika o identyfikatorze 2, aby mogli skorzystać z promocji -10% na kolejne zakupy. Zapytanie to jest skonstruowane, aby identyfikować te osoby, które spełniają warunki promocji. Oto, jak zapytanie osiąga ten cel:

- `SELECT customer_id, SUM(amount)`: Zapytanie wybiera identyfikator klienta (`customer_id`) i sumuje kwoty (`SUM(amount)`) wszystkich jego płatności, aby określić całkowitą kwotę wydaną przez każdego klienta.

- `FROM payment`: Wykorzystywana jest tabela `payment`, która zawiera informacje o płatnościach dokonywanych przez klientów.

- `WHERE staff_id=2`: Filtr aplikowany do zapytania, ograniczający wyniki do płatności przetworzonych przez pracownika o identyfikatorze 2. Zapewnia to, że promocja jest stosowana tylko do transakcji obsłużonych przez tego pracownika.

- `GROUP BY customer_id`: Zapytanie grupuje wyniki według identyfikatora klienta (`customer_id`), co umożliwia agregację i obliczenie sumy wydatków dla każdego klienta indywidualnie.

- `HAVING SUM(amount) > 110`: Klauzula `HAVING` jest używana do filtrowania wyników, tak aby w zestawieniu końcowym znaleźli się tylko klienci, którzy wydali więcej niż 110 USD. Dzięki temu, zidentyfikowane zostają tylko te osoby, które kwalifikują się do otrzymania promocji.






