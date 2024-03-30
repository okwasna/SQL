### Problem Biznesowy 1:

Firma chce analizować swoje przychody w podziale na kwartały każdego roku, aby zidentyfikować trendy wzrostu, sezonowość, oraz okresy o największej i najmniejszej aktywności klientów. Analiza ta ma na celu lepsze planowanie działań marketingowych, budżetowania oraz dostosowywanie poziomu zapasów i personelu do przewidywanego popytu.

### Zapytanie SQL:

```sql
SELECT 
  EXTRACT(YEAR FROM payment_date) AS payment_year,
  EXTRACT(QUARTER FROM payment_date) AS payment_quarter,
  SUM(amount) AS total_amount
FROM 
  payment
GROUP BY 
  payment_year, 
  payment_quarter
ORDER BY 
  payment_year, 
  payment_quarter;
```

### Opis Działania:

- `SELECT EXTRACT(YEAR FROM payment_date) AS payment_year, EXTRACT(QUARTER FROM payment_date) AS payment_quarter`: Z każdego rekordu w tabeli `payment` wybierany jest rok i kwartał z daty płatności, nadając im odpowiednio aliasy `payment_year` i `payment_quarter`. Pozwala to na agregację danych finansowych według okresów kwartalnych każdego roku.

- `SUM(amount) AS total_amount`: Dla każdej grupy, zdefiniowanej przez unikalną kombinację roku i kwartału, sumowana jest wartość płatności (`amount`), co daje całkowitą sumę przychodów firmy za dany kwartał. Ta suma jest prezentowana jako `total_amount`.

- `FROM payment`: Określa tabelę źródłową jako `payment`, z której pobierane są dane dotyczące płatności.

- `GROUP BY payment_year, payment_quarter`: Grupuje dane według roku i kwartału, umożliwiając agregację sumy płatności dla każdej unikalnej pary rok-kwartał.

- `ORDER BY payment_year, payment_quarter`: Sortuje wyniki według roku i kwartału, zapewniając chronologiczną kolejność danych, co ułatwia analizę trendów wzrostu, sezonowości oraz okresów o zmiennej aktywności klientów.

### Problem Biznesowy 2:

Firma chce dowiedzieć się, w który dzień tygodnia odnotowuje największą sprzedaż, aby lepiej zaplanować swoje działania promocyjne, zapasy oraz zasoby ludzkie.

### Zapytanie SQL:

```sql
SELECT 
  TO_CHAR(payment_date, 'Day') AS payment_date, 
  COUNT(*) AS transactions_count,
  SUM(amount) AS total_sales
FROM 
  payment
GROUP BY 
  TO_CHAR(payment_date, 'Day')
ORDER BY 
  total_sales DESC
LIMIT 1;
```

### Opis Działania:

- **Wybór i Formatowanie Danych**: `TO_CHAR(payment_date, 'Day') AS payment_date` konwertuje daty płatności na nazwy dni tygodnia i przypisuje wynik do kolumny `payment_date`.
- **Agregacja Danych**: `COUNT(*) AS transactions_count` liczy liczbę transakcji dla każdego dnia tygodnia, a `SUM(amount) AS total_sales` sumuje łączną kwotę sprzedaży.
- **Grupowanie**: `GROUP BY TO_CHAR(payment_date, 'Day')` grupuje wyniki według dni tygodnia, umożliwiając wykonanie operacji agregacji dla każdego dnia osobno.
- **Sortowanie i Ograniczenie Wyników**: `ORDER BY total_sales DESC` sortuje dni tygodnia według łącznej kwoty sprzedaży od największej do najmniejszej, a `LIMIT 1` ogranicza wyniki do dnia z najwyższą sprzedażą.
