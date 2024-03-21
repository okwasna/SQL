

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


### Opis działania:
Zapytanie SQL służy do określenia liczby filmów z kategorii ratingu 'R', które mają określony zakres kosztów zastępczych. Wykorzystuje ono następującą logikę:

- `SELECT COUNT(rating)`: Polecenie to wylicza liczbę wystąpień kolumny `rating` w tabeli, co w efekcie da nam liczbę filmów spełniających podane kryteria.
- `FROM film`: Określa tabelę `film` jako źródło danych do analizy.
- `WHERE rating='R'`: Filtruje filmy tak, aby brane pod uwagę były jedynie te z oceną 'R', czyli przeznaczone dla widzów dorosłych.
- `AND replacement_cost BETWEEN 5 AND 15`: Dodatkowo, warunek ten ogranicza wyniki do filmów, których koszt zastępczy mieści się w przedziale od 5 do 15 dolarów. 





