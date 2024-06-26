
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

### Problem Biznesowy 3:

Klient chce znaleźć wszystkie filmy, w których gra aktor o imieniu Nick Wahlberg. Jest to typowe zadanie w branży rozrywkowej, które pomaga klientom szybko znaleźć treści związane z konkretnymi aktorami, na które mogą chcieć zwrócić uwagę lub które chcą oglądać. Wiedza o tym, w jakich filmach występuje dany aktor, może również wspierać działania marketingowe i promocyjne związane z nowymi wydaniami lub rekomendacjami filmów.

### Zapytanie SQL:

```sql
SELECT film.title, actor.first_name, actor.last_name 
FROM film
INNER JOIN film_actor ON film.film_id = film_actor.film_id
LEFT JOIN actor ON actor.actor_id = film_actor.actor_id
WHERE first_name= 'Nick' AND last_name= 'Wahlberg'
```

### Opis Działania:

1. **SELECT film.title, actor.first_name, actor.last_name**: Polecenie to instruuje bazę danych, aby wybrała tytuły filmów oraz imiona i nazwiska aktorów. Jest to zestaw danych, który zostanie zwrócony jako wynik zapytania, pozwalając klientowi zidentyfikować filmy z udziałem Nicka Wahlberga.

2. **FROM film**: Określa tabelę `film` jako punkt wyjścia dla zapytania. Jest to podstawowa tabela zawierająca informacje o filmach, w tym ich tytuły.

3. **INNER JOIN film_actor ON film.film_id = film_actor.film_id**: Ta część zapytania wykonuje wewnętrzne łączenie (INNER JOIN) tabeli `film` z tabelą `film_actor` na podstawie wspólnego klucza, którym jest `film_id`. Pozwala to na połączenie informacji o filmach z informacjami o aktorach, którzy w tych filmach występują, na podstawie relacji film-aktor.

4. **LEFT JOIN actor ON actor.actor_id = film_actor.actor_id**: Następnie zapytanie wykonuje lewe łączenie (LEFT JOIN) z tabelą `actor`, aby połączyć informacje o aktorach z poprzednio utworzonym zestawem danych. Używa klucza `actor_id` do zidentyfikowania, którzy aktorzy są związani z każdym filmem. Wybór LEFT JOIN (zamiast INNER JOIN) pozwala na zachowanie wszystkich rekordów z lewej tabeli (`film_actor`), nawet jeśli nie znajdzie się dokładne dopasowanie w tabeli `actor`, co jest szczególnie przydatne w innych scenariuszach; tutaj jednak, w kontekście tego zapytania, można by rozważyć użycie INNER JOIN, ponieważ zakładamy istnienie dopasowania.

5. **WHERE first_name= 'Nick' AND last_name= 'Wahlberg'**: Klauzula WHERE jest używana do filtrowania wyników, tak aby zwrócić tylko te rekordy, które dotyczą aktora o imieniu Nick i nazwisku Wahlberg. To ograniczenie pozwala na precyzyjne określenie, których aktorów dotyczy zapytanie.

### Problem Biznesowy 4:

W ramach inicjatywy mającej na celu wzmocnienie relacji z kluczowymi klientami, dział marketingu zamierza przeprowadzić kampanię e-mailową. Celem jest dotarcie do 10 klientów, którzy wydali najwięcej pieniędzy w naszym sklepie, przekraczając kwotę 100. Kampania ta ma na celu nie tylko podziękowanie tym klientom za ich lojalność, ale także zaoferowanie im specjalnych rabatów i zaproszeń do programów VIP.

### Zapytanie SQL:

```sql
SELECT customer.first_name || ' ' || customer.last_name AS full_name,
       customer.email,
       SUM(payment.amount) AS total_price
FROM customer
JOIN payment ON customer.customer_id = payment.customer_id
GROUP BY customer.first_name, customer.last_name, customer.email
HAVING SUM(payment.amount) > 100
ORDER BY SUM(payment.amount) DESC
LIMIT 10;
```

### Opis Działania:

- **SELECT customer.first_name || ' ' || customer.last_name AS full_name, customer.email, SUM(payment.amount) AS total_price**: Polecenie to łączy imię i nazwisko klienta w jedną kolumnę `full_name` i wybiera ich adres email oraz sumę wydatków (`payment.amount`). Użycie funkcji agregującej `SUM()` pozwala na obliczenie całkowitej kwoty wydanej przez każdego klienta.

- **FROM customer JOIN payment ON customer.customer_id = payment.customer_id**: Klauzula FROM określa tabelę źródłową (`customer`), a JOIN dołącza tabelę `payment` w celu połączenia danych o płatnościach klientów z ich rekordami. Dołączenie odbywa się poprzez porównanie identyfikatorów klientów (`customer.customer_id`) w obu tabelach.

- **GROUP BY customer.first_name, customer.last_name, customer.email**: Grupowanie wyników według imienia, nazwiska i emaila klienta zapewnia, że suma wydatków jest obliczana indywidualnie dla każdego klienta. To również umożliwia selekcję unikalnych rekordów klienta, eliminując powtórzenia.

- **HAVING SUM(payment.amount) > 100**: Klauzula HAVING filtruje zgrupowane rekordy, pozostawiając tylko te, dla których suma wydatków przekracza 100. To kryterium wyboru pozwala skupić się na klientach, którzy najwięcej wydali.

- **ORDER BY SUM(payment.amount) DESC**: Sortowanie wyników w malejącej kolejności według sumy wydatków pozwala na ustalenie, którzy klienci wydali najwięcej. 

- **LIMIT 10**: Ograniczenie wyników do 10 najwyższych sum wydatków zapewnia, że kampania e-mailowa będzie skierowana tylko do najbardziej wartościowych klientów z punktu widzenia finansowego.


### Problem Biznesowy 5:

Dział IT firmy X został poproszony o przygotowanie unikatowych adresów e-mailowych dla wszystkich obecnych klientów w systemie. Te adresy e-mail mają być używane do wewnętrznych celów komunikacyjnych, takich jak wysyłanie informacji o aktualizacjach konta, powiadomień o konserwacji systemu oraz ekskluzywnych newsletterów. Format adresu e-mail powinien składać się z pierwszej litery imienia klienta, połączonej z jego nazwiskiem (wszystko zapisane małymi literami), z dodaniem domeny `@xfirma.com` na końcu. Lista ta musi być uporządkowana według identyfikatora klienta, aby ułatwić synchronizację z obecnymi rekordami systemowymi.

### Zapytanie SQL:

```sql
SELECT LOWER(LEFT(first_name,1)) || LOWER(last_name) || '@xfirma.com' AS email, 
       first_name, 
       last_name, 
       customer_id
FROM customer
ORDER BY customer_id ASC;
```

### Opis Działania:

- **SELECT LOWER(LEFT(first_name,1)) || LOWER(last_name) || '@xfirma.com' AS email**: Polecenie to konstruuje adres e-mail dla każdego klienta, łącząc pierwszą literę imienia (używając funkcji `LEFT(first_name,1)`) z pełnym nazwiskiem (wszystko przekształcone na małe litery za pomocą funkcji `LOWER()`), a następnie dodając domenę `@xfirma.com`. Wynikowy adres e-mail jest przypisywany do aliasu `email`.

- **first_name, last_name, customer_id**: Wybierane są również imię, nazwisko oraz identyfikator klienta, aby zapewnić pełną identyfikowalność każdego rekordu i umożliwić łatwe skorelowanie adresów e-mail z istniejącymi danymi klientów.

- **FROM customer**: Klauzula FROM określa, że dane będą pobierane z tabeli `customer`, która zawiera informacje o klientach.

- **ORDER BY customer_id ASC**: Wyniki są sortowane w porządku rosnącym według identyfikatora klienta (`customer_id`). Takie uporządkowanie ułatwia pracę z danymi, zwłaszcza w przypadku synchronizacji z innymi systemami lub rekordami, gdzie konsekwentna kolejność rekordów jest kluczowa.

### Problem Biznesowy 6:

Firma XYZ, działająca w branży e-commerce, dąży do zapewnienia wyjątkowej obsługi klienta poprzez proaktywną komunikację. Zauważyli, że niektóre transakcje znacząco odbiegają od średniej wartości zakupu, co może budzić zaniepokojenie klientów odnośnie dokonywanych wydatków. Aby temu zaradzić, planują wysłać spersonalizowane e-maile do klientów, którzy dokonali transakcji przekraczających 150% średniej wartości płatności. Celem jest oferowanie bezpośredniego wsparcia i adresowanie wszelkich obaw związanych z takimi zakupami. Lista ta musi być precyzyjna, zawierać pełne dane klienta i kwotę transakcji, oraz być uporządkowana od największych transakcji, aby usprawnić proces komunikacji.

### Zapytanie SQL:

```sql
SELECT customer.first_name, customer.last_name, customer.email, payment.amount
FROM customer
LEFT JOIN payment ON customer.customer_id = payment.customer_id
WHERE payment.amount > 1.5 * (SELECT AVG(amount) FROM payment)
ORDER BY payment.amount DESC;
```

### Opis Działania:

Rozumiem, co masz na myśli. Oto szczegółowy opis działania twojego zapytania SQL, skonstruowany w oparciu o podany przykład:

- **SELECT first_name, last_name, customer.email, payment.amount**: Wybierane są imię i nazwisko klienta oraz jego adres email z tabeli `customer`, a także kwota każdej płatności z tabeli `payment`. Te informacje są niezbędne, aby zidentyfikować klientów dokonujących wyjątkowo wysokich zakupów i umożliwiają bezpośredni kontakt z nimi poprzez email. Selekcja kwoty płatności pozwala na ocenę wielkości transakcji dokonanych przez klientów.

- **FROM customer**: Klauzula `FROM` wskazuje na tabelę `customer` jako źródło danych, która zawiera szczegółowe informacje o klientach. Jest to punkt wyjścia do łączenia danych klientów z informacjami o ich płatnościach.

- **LEFT JOIN payment ON customer.customer_id = payment.customer_id**: Operacja `LEFT JOIN` połączenia tabeli `customer` z tabelą `payment` za pomocą wspólnego identyfikatora `customer_id` umożliwia złączenie danych o klientach z informacjami o dokonanych przez nich płatnościach. Dzięki temu można uwzględnić wszystkich klientów, nawet tych bez zarejestrowanych płatności, ale w kontekście tego zapytania skupiamy się na tych, którzy przekroczyli określony próg wydatków.

- **WHERE payment.amount > 1.5 * (SELECT AVG(amount) FROM payment)**: Klauzula `WHERE` filtruje płatności, pozostawiając tylko te, które są większe niż 150% średniej kwoty wszystkich płatności. Obliczenie średniej wartości płatności za pomocą podzapytania umożliwia dynamiczne dostosowanie progu do bieżących trendów zakupowych. To kryterium selekcji wskazuje na zamiar skoncentrowania się na najbardziej wartościowych transakcjach.

- **ORDER BY payment.amount DESC**: Kluczowym elementem zapytania jest klauzula `ORDER BY`, która sortuje wyniki w porządku malejącym według kwoty płatności (`payment.amount`). Decyzja o sortowaniu w ten sposób jest podjęta, aby na czele listy znaleźli się klienci, którzy dokonali największych zakupów. Takie uporządkowanie ułatwia identyfikację transakcji o najwyższej wartości, co jest szczególnie przydatne w strategiach marketingowych skierowanych na promowanie lojalności i zwiększanie wartości życiowej klienta.
