**Notatka: Najważniejsze polecenia i koncepcje języka SQL**
*Przydatne na egzamin zawodowy INF.03*

---

## 1. Podstawowe pojęcia

1. **SQL (Structured Query Language)**

   * Język zapytań do relacyjnych baz danych (np. MySQL, PostgreSQL, SQL Server, Oracle).
   * Dzieli się na kategorie:

     * **DDL** (Data Definition Language) – tworzenie i modyfikacja struktury bazy: `CREATE`, `ALTER`, `DROP`.
     * **DML** (Data Manipulation Language) – operacje na danych: `SELECT`, `INSERT`, `UPDATE`, `DELETE`.
     * **DCL** (Data Control Language) – zarządzanie uprawnieniami: `GRANT`, `REVOKE`.
     * **TCL** (Transaction Control Language) – transakcje: `BEGIN TRANSACTION`, `COMMIT`, `ROLLBACK`.

2. **Schemat relacyjny**

   * Baza danych składa się z tabel (relacji).
   * Każda tabela ma kolumny (atrybuty) i wiersze (rekordy).
   * Rekordy w tabeli nie muszą być unikalnie identyfikowane – dlatego często definiuje się klucz główny (PRIMARY KEY).

---

## 2. Definicja i modyfikacja tabel (DDL)

1. **`CREATE TABLE`**

   * Tworzy nową tabelę z określonymi kolumnami i typami danych.

   ```sql
   CREATE TABLE Pracownicy (
     id INT PRIMARY KEY,             -- klucz główny
     imie VARCHAR(50) NOT NULL,
     nazwisko VARCHAR(50) NOT NULL,
     data_zatrudnienia DATE,
     pensja DECIMAL(10,2) DEFAULT 0.00
   );
   ```

   * W przykładzie:

     * `INT` – liczba całkowita,
     * `VARCHAR(50)` – ciąg znaków o maksymalnej długości 50,
     * `DATE` – data w formacie RRRR-MM-DD,
     * `DECIMAL(10,2)` – liczba z częścią dziesiętną (10 cyfr łącznie, 2 po przecinku).

2. **`ALTER TABLE`**

   * Dodaje/usuwa kolumnę lub modyfikuje strukturę istniejącej tabeli.

   ```sql
   -- Dodanie kolumny
   ALTER TABLE Pracownicy
     ADD COLUMN email VARCHAR(100);

   -- Zmiana typu istniejącej kolumny
   ALTER TABLE Pracownicy
     MODIFY COLUMN pensja DECIMAL(12,2);

   -- Usunięcie kolumny
   ALTER TABLE Pracownicy
     DROP COLUMN data_zatrudnienia;
   ```

3. **`DROP TABLE`**

   * Usuwa całą tabelę i wszystkie jej dane.

   ```sql
   DROP TABLE Pracownicy;
   ```

4. **`TRUNCATE TABLE`**

   * Usuwa wszystkie wiersze z tabeli, zachowując jej definicję (szybsze niż `DELETE`).

   ```sql
   TRUNCATE TABLE Pracownicy;
   ```

---

## 3. Wstawianie i modyfikacja danych (DML)

1. **`INSERT INTO`**

   * Wstawienie pojedynczego lub wielu wierszy.

   ```sql
   INSERT INTO Pracownicy (id, imie, nazwisko, data_zatrudnienia, pensja)
   VALUES (1, 'Anna', 'Kowalska', '2023-04-01', 4500.00);

   -- Wstawienie bez określania kolumn (kolejność musi być zgodna z definicją tabeli):
   INSERT INTO Pracownicy
   VALUES (2, 'Bartek', 'Nowak', '2022-11-15', 5200.50);
   ```

2. **`UPDATE`**

   * Modyfikacja istniejących wierszy.

   ```sql
   -- Zwiększenie pensji o 10% pracowników zatrudnionych przed rokiem 2023
   UPDATE Pracownicy
   SET pensja = pensja * 1.10
   WHERE data_zatrudnienia < '2023-01-01';
   ```

3. **`DELETE`**

   * Usunięcie wierszy spełniających warunek.

   ```sql
   -- Usunięcie pracownika o id = 2
   DELETE FROM Pracownicy
   WHERE id = 2;

   -- Usunięcie wszystkich wierszy (różnica: loguje każdy wiersz, wolniejsze niż TRUNCATE)
   DELETE FROM Pracownicy;
   ```

4. **`SELECT`** (podstawy)

   * Pobranie danych z jednej lub wielu tabel.

   ```sql
   -- Pobranie wszystkich kolumn i wszystkich wierszy
   SELECT * FROM Pracownicy;

   -- Pobranie konkretnych kolumn
   SELECT imie, nazwisko, pensja
   FROM Pracownicy;
   ```

---

## 4. Klauzule w zapytaniach SELECT

1. **`WHERE`**

   * Filtruje wiersze według warunku (logiczny, porównania).

   ```sql
   SELECT *
   FROM Pracownicy
   WHERE pensja > 5000.00 AND data_zatrudnienia >= '2022-01-01';
   ```

2. **Operatorzy porównania i logiczni**

   | Operator    | Znaczenie                     | Przykład                                |
   | ----------- | ----------------------------- | --------------------------------------- |
   | `=`         | równe                         | `pensja = 4500`                         |
   | `<>`, `!=`  | różne                         | `nazwisko <> 'Kowalska'`                |
   | `>` , `<`   | większe, mniejsze             | `id > 10`, `pen < 3000`                 |
   | `>=`, `<=`  | większe/równe, mniejsze/równe | `wiek >= 30`                            |
   | `AND`, `OR` | łączenie warunków             | `pensja > 5000 AND miasto = 'Warszawa'` |
   | `NOT`       | negacja                       | `NOT (pensja < 4000)`                   |

3. **`ORDER BY`**

   * Sortowanie wyników według jednej lub wielu kolumn.

   ```sql
   SELECT imie, nazwisko, pensja
   FROM Pracownicy
   WHERE pensja >= 4000
   ORDER BY pensja DESC, nazwisko ASC;
   ```

4. **`LIMIT` / `TOP`**

   * Ograniczenie liczby zwracanych wierszy.

   ```sql
   -- W MySQL / PostgreSQL / SQLite:
   SELECT * FROM Pracownicy
   ORDER BY pensja DESC
   LIMIT 5;              -- tylko 5 wierszy

   -- W SQL Server:
   SELECT TOP 5 * FROM Pracownicy
   ORDER BY pensja DESC;
   ```

5. **`DISTINCT`**

   * Usunięcie duplikatów w wynikach (tylko unikalne wiersze).

   ```sql
   SELECT DISTINCT miasto
   FROM Pracownicy;
   ```

---

## 5. Agregacja i grupowanie

1. **Funkcje agregujące**

   | Funkcja        | Opis                     |
   | -------------- | ------------------------ |
   | `COUNT(*)`     | Policzy liczbę wierszy   |
   | `SUM(kolumna)` | Suma wartości w kolumnie |
   | `AVG(kolumna)` | Średnia wartość          |
   | `MIN(kolumna)` | Minimalna wartość        |
   | `MAX(kolumna)` | Maksymalna wartość       |

   ```sql
   -- Przykład: ile jest pracowników
   SELECT COUNT(*) AS liczba_pracownikow
   FROM Pracownicy;

   -- Przykład: łączna i średnia pensja
   SELECT SUM(pensja) AS suma_pensji,
          AVG(pensja) AS srednia_pensji
   FROM Pracownicy;
   ```

2. **`GROUP BY`**

   * Grupuje wiersze według jednej lub wielu kolumn, pozwala na agregację w grupach.

   ```sql
   -- Średnia pensja w każdym mieście:
   SELECT miasto, AVG(pensja) AS srednia_pensja
   FROM Pracownicy
   GROUP BY miasto;
   ```

3. **`HAVING`**

   * Filtruje grupy (podobnie do `WHERE`, ale na poagregowanym wyniku).

   ```sql
   -- Miasta, w których średnia pensja > 5000
   SELECT miasto, AVG(pensja) AS srednia_pensja
   FROM Pracownicy
   GROUP BY miasto
   HAVING AVG(pensja) > 5000;
   ```

4. **Łączenie `WHERE`, `GROUP BY`, `HAVING`, `ORDER BY`**

   ```sql
   SELECT miasto, COUNT(*) AS liczba_pracownikow, MAX(pensja) AS najwyzsza_pensja
   FROM Pracownicy
   WHERE data_zatrudnienia >= '2022-01-01'
   GROUP BY miasto
   HAVING COUNT(*) >= 3
   ORDER BY liczba_pracownikow DESC;
   ```

---

## 6. Łączenie tabel (JOIN)

1. **Schemat przykładowych tabel**

   * `Pracownicy(id, imie, nazwisko, miasto_id, pensja)`
   * `Miasta(miasto_id, nazwa_miasta, wojewodztwo)`

2. **`INNER JOIN`**

   * Zwraca wiersze, które mają dopasowanie w obu tabelach.

   ```sql
   SELECT p.imie, p.nazwisko, m.nazwa_miasta
   FROM Pracownicy p
   INNER JOIN Miasta m
     ON p.miasto_id = m.miasto_id;
   ```

3. **`LEFT (OUTER) JOIN`**

   * Zwraca wszystkie wiersze z tabeli „lewej” (pierwszej), a dopasowane z tabeli „prawej” (drugiej). Jeśli nie ma dopasowania, zwraca `NULL` dla kolumn „prawej”.

   ```sql
   SELECT p.imie, p.nazwisko, m.nazwa_miasta
   FROM Pracownicy p
   LEFT JOIN Miasta m
     ON p.miasto_id = m.miasto_id;
   ```

4. **`RIGHT (OUTER) JOIN`**

   * Zwraca wszystkie wiersze z tabeli „prawej” (drugiej) i dopasowane z tabeli „lewej”.

   ```sql
   SELECT p.imie, p.nazwisko, m.nazwa_miasta
   FROM Pracownicy p
   RIGHT JOIN Miasta m
     ON p.miasto_id = m.miasto_id;
   ```

5. **`FULL (OUTER) JOIN`** (w niektórych systemach)

   * Zwraca wszystkie wiersze z obu tabel – jeśli nie ma dopasowania, pojawia się `NULL` po jednej ze stron.

   ```sql
   SELECT p.imie, p.nazwisko, m.nazwa_miasta
   FROM Pracownicy p
   FULL OUTER JOIN Miasta m
     ON p.miasto_id = m.miasto_id;
   ```

6. **`CROSS JOIN`**

   * Iloczyn kartezjański – każda kombinacja wierszy z obu tabel.

   ```sql
   SELECT p.imie, m.nazwa_miasta
   FROM Pracownicy p
   CROSS JOIN Miasta m;
   ```

---

## 7. Podzapytania (subqueries)

1. **Podzapytania w klauzuli `WHERE`**

   ```sql
   -- Pracownicy, których pensja jest wyższa od średniej pensji dla wszystkich
   SELECT imie, nazwisko, pensja
   FROM Pracownicy
   WHERE pensja > (SELECT AVG(pensja) FROM Pracownicy);
   ```

2. **Podzapytania w `FROM` (tworzenie aliasowanej tabeli tymczasowej)**

   ```sql
   SELECT sub.miasto, sub.srednia_pensja
   FROM (
     SELECT miasto_id, AVG(pensja) AS srednia_pensja
     FROM Pracownicy
     GROUP BY miasto_id
   ) AS sub
   INNER JOIN Miasta m
     ON sub.miasto_id = m.miasto_id;
   ```

3. **`EXISTS` / `NOT EXISTS`**

   ```sql
   -- Pracownicy, którzy pracują w mieście, gdzie jest co najmniej 5 pracowników
   SELECT imie, nazwisko
   FROM Pracownicy p
   WHERE EXISTS (
     SELECT 1
     FROM Pracownicy p2
     WHERE p2.miasto_id = p.miasto_id
     GROUP BY p2.miasto_id
     HAVING COUNT(*) >= 5
   );
   ```

4. **`IN` / `NOT IN`**

   ```sql
   -- Pracownicy z miast o ID w zbiorze (1, 3, 5)
   SELECT *
   FROM Pracownicy
   WHERE miasto_id IN (1, 3, 5);

   -- Pracownicy, których miasto_id nie występuje w tabeli Miasta o województwie = 'Mazowieckie'
   SELECT *
   FROM Pracownicy
   WHERE miasto_id NOT IN (
     SELECT miasto_id
     FROM Miasta
     WHERE wojewodztwo = 'Mazowieckie'
   );
   ```

---

## 8. Indeksy i optymalizacja

1. **`CREATE INDEX`**

   * Przyspiesza wyszukiwanie po kolumnie (lub kombinacji kolumn).

   ```sql
   -- Indeks na kolumnie nazwisko w tabeli Pracownicy
   CREATE INDEX idx_pracownicy_nazwisko
   ON Pracownicy(nazwisko);

   -- Indeks wielokolumnowy: najpierw miasto_id, potem pensja
   CREATE INDEX idx_pracownicy_miasto_pensja
   ON Pracownicy(miasto_id, pensja);
   ```

2. **`DROP INDEX`**

   * Usuwa indeks. Składnia zależy od systemu bazy (MySQL, PostgreSQL, SQL Server).

   ```sql
   -- MySQL (indeks w danej tabeli):
   DROP INDEX idx_pracownicy_nazwisko ON Pracownicy;

   -- PostgreSQL:
   DROP INDEX idx_pracownicy_nazwisko;
   ```

3. **Gdy indeks jest przydatny**

   * Gdy często filtrujemy lub sortujemy po danej kolumnie (`WHERE nazwisko = 'Nowak'`, `ORDER BY data_zatrudnienia`).
   * Należy uważać: zbyt wiele indeksów spowalnia operacje `INSERT`/`UPDATE`/`DELETE`, bo każdy indeks trzeba aktualizować.

---

## 9. Transakcje (TCL)

1. **`BEGIN TRANSACTION` / `START TRANSACTION`**

   * Rozpoczyna transakcję (zbiór operacji, które muszą być wykonane razem).

   ```sql
   START TRANSACTION;
   ```

2. **`COMMIT`**

   * Zatwierdza wszystkie zmiany wykonane od `BEGIN`.

   ```sql
   COMMIT;
   ```

3. **`ROLLBACK`**

   * Cofa zmiany dokonane w transakcji (jeśli nastąpił błąd lub chcemy anulować operacje).

   ```sql
   ROLLBACK;
   ```

4. **Przykład transakcji**
   ● Wyobraźmy sobie przelew między kontami w tabeli `Konta(konto_id, saldo)`:

   ```sql
   START TRANSACTION;

   UPDATE Konta
   SET saldo = saldo - 100
   WHERE konto_id = 1;

   UPDATE Konta
   SET saldo = saldo + 100
   WHERE konto_id = 2;

   -- Jeśli wszystko ok:
   COMMIT;

   -- W razie błędu:
   -- ROLLBACK;
   ```

5. **Poziomy izolacji transakcji**

   * `READ UNCOMMITTED`, `READ COMMITTED`, `REPEATABLE READ`, `SERIALIZABLE`
   * Wyższy poziom izolacji daje większą spójność, ale może zmniejszać wydajność (blokady).

---

## 10. Uprawnienia i bezpieczeństwo (DCL)

1. **`GRANT`**

   * Przyznaje uprawnienia (SELECT, INSERT, UPDATE, DELETE, …) użytkownikowi lub roli.

   ```sql
   -- W MySQL:
   GRANT SELECT, INSERT, UPDATE
   ON moja_baza.Pracownicy
   TO 'uzytkownik'@'localhost';

   -- W PostgreSQL:
   GRANT SELECT, INSERT
   ON TABLE Pracownicy
   TO nazwa_usera;
   ```

2. **`REVOKE`**

   * Odbiera wcześniej nadane uprawnienia.

   ```sql
   REVOKE UPDATE
   ON Pracownicy
   FROM nazwa_usera;
   ```

3. **Typowe uprawnienia**

   | Uprawnienie      | Opis                                                   |
   | ---------------- | ------------------------------------------------------ |
   | `SELECT`         | Odczyt danych                                          |
   | `INSERT`         | Wstawianie nowych wierszy                              |
   | `UPDATE`         | Modyfikacja istniejących wierszy                       |
   | `DELETE`         | Usuwanie wierszy                                       |
   | `EXECUTE`        | Uruchamianie procedur składowanych (stored procedures) |
   | `ALL PRIVILEGES` | Wszystkie dostępne uprawnienia                         |

---

## 11. Złożone koncepcje i przydatne funkcje

1. **Widoki (VIEW)**

   * Wirtualna tabela oparta na wyniku zapytania `SELECT`.

   ```sql
   CREATE VIEW Widok_Pracownicy AS
   SELECT id, imie, nazwisko, pensja
   FROM Pracownicy
   WHERE pensja > 4000;

   -- Korzystanie:
   SELECT * FROM Widok_Pracownicy;
   ```

2. **Kursor (cursor)** (głównie w procedurach składowanych)

   * Pozwala na iterację po zbiorze wyników i przetwarzanie wiersz po wierszu (np. w PL/SQL, T‑SQL).

   ```sql
   -- Przykład w PostgreSQL:
   DO $$
   DECLARE
     rec RECORD;
   BEGIN
     FOR rec IN SELECT id, imie FROM Pracownicy LOOP
       RAISE NOTICE 'ID: %, Imię: %', rec.id, rec.imie;
     END LOOP;
   END $$;
   ```

3. **Grupowanie okienkowe (window functions)**

   * Umożliwia obliczenia agregujące z zachowaniem szczegółów wiersza.

   ```sql
   SELECT 
     id, imie, nazwisko, pensja,
     AVG(pensja) OVER (PARTITION BY miasto_id) AS srednia_w_miescie
   FROM Pracownicy;
   ```

4. **Procedury składowane i funkcje**

   * Kod SQL (lub PL/SQL / T‑SQL) zapisany w bazie, który można wywołać wielokrotnie.

   ```sql
   -- Przykład funkcji w PostgreSQL:
   CREATE FUNCTION Podatek(pen NUMERIC)
   RETURNS NUMERIC
   LANGUAGE plpgsql
   AS $$
   BEGIN
     RETURN pen * 0.19;  -- 19% podatek
   END; $$
   ;

   -- Wywołanie:
   SELECT Podatek(pensja) AS kwota_podatku FROM Pracownicy;
   ```

5. **Funkcje tekstowe i daty**

   | Funkcja                                | Opis                                     |
   | -------------------------------------- | ---------------------------------------- |
   | `CONCAT(s1, s2, …)`                    | Łączenie ciągów                          |
   | `SUBSTRING(s, start, len)`             | Wycinanie fragmentu tekstu               |
   | `UPPER(s)`, `LOWER(s)`                 | Zamiana na wielkie/małe litery           |
   | `LENGTH(s)`                            | Długość ciągu                            |
   | `NOW()` / `CURRENT_TIMESTAMP`          | Bieżąca data i godzina                   |
   | `DATE_ADD(d, INTERVAL x unit)` (MySQL) | Dodawanie do daty (np. `INTERVAL 7 DAY`) |
   | `DATEDIFF(d1, d2)` (MySQL)             | Różnica w dniach między dwiema datami    |

   ```sql
   -- Przykład: wypisanie imienia i nazwiska w jednym polu
   SELECT CONCAT(imie, ' ', nazwisko) AS pelne_imie
   FROM Pracownicy;

   -- Przykład: pracownicy zatrudnieni w ciągu ostatnich 30 dni
   SELECT *
   FROM Pracownicy
   WHERE data_zatrudnienia >= DATE_SUB(CURDATE(), INTERVAL 30 DAY);
   ```

6. **Funkcje numeryczne**

   | Funkcja       | Opis                                      |
   | ------------- | ----------------------------------------- |
   | `ROUND(x, d)` | Zaokrąglenie do d miejsc po przecinku     |
   | `CEIL(x)`     | Sufit (najmniejsza liczba całkowita ≥ x)  |
   | `FLOOR(x)`    | Podłoga (największa liczba całkowita ≤ x) |
   | `ABS(x)`      | Wartość bezwzględna                       |

---

## 12. Przykładowe zapytania „gotowe do użycia”

W dalszej części kilka praktycznych przykładów zestawiających różne elementy SQL.

1. **Lista pracowników z imieniem, nazwiskiem i nazwą miasta**

   ```sql
   SELECT p.imie, p.nazwisko, m.nazwa_miasta
   FROM Pracownicy p
   LEFT JOIN Miasta m
     ON p.miasto_id = m.miasto_id
   WHERE p.pensja > 4000
   ORDER BY p.nazwisko ASC;
   ```

2. **Ile pracowników w każdym województwie**

   ```sql
   SELECT m.wojewodztwo, COUNT(*) AS liczba_pracownikow
   FROM Pracownicy p
   JOIN Miasta m
     ON p.miasto_id = m.miasto_id
   GROUP BY m.wojewodztwo
   ORDER BY liczba_pracownikow DESC;
   ```

3. **Dodanie nowego miasta i przypisanie pracownika**

   ```sql
   -- Dodanie miasta
   INSERT INTO Miasta (miasto_id, nazwa_miasta, wojewodztwo)
   VALUES (10, 'Gdańsk', 'Pomorskie');

   -- Przypisanie pracownika o id=5 do nowego miasta
   UPDATE Pracownicy
   SET miasto_id = 10
   WHERE id = 5;
   ```

4. **Usuwanie „starych” danych w transakcji**

   ```sql
   START TRANSACTION;

   DELETE FROM Pracownicy
   WHERE data_zatrudnienia < '2010-01-01';

   DELETE FROM Miasta
   WHERE miasto_id NOT IN (SELECT DISTINCT miasto_id FROM Pracownicy);

   COMMIT;
   ```

5. **Utworzenie widoku z sumą pensji w miastach**

   ```sql
   CREATE VIEW Widok_Pensje_Miasta AS
   SELECT m.nazwa_miasta, SUM(p.pensja) AS suma_pensji
   FROM Pracownicy p
   JOIN Miasta m
     ON p.miasto_id = m.miasto_id
   GROUP BY m.nazwa_miasta;
   ```

   * Teraz wystarczy:

     ```sql
     SELECT * FROM Widok_Pensje_Miasta
     WHERE suma_pensji > 200000;
     ```

---

## 13. Podsumowanie kluczowych poleceń i koncepcji

| Kategoria                     | Polecenie / Funkcja                              | Zastosowanie                                          |
| ----------------------------- | ------------------------------------------------ | ----------------------------------------------------- |
| **Definicja struktury (DDL)** | `CREATE TABLE`                                   | Tworzenie nowej tabeli z kolumnami i typami danych    |
|                               | `ALTER TABLE`                                    | Dodawanie/usuwanie/zmiana kolumn i kluczy             |
|                               | `DROP TABLE`                                     | Usuwanie całej tabeli                                 |
|                               | `TRUNCATE TABLE`                                 | Szybkie wyczyszczenie tabeli (zachowanie struktury)   |
| **Manipulacja danymi (DML)**  | `INSERT INTO`                                    | Wstawianie nowych wierszy                             |
|                               | `UPDATE`                                         | Modyfikacja istniejących wierszy                      |
|                               | `DELETE`                                         | Usuwanie wierszy                                      |
| **Zapytania (SELECT)**        | `SELECT ... FROM ... WHERE ...`                  | Pobranie danych z tabeli z opcjonalnym filtrowaniem   |
|                               | `ORDER BY`                                       | Sortowanie wyników                                    |
|                               | `LIMIT` / `TOP`                                  | Ograniczenie liczby zwracanych wierszy                |
|                               | `DISTINCT`                                       | Usunięcie duplikatów                                  |
| **Agregacja**                 | `COUNT()`, `SUM()`, `AVG()`, `MIN()`, `MAX()`    | Funkcje agregujące                                    |
|                               | `GROUP BY`                                       | Grupowanie wyników przed agregacją                    |
|                               | `HAVING`                                         | Filtrowanie grup (po agregacji)                       |
| **Łączenie tabel (JOIN)**     | `INNER JOIN`                                     | Zwraca wiersze występujące w obu tabelach             |
|                               | `LEFT JOIN` / `RIGHT JOIN` / `FULL JOIN`         | Łączenie „lewe”, „prawe” lub „pełne”                  |
|                               | `CROSS JOIN`                                     | Iloczyn kartezjański (wszystkie kombinacje)           |
| **Podzapytania**              | `SELECT ... WHERE ... IN (SELECT ...)`           | Podzapytania w klauzuli `WHERE` lub w `FROM`          |
|                               | `EXISTS` / `NOT EXISTS`                          | Sprawdzenie istnienia wierszy w podzapytaniu          |
| **Indeksy**                   | `CREATE INDEX`, `DROP INDEX`                     | Indeksowanie kolumn w celu przyspieszenia zapytań     |
| **Transakcje (TCL)**          | `START TRANSACTION` / `BEGIN`                    | Rozpoczęcie transakcji                                |
|                               | `COMMIT`                                         | Zatwierdzenie wszystkich zmian                        |
|                               | `ROLLBACK`                                       | Cofnięcie wszystkich zmian                            |
| **Uprawnienia (DCL)**         | `GRANT`, `REVOKE`                                | Zarządzanie uprawnieniami użytkowników                |
| **Widoki (VIEW)**             | `CREATE VIEW`, `DROP VIEW`                       | Wirtualne tabele oparte na wynikach zapytań           |
| **Funkcje okienkowe**         | `OVER (PARTITION BY ...)`                        | Agregacja w oknach zachowująca szczegóły wiersza      |
| **Funkcje tekstowe i datowe** | `CONCAT()`, `SUBSTRING()`, `NOW()`, `DATE_ADD()` | Operacje na ciągach i datach                          |
| **Procedury składowane**      | `CREATE FUNCTION`, `CREATE PROCEDURE`            | Logika przechowywana w bazie (np. obliczanie podatku) |

---

### Uwagi końcowe

1. **Zgodność dialektów SQL**

   * Różne systemy baz danych (MySQL, PostgreSQL, SQL Server, Oracle) mają drobne różnice składniowe (np. `LIMIT` vs. `TOP`, `IFNULL()` vs. `COALESCE()`, różne typy danych).
   * Na egzaminie warto dopytać, którego dialektu używacie lub stosować składnię najbardziej uniwersalną.

2. **Bezpieczeństwo**

   * Unikać budowania dynamicznych zapytań przez konkatenację stringów (ryzyko SQL Injection).
   * Zamiast tego stosować zapytania przygotowane (prepared statements) i wiązanie parametrów w aplikacji.

3. **Optymalizacja**

   * Przemyślane indeksy potrafią znacząco przyspieszyć zapytania.
   * Uważać, by nie tworzyć zbyt wielu indeksów – nadmiar spowalnia operacje wstawiania i aktualizacji.
   * Czytać plany wykonania zapytania (`EXPLAIN` w MySQL/PostgreSQL) w celu identyfikacji wąskich gardeł.

4. **Bieżąca praktyka**

   * Tworzenie własnych baz testowych i ćwiczenie zapytań na rzeczywistych lub przykładowych danych (np. tabele „Pracownicy”, „Miasta”, „Zamówienia”, „Produkty”).
   * Poznanie podstawowe komend, jak również bardziej zaawansowanych: transakcje, widoki, funkcje okienkowe (window functions).

Opanowanie powyższych poleceń, klauzul i koncepcji pozwoli na swobodne tworzenie, modyfikowanie i odpytywanie relacyjnych baz danych, co jest niezbędne na egzaminie INF.03!
