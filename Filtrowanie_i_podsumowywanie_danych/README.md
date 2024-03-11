

## Wyjaśnienie komend użytych w przykładowych symulacjach problemów biznesowych

### Problem biznesowy: 
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

