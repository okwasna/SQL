
## Wyjaśnienie komend użytych w przykładowych symulacjach problemów biznesowych

### Problem biznesowy 1: 
Szef poprosił Cię o listę wszystkich klientów(imię, nazwisko, id), którzy wykonali zakupy w naszym sklepie.

###Zapytanie SQL:

```sql
SELECT DISTINCT customer.customer_id, first_name, last_name
FROM customer
INNER JOIN payment ON customer.customer_id = payment.customer_id
```

###Opis działania:

Zapytanie to służy do wyodrębnienia unikalnych rekordów klientów, którzy dokonali zakupów w sklepie, uwzględniając ich identyfikatory, imiona oraz nazwiska. Proces ten składa się z kilku kroków:

- `SELECT DISTINCT customer.customer_id, first_name, last_name`: Polecenie to wybiera unikalne wartości trzech kolumn: identyfikator klienta (`customer.customer_id`), imię (`first_name`) i nazwisko (`last_name`) z tabeli `customer`. Użycie słowa kluczowego `DISTINCT` zapewnia, że każdy klient zostanie wymieniony tylko raz, nawet jeśli dokonał wielu zakupów.

- `FROM customer`: Określa tabelę `customer` jako źródło danych dla zapytania. Jest to tabela zawierająca dane personalne klientów.

- `INNER JOIN payment ON customer.customer_id = payment.customer_id`: Dokonuje wewnętrznego połączenia (`INNER JOIN`) tabeli `customer` z tabelą `payment`, bazując na wspólnym polu `customer_id`. To połączenie umożliwia złączenie danych klienta z jego płatnościami. Warunek `ON` określa, jakie pola z obu tabel są porównywane w celu dokonania złączenia — w tym przypadku jest to `customer_id`.
