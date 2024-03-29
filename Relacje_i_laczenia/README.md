
## Wyjaśnienie komend użytych w przykładowych symulacjach problemów biznesowych

### Problem biznesowy 1: 
Szef poprosił Cię o listę wszystkich klientów(imię, nazwisko, id), którzy wykonali zakupy w naszym sklepie.

### Zapytanie SQL:

```sql
SELECT DISTINCT customer.customer_id, first_name, last_name
FROM customer
INNER JOIN payment ON customer.customer_id = payment.customer_id
```

### Opis działania:

Zapytanie to służy do wyodrębnienia unikalnych rekordów klientów, którzy dokonali zakupów w sklepie, uwzględniając ich identyfikatory, imiona oraz nazwiska. Proces ten składa się z kilku kroków:

- `SELECT DISTINCT customer.customer_id, first_name, last_name`: Polecenie to wybiera unikalne wartości trzech kolumn: identyfikator klienta (`customer.customer_id`), imię (`first_name`) i nazwisko (`last_name`) z tabeli `customer`. Użycie słowa kluczowego `DISTINCT` zapewnia, że każdy klient zostanie wymieniony tylko raz, nawet jeśli dokonał wielu zakupów.

- `FROM customer`: Określa tabelę `customer` jako źródło danych dla zapytania. Jest to tabela zawierająca dane personalne klientów.

- `INNER JOIN payment ON customer.customer_id = payment.customer_id`: Dokonuje wewnętrznego połączenia (`INNER JOIN`) tabeli `customer` z tabelą `payment`, bazując na wspólnym polu `customer_id`. To połączenie umożliwia złączenie danych klienta z jego płatnościami. Warunek `ON` określa, jakie pola z obu tabel są porównywane w celu dokonania złączenia — w tym przypadku jest to `customer_id`.

### Problem biznesowy 2:
Kalifornijskie prawo dotyczące podatku od sprzedaży się zmieniło i musimy powiadomić o tym naszych klientów za pośrednictwiem poczty elektronicznej. Jakie są e-mail osób mieszkających w Kalifornii.

### Zapytanie SQL:
```sql
SELECT address.district, customer.email
FROM customer
INNER JOIN address ON customer.address_id = address.address_id
WHERE address.district = 'California'
```

### Opis Działania:

1. **SELECT address.district, customer.email**: Polecenie to wybiera dwie kolumny: `district` z tabeli `address` oraz `email` z tabeli `customer`. Celem jest uzyskanie adresów e-mail klientów, którzy znajdują się w określonym dystrykcie, w tym przypadku 'California'.

2. **FROM customer**: Określa tabelę źródłową dla zapytania, którą jest `customer`. Jest to tabela zawierająca informacje o klientach, w tym ich adresy e-mail.

3. **INNER JOIN address ON customer.address_id = address.address_id**: Dokonuje wewnętrznego łączenia (INNER JOIN) tabeli `customer` z tabelą `address`, bazując na wspólnym polu `address_id`. Takie połączenie umożliwia skorelowanie każdego klienta z jego adresem. Warunek `ON` określa, które pola z obu tabel są porównywane w celu dokonania złączenia – w tym wypadku jest to `address_id`. Dzięki temu złączeniu możemy połączyć dane adresowe z informacjami o klientach, aby zidentyfikować, którzy z nich mieszkają w Kalifornii.

4. **WHERE address.district = 'California'**: Klauzula `WHERE` filtruje wyniki zapytania tak, aby zawierały tylko te rekordy, dla których wartość w kolumnie `district` tabeli `address` jest równa 'California'. Dzięki temu zapytanie zwróci informacje tylko o tych klientach, którzy mieszkają w określonym dystrykcie i którzy będą musieli zostać poinformowani o zmianie prawa dotyczącego podatku od sprzedaży.

