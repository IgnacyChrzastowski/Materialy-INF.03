**Notatka: Podstawy i najważniejsze elementy PHP**
*Przydatne na egzamin zawodowy INF.03*

---

## 1. Podstawowa składnia

1. **Znacznik otwierający i zamykający**

   * PHP wstawiamy między `<?php … ?>`.

   ```php
   <?php
     echo "Witaj w PHP!";
   ?>
   ```

2. **Polecenia i średnik**

   * Każde wyrażenie kończy się średnikiem `;`.
   * Można w jednym pliku mieszać PHP i HTML:

   ```php
   <!DOCTYPE html>
   <html>
     <body>
       <h1><?php echo "Nagłówek"; ?></h1>
       <p>To jest zwykły tekst HTML.</p>
     </body>
   </html>
   ```

3. **Komentarze**

   * Jednolinijkowy: `// komentarz` lub `# komentarz`
   * Wielolinijkowy: `/* … */`

   ```php
   <?php
     // To jest komentarz
     # To też jest komentarz
     /* 
       Komentarz
       wielolinijkowy
     */
   ?>
   ```

---

## 2. Zmienne i typy danych

1. **Deklaracja zmiennej**

   * Zmienne zaczynamy od znaku dolara `$`, np. `$nazwa`.
   * Nie wymagamy wcześniejszej deklaracji typu – PHP jest wstępnie typowany dynamicznie.

   ```php
   <?php
     $liczba = 10;          // integer
     $nazwa = "Anna";       // string
     $czyAktywny = true;    // boolean
     $cena = 12.50;         // float
     $pusta = null;         // null
   ?>
   ```

2. **Type juggling (automatyczna konwersja)**

   * PHP automatycznie konwertuje typy w zależności od kontekstu.

   ```php
   <?php
     $a = "5";
     $b = 3;
     $suma = $a + $b;  // 8 (string "5" zamienia na int 5)
     echo gettype($suma); // "integer"
   ?>
   ```

3. **Stałe (`define` i `const`)**

   * Stałych używamy do wartości niezmiennych.

   ```php
   <?php
     define("NAZWA_STALEJ", "Wartość");
     const DRUGA_STALA = 3.14;
     echo NAZWA_STALEJ;
     echo DRUGA_STALA;
   ?>
   ```

---

## 3. Operatory

1. **Arytmetyczne**

   | Operator | Znaczenie       | Przykład | Wynik |
   | -------- | --------------- | -------- | ----- |
   | `+`      | dodawanie       | `2 + 3`  | 5     |
   | `-`      | odejmowanie     | `5 - 2`  | 3     |
   | `*`      | mnożenie        | `4 * 3`  | 12    |
   | `/`      | dzielenie       | `10 / 2` | 5     |
   | `%`      | modulo (reszta) | `7 % 3`  | 1     |
   | `**`     | potęgowanie     | `2 ** 3` | 8     |

2. **Przypisania**

   | Operator | Znaczenie          | Przykład               |
   | -------- | ------------------ | ---------------------- |
   | `=`      | przypisanie        | `$x = 5;`              |
   | `+=`     | dodaj i przypisz   | `$x += 3;` (x = x + 3) |
   | `-=`     | odejmij i przypisz | `$x -= 2;`             |
   | `*=`     | pomnóż i przypisz  | `$x *= 4;`             |
   | `/=`     | podziel i przypisz | `$x /= 2;`             |
   | `%=`     | modulo i przypisz  | `$x %= 3;`             |

3. **Porównania**

   | Operator             | Znaczenie                            | Przykład          | Wynik (typ boolean) |
   | -------------------- | ------------------------------------ | ----------------- | ------------------- |
   | `==`                 | równe (porównanie po konwersji)      | `"5" == 5`        | true                |
   | `===`                | identyczne (typ i wartość)           | `"5" === 5`       | false               |
   | `!=`                 | różne (po konwersji)                 | `3 != "3.0"`      | false               |
   | `!==`                | nieidentyczne (typ lub wartość inna) | `3 !== "3"`       | true                |
   | `<`, `>`, `<=`, `>=` | mniejsze, większe, itd.              | `4 < 7`, `5 >= 5` | boolean             |

4. **Logiczne**

   | Operator | Znaczenie                       | Przykład        |          |            |   |         |
   | -------- | ------------------------------- | --------------- | -------- | ---------- | - | ------- |
   | `&&`     | AND (i)                         | `true && false` |          |            |   |         |
   | \`       |                                 | \`              | OR (lub) | \`true     |   | false\` |
   | `!`      | NOT (negacja)                   | `!true`         |          |            |   |         |
   | `and`    | AND (niższy priorytet niż `&&`) | `$a and $b`     |          |            |   |         |
   | `or`     | OR (niższy priorytet niż \`     |                 | \`)      | `$a or $b` |   |         |

5. **Łańcuchy (string)**

   | Operator | Znaczenie               | Przykład             | Wynik           |
   | -------- | ----------------------- | -------------------- | --------------- |
   | `.`      | konkatenacja (łączenie) | `"Ala " . "ma kota"` | `"Ala ma kota"` |
   | `.= `    | dołącz i przypisz       | `$s .= " coś";`      |                 |

---

## 4. Struktury sterujące

1. **Instrukcja warunkowa `if…elseif…else`**

   ```php
   <?php
     $x = 7;
     if ($x > 10) {
       echo "Większe niż 10";
     } elseif ($x == 10) {
       echo "Równe 10";
     } else {
       echo "Mniejsze niż 10";
     }
   ?>
   ```

2. **`switch…case…default`**

   ```php
   <?php
     $kolor = "czerwony";
     switch ($kolor) {
       case "czerwony":
         echo "Wybrałeś czerwony";
         break;
       case "zielony":
         echo "Wybrałeś zielony";
         break;
       default:
         echo "Nieznany kolor";
     }
   ?>
   ```

3. **Pętla `while`**

   ```php
   <?php
     $i = 1;
     while ($i <= 5) {
       echo $i . " ";
       $i++;
     }
     // Wynik: 1 2 3 4 5
   ?>
   ```

4. **Pętla `do…while`**

   ```php
   <?php
     $i = 1;
     do {
       echo $i . " ";
       $i++;
     } while ($i <= 5);
   ?>
   ```

5. **Pętla `for`**

   ```php
   <?php
     for ($i = 0; $i < 5; $i++) {
       echo $i . " ";
     }
     // Wynik: 0 1 2 3 4
   ?>
   ```

6. **Pętla `foreach` (dla tablic)**

   ```php
   <?php
     $fruits = ["jabłko", "banan", "gruszka"];
     foreach ($fruits as $owoc) {
       echo $owoc . "<br>";
     }

     // Z kluczem => wartość:
     $ages = ["Ania" => 25, "Bartek" => 30];
     foreach ($ages as $imie => $wiek) {
       echo "$imie ma $wiek lat.<br>";
     }
   ?>
   ```

7. **Sterowanie pętlą: `break` i `continue`**

   ```php
   <?php
     for ($i = 1; $i <= 10; $i++) {
       if ($i == 5) {
         break;        // przerywa całą pętlę
       }
       echo $i . " ";
     }
     // Wynik: 1 2 3 4

     for ($i = 1; $i <= 10; $i++) {
       if ($i % 2 == 0) {
         continue;     // pomija resztę pętli dla parzystych
       }
       echo $i . " ";
     }
     // Wynik: 1 3 5 7 9
   ?>
   ```

---

## 5. Tablice (arrays)

1. **Tablica indeksowana (lista)**

   ```php
   <?php
     $colors = array("czerwony", "zielony", "niebieski");
     // od PHP 5.4 można też:
     $shapes = ["koło", "kwadrat", "trójkąt"];
     echo $colors[1]; // "zielony"
   ?>
   ```

2. **Tablica asocjacyjna**

   ```php
   <?php
     $person = [
       "imie" => "Adam",
       "wiek" => 28,
       "miasto" => "Warszawa"
     ];
     echo $person["miasto"]; // "Warszawa"
   ?>
   ```

3. **Dodawanie i usuwanie elementów**

   ```php
   <?php
     $lista[] = "element1";         // dodaje na koniec tablicy indeksowanej
     $osoby["Nowak"] = "Ania";      // w tablicy asocjacyjnej
     unset($lista[0]);              // usuwa pierwszy element (indeks 0)
     unset($osoby["Nowak"]);        // usuwa parę o kluczu "Nowak"
   ?>
   ```

4. **Przydatne funkcje pracy z tablicami**

   ```php
   <?php
     $t = [1, 5, 3, 9, 2];
     sort($t);             // sortuje rosnąco wartości i resetuje klucze
     rsort($t);            // malejąco

     $assoc = ["b" => 2, "a" => 1];
     ksort($assoc);        // sortuje wg kluczy rosnąco
     krsort($assoc);       // sortuje wg kluczy malejąco

     $count = count($t);   // liczba elementów

     $pos = array_search(3, $t); // zwraca indeks/zwraca false, jeśli nie ma

     $slice = array_slice($t, 1, 2); // fragment tablicy (od indeksu 1, 2 elementy)

     $merged = array_merge($t, [10, 20]); // łączy dwie tablice

     $keys = array_keys($person);   // pobiera listę kluczy tablicy asocjacyjnej
     $vals = array_values($person); // pobiera listę wartości

     // Iteracja:
     foreach ($t as $val) {
       echo $val . "<br>";
     }
   ?>
   ```

---

## 6. Funkcje

1. **Definiowanie i wywoływanie funkcji**

   ```php
   <?php
     function powitanie($imie) {
       return "Cześć, $imie!";
     }

     echo powitanie("Piotr"); // „Cześć, Piotr!”
   ?>
   ```

2. **Argumenty domyślne**

   ```php
   <?php
     function dodaj($a, $b = 1) {
       return $a + $b;
     }

     echo dodaj(5);    // 6 (b przyjmuje wartość domyślną 1)
     echo dodaj(5, 3); // 8
   ?>
   ```

3. **Typowanie (od PHP 7+)**

   * Można zadeklarować typy parametrów i typ zwracany:

   ```php
   <?php
     function pomnoz(int $x, int $y): int {
       return $x * $y;
     }
     echo pomnoz(2, 3); // 6
   ?>
   ```

   * Jeśli argument nie pasuje do typu, PHP może rzutować lub rzucić wyjątek w zależności od ustawień `declare(strict_types=1);`.

4. **Zmienna liczba argumentów (`...$args`)**

   ```php
   <?php
     function suma(...$liczby) {
       $s = 0;
       foreach ($liczby as $n) {
         $s += $n;
       }
       return $s;
     }
     echo suma(1, 2, 3, 4); // 10
   ?>
   ```

5. **Funkcje anonimowe (closures)**

   ```php
   <?php
     $fn = function($x) {
       return $x * 2;
     };
     echo $fn(5); // 10

     // Przekazywanie do innej funkcji:
     $lista = [1, 2, 3];
     $podwojone = array_map(function($v) { return $v * 2; }, $lista);
     // $podwojone = [2, 4, 6]
   ?>
   ```

---

## 7. Superglobalne tablice (dostęp do danych zewnętrznych)

1. **`$_GET`** – zmienne przesyłane metodą GET (parametry w URL)

   ```php
   // URL: example.com/?foo=bar&x=5
   <?php
     echo $_GET["foo"]; // "bar"
     echo $_GET["x"];   // "5"
   ?>
   ```

2. **`$_POST`** – zmienne przesyłane metodą POST (formularze HTML)

   ```html
   <!-- HTML -->
   <form method="post" action="process.php">
     <input type="text" name="email">
     <input type="submit" value="Wyślij">
   </form>
   ```

   ```php
   // process.php
   <?php
     $email = $_POST["email"];
     echo "Wpisałeś adres: $email";
   ?>
   ```

3. **`$_REQUEST`** – łączy `$_GET`, `$_POST` i `$_COOKIE` (kolejność określona w konfiguracji)

   ```php
   <?php
     $val = $_REQUEST["foo"]; // pobierze z dowolnej z wymienionych
   ?>
   ```

4. **`$_SERVER`** – informacje o serwerze i środowisku wykonawczym

   ```php
   <?php
     echo $_SERVER["REQUEST_METHOD"]; // np. "GET" lub "POST"
     echo $_SERVER["HTTP_USER_AGENT"]; // przeglądarka użytkownika
     echo $_SERVER["PHP_SELF"]; // ścieżka do aktualnego pliku
   ?>
   ```

5. **`$_SESSION`** – zmienne sesyjne użytkownika (wymaga `session_start()`)

   ```php
   <?php
     session_start();          // rozpoczęcie lub wznowienie sesji
     $_SESSION["user"] = "Jan"; 
     echo $_SESSION["user"];   // "Jan"
   ?>
   ```

6. **`$_COOKIE`** – ciasteczka (przechowywane w przeglądarce klienta)

   ```php
   <?php
     // ustawianie ciasteczka (trzeba przed wysłaniem jakiegokolwiek wyjścia):
     setcookie("lang", "pl", time() + 3600); // ważne godzinę

     // odczyt:
     if (isset($_COOKIE["lang"])) {
       echo "Język: " . $_COOKIE["lang"];
     }
   ?>
   ```

7. **`$_FILES`** – obsługa przesyłania plików przez formularz

   ```html
   <!-- HTML -->
   <form method="post" enctype="multipart/form-data" action="upload.php">
     <input type="file" name="plik">
     <input type="submit" value="Prześlij">
   </form>
   ```

   ```php
   // upload.php
   <?php
     if (isset($_FILES["plik"])) {
       $nazwaTemp = $_FILES["plik"]["tmp_name"];
       $nazwaOryg = $_FILES["plik"]["name"];
       move_uploaded_file($nazwaTemp, "uploads/" . $nazwaOryg);
       echo "Plik został przesłany.";
     }
   ?>
   ```

---

## 8. Przetwarzanie formularzy

1. **Prosty formularz z walidacją**

   ```html
   <!-- kontakt.php -->
   <form method="post" action="kontakt.php">
     Imię: <input type="text" name="imie"><br>
     Email: <input type="email" name="email"><br>
     <input type="submit" value="Wyślij">
   </form>

   <?php
     if ($_SERVER["REQUEST_METHOD"] == "POST") {
       $imie = trim($_POST["imie"]);
       $email = trim($_POST["email"]);

       if (empty($imie) || empty($email)) {
         echo "Wypełnij wszystkie pola.";
       } elseif (!filter_var($email, FILTER_VALIDATE_EMAIL)) {
         echo "Niepoprawny format adresu e-mail.";
       } else {
         echo "Dziękujemy, $imie. Twój e-mail: $email";
       }
     }
   ?>
   ```

2. **Funkcje pomocnicze do walidacji i filtrowania**

   ```php
   <?php
     // Usunięcie białych znaków z początku i końca:
     $val = trim($_POST["pole"]);

     // Usunięcie potencjalnego złośliwego kodu HTML:
     $val = htmlspecialchars($val, ENT_QUOTES, 'UTF-8');

     // Sprawdzanie e-mail:
     if (filter_var($email, FILTER_VALIDATE_EMAIL)) {
       // poprawny e-mail
     }

     // Sprawdzanie int:
     if (filter_var($x, FILTER_VALIDATE_INT)) {
       // poprawna liczba całkowita
     }

     // Sprawdzanie URL:
     if (filter_var($url, FILTER_VALIDATE_URL)) {
       // poprawny URL
     }
   ?>
   ```

---

## 9. Sesje i ciasteczka

1. **Rozpoczęcie i zakończenie sesji**

   ```php
   <?php
     session_start(); // wywołujemy na początku pliku przed wyjściem HTML

     // Ustawianie zmiennej sesyjnej:
     $_SESSION["user"] = "Kasia";

     // Zakończenie sesji (wylogowanie):
     session_unset();    // usuwa wszystkie zmienne sesji
     session_destroy();  // niszczy sesję
   ?>
   ```

2. **Ciasteczka (`setcookie`, `$_COOKIE`)**

   ```php
   <?php
     // Ustawienie ciasteczka ważnego przez 7 dni:
     setcookie("theme", "dark", time() + (7 * 24 * 60 * 60), "/");

     // Odczyt ciasteczka:
     if (isset($_COOKIE["theme"])) {
       $currentTheme = $_COOKIE["theme"];
     } else {
       $currentTheme = "light";
     }
   ?>
   ```

---

## 10. Include / Require (włączanie plików)

1. **`include` vs. `require`**

   * `include "plik.php";` – ostrzeżenie (`warning`), jeśli plik nie istnieje, skrypt dalej się wykonuje.
   * `require "plik.php";` – błąd krytyczny (`fatal error`), jeśli plik nie istnieje, skrypt przerywa działanie.

   ```php
   <?php
     include "naglowek.php";   // dołącza nagłówek (jeśli nie ma – ostrzeżenie)
     require "funkcje.php";    // dołącza dodatkowe funkcje (jeśli nie ma – przerwanie)

     // Wersje z _once:
     include_once "plik.php";  // dołącza tylko raz, nawet jeśli wywołamy ponownie
     require_once "plik.php";  // analogicznie
   ?>
   ```

2. **Przykład struktury projektu**

   ```
   /projekt
     index.php        // główny plik
     naglowek.php     // wspólny nagłówek HTML/PHP
     stopka.php       // wspólny footer
     sekret.php       // wrażliwe dane (np. konfiguracja bazy)
   ```

   ```php
   <!-- index.php -->
   <?php
     require_once "sekret.php";    // dane konfiguracyjne
     include "naglowek.php";       // wspólny nagłówek
   ?>
   <h2>Strona główna</h2>
   <p>Treść strony…</p>
   <?php include "stopka.php"; ?>
   ```

---

## 11. Praca z plikami

1. **Otwieranie i zamykanie pliku**

   ```php
   <?php
     $plik = fopen("dane.txt", "r"); // tryby: "r" – odczyt, "w" – zapis (nadpisuje), "a" – dopisywanie
     if ($plik) {
       // operacje na pliku
       fclose($plik); // zamknięcie pliku
     } else {
       echo "Nie można otworzyć pliku.";
     }
   ?>
   ```

2. **Odczytywanie zawartości**

   ```php
   <?php
     $plik = fopen("dane.txt", "r");
     while (!feof($plik)) {
       $linia = fgets($plik); // czyta pojedynczą linię
       echo $linia . "<br>";
     }
     fclose($plik);
   ?>
   ```

3. **Zapisywanie do pliku**

   ```php
   <?php
     $plik = fopen("dane.txt", "a"); // tryb "a" dopisuje na końcu
     $tekst = "Nowa linia tekstu\n";
     fwrite($plik, $tekst);          // zapis
     fclose($plik);
   ?>
   ```

4. **Wygodniejsze funkcje**

   ```php
   <?php
     // Wczytanie całego pliku do tablicy (po liniach):
     $lines = file("dane.txt"); 
     foreach ($lines as $l) {
       echo $l . "<br>";
     }

     // Wczytanie całego pliku do stringa:
     $all = file_get_contents("dane.txt");

     // Zapis stringa do pliku (nadpisuje):
     file_put_contents("dane.txt", "Całkowicie nowa zawartość");
   ?>
   ```

---

## 12. Obsługa wyjątków (od PHP 5+)

1. **Rzucanie i łapanie wyjątków**

   ```php
   <?php
     function dziel($a, $b) {
       if ($b == 0) {
         throw new Exception("Dzielenie przez zero!");
       }
       return $a / $b;
     }

     try {
       echo dziel(10, 0);
     } catch (Exception $e) {
       echo "Błąd: " . $e->getMessage();
     }
   ?>
   ```

2. **Własne klasy wyjątków**

   ```php
   <?php
     class MyException extends Exception {
       public function info() {
         return "Kod błędu: " . $this->getCode();
       }
     }

     try {
       throw new MyException("Coś poszło nie tak", 123);
     } catch (MyException $e) {
       echo $e->getMessage(); // komunikat
       echo $e->info();       // dodatkowa metoda
     }
   ?>
   ```

---

## 13. Podstawy programowania obiektowego (OOP)

1. **Definicja klasy i obiektu**

   ```php
   <?php
     class Osoba {
       public $imie;    // właściwość (atrybut) publiczna
       private $wiek;   // właściwość prywatna

       // Konstruktor
       public function __construct($imie, $wiek) {
         $this->imie = $imie;
         $this->wiek = $wiek;
       }

       // Metoda publiczna
       public function przedstawSie() {
         echo "Cześć, jestem " . $this->imie . " i mam " . $this->wiek . " lat.";
       }

       // Metoda prywatna
       private function sekret() {
         echo "To jest sekret!";
       }

       // Getter dla wieku
       public function getWiek() {
         return $this->wiek;
       }

       // Setter dla wieku (może weryfikować poprawność)
       public function setWiek($w) {
         if ($w > 0) {
           $this->wiek = $w;
         }
       }
     }

     // Utworzenie obiektu:
     $os = new Osoba("Marta", 22);
     $os->przedstawSie(); // wywołanie metody
     echo $os->getWiek();
   ?>
   ```

2. **Dziedziczenie**

   ```php
   <?php
     class Pracownik extends Osoba {
       public $stanowisko;

       public function __construct($imie, $wiek, $stanowisko) {
         parent::__construct($imie, $wiek); // wywołanie konstruktora klasy bazowej
         $this->stanowisko = $stanowisko;
       }

       // Nadpisanie metody:
       public function przedstawSie() {
         echo "Jestem " . $this->imie . ", mam " . $this->getWiek() . 
              " lat i pracuję jako " . $this->stanowisko . ".";
       }
     }

     $p = new Pracownik("Tomek", 30, "Programista");
     $p->przedstawSie();
   ?>
   ```

3. **Modyfikatory dostępu**

   * `public` – dostępne z zewnątrz i wewnątrz klasy.
   * `protected` – dostępne tylko w klasie i klasach dziedziczących.
   * `private` – dostępne tylko wewnątrz danej klasy.

4. **Interfejsy i abstrakcja**

   ```php
   <?php
     interface Pojazd {
       public function jedz();
     }

     abstract class Maszyna {
       abstract public function start();
       public function zatrzymaj() {
         echo "Maszyna zatrzymana.";
       }
     }

     class Samochod extends Maszyna implements Pojazd {
       public function start() {
         echo "Samochód odpala silnik.";
       }
       public function jedz() {
         echo "Samochód jedzie.";
       }
     }

     $s = new Samochod();
     $s->start();
     $s->jedz();
     $s->zatrzymaj();
   ?>
   ```

---

## 14. Praca z bazą danych (rozszerzenie PDO)

1. **Połączenie z bazą MySQL za pomocą PDO**

   ```php
   <?php
     $dsn = "mysql:host=localhost;dbname=testdb;charset=utf8";
     $u = "root";
     $p = "";

     try {
       $pdo = new PDO($dsn, $u, $p);
       // tryb raportowania błędów:
       $pdo->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
     } catch (PDOException $e) {
       echo "Błąd połączenia: " . $e->getMessage();
       exit;
     }
   ?>
   ```

2. **Zapytanie SELECT (przygotowane instrukcje)**

   ```php
   <?php
     $sql = "SELECT id, imie, wiek FROM users WHERE wiek > :wiekMin";
     $stmt = $pdo->prepare($sql);
     $wiekMin = 18;
     $stmt->bindParam(':wiekMin', $wiekMin, PDO::PARAM_INT);
     $stmt->execute();

     while ($row = $stmt->fetch(PDO::FETCH_ASSOC)) {
       echo $row['imie'] . " ma " . $row['wiek'] . " lat.<br>";
     }

     // Lub w jednej linii:
     // $rows = $pdo->query("SELECT * FROM users")->fetchAll(PDO::FETCH_ASSOC);
   ?>
   ```

3. **INSERT / UPDATE / DELETE**

   ```php
   <?php
     // INSERT
     $sql = "INSERT INTO users (imie, wiek) VALUES (:imie, :wiek)";
     $stmt = $pdo->prepare($sql);
     $stmt->execute([
       ':imie' => 'Ewa',
       ':wiek' => 25
     ]);
     echo "Dodano użytkownika.";

     // UPDATE
     $sql2 = "UPDATE users SET wiek = :wiek WHERE id = :id";
     $stmt2 = $pdo->prepare($sql2);
     $stmt2->execute([':wiek' => 26, ':id' => 3]);
     echo "Zaktualizowano wiek.";

     // DELETE
     $sql3 = "DELETE FROM users WHERE id = :id";
     $stmt3 = $pdo->prepare($sql3);
     $stmt3->execute([':id' => 4]);
     echo "Usunięto użytkownika.";
   ?>
   ```

4. **Transakcje**

   ```php
   <?php
     try {
       $pdo->beginTransaction();

       $pdo->exec("UPDATE konto SET saldo = saldo - 100 WHERE id = 1");
       $pdo->exec("UPDATE konto SET saldo = saldo + 100 WHERE id = 2");

       $pdo->commit();
       echo "Przelew wykonany.";
     } catch (PDOException $e) {
       $pdo->rollBack();
       echo "Transakcja nie udała się: " . $e->getMessage();
     }
   ?>
   ```

---

## 15. Funkcje przydatne w PHP

1. **Praca z ciągami znaków (string)**

   ```php
   <?php
     $s = "Przykładowy tekst";

     echo strlen($s);                  // długość: 16
     echo strpos($s, "tek");           // pozycja: 12 (licząc od 0)
     echo str_replace("tekst", "ciąg", $s); // "Przykładowy ciąg"
     echo strtolower($s);              // "przykładowy tekst"
     echo strtoupper($s);              // "PRZYKŁADOWY TEKST"
     echo substr($s, 4, 6);            // "kładow"
     echo trim("  coś  ");             // usuwa spacje z końców
   ?>
   ```

2. **Data i czas**

   ```php
   <?php
     echo date("Y-m-d");          // np. "2025-06-01"
     echo date("H:i:s");          // np. "14:30:05"
     // Timestamp (sekundy od 1970):
     $ts = time();
     echo date("d-m-Y H:i", $ts + 3600); // data + godzina w przyszłości
   ?>
   ```

3. **Losowe liczby**

   ```php
   <?php
     echo rand(1, 100);   // liczba pseudolosowa od 1 do 100
     echo mt_rand(1, 100); // szybsza funkcja Mersenne Twister
   ?>
   ```

4. **Serializacja**

   ```php
   <?php
     $tab = ["a" => 1, "b" => 2];
     $s = serialize($tab);      // przekształca do stringa
     $t2 = unserialize($s);     // z powrotem do tablicy
   ?>
   ```

5. **Generowanie i sprawdzanie unikalnego identyfikatora**

   ```php
   <?php
     $id = uniqid();     // „60b725f10c9c85c70d97880d”
     $id2 = uniqid("user_"); // prefiks
   ?>
   ```

---

## 16. Bezpieczeństwo

1. **Unikanie XSS**

   * Zawsze „uciekać” dane wyświetlane w HTML:

   ```php
   <?php
     $txt = "<script>alert('xss');</script>";
     echo htmlspecialchars($txt, ENT_QUOTES, 'UTF-8');
     // Wyświetli dosłownie: &lt;script&gt;alert(&#039;xss&#039;);&lt;/script&gt;
   ?>
   ```

2. **Unikanie SQL Injection**

   * Korzystać tylko z przygotowanych zapytań (prepared statements) i wiązania parametrów (`bindParam` lub przekazywanie tablicy do `execute`).

   ```php
   <?php
     // poprawne:
     $stmt = $pdo->prepare("SELECT * FROM users WHERE login = :login");
     $stmt->execute([':login' => $login]);
   ?>
   ```

3. **Haszowanie haseł**

   * Nigdy nie przechowywać haseł w czystym tekście.

   ```php
   <?php
     // Tworzenie hasha:
     $hash = password_hash($password, PASSWORD_DEFAULT);
     // Weryfikacja:
     if (password_verify($inputPassword, $hash)) {
       echo "Poprawne hasło.";
     } else {
       echo "Błędne hasło.";
     }
   ?>
   ```

4. **Walidacja i filtrowanie danych**

   * Używać funkcji `filter_input`, `filter_var` (omówione w sekcji formularzy).
   * Sprawdzać i oczyszczać dane wejściowe przed użyciem.

---

## 17. Przydatne wskazówki

1. **Raportowanie błędów**

   * W trakcie developmentu warto włączyć wyświetlanie błędów:

   ```php
   <?php
     ini_set('display_errors', 1);
     ini_set('display_startup_errors', 1);
     error_reporting(E_ALL);
   ?>
   ```

2. **Struktura projektu**

   * Rozdzielaj logikę (PHP) od szablonów (HTML/CSS).
   * Stosuj `include`/`require` do wspólnych części (nagłówek, stopka).
   * Trzymaj dane konfiguracyjne (np. połączenie z bazą) w osobnym, bezpiecznym pliku poza katalogiem publicznym.

3. **Użycie Composer**

   * Choć w prostych projektach nie zawsze konieczne, Composer pozwala zarządzać zewnętrznymi bibliotekami i autoloadingiem klas.

4. **Obsługa błędów w produkcji**

   * Wyłącz `display_errors` i loguj błędy do pliku (np. `error_log` w `php.ini` lub w kodzie PHP).

---

## 18. Przykładowy mini‑projekt: prosty system logowania

1. **Struktura plików**

   ```
   /login_system
     config.php       // dane połączenia z bazą, wspólne funkcje
     register.php     // formularz rejestracji
     login.php        // formularz logowania
     logout.php       // wylogowanie
     dashboard.php    // strona dla zalogowanych
     header.php       // wspólny nagłówek HTML
     footer.php       // wspólna stopka HTML
   ```

2. **config.php**

   ```php
   <?php
   // config.php
   session_start();

   // Połączenie z bazą (PDO):
   try {
     $dsn = "mysql:host=localhost;dbname=loga;charset=utf8";
     $pdo = new PDO($dsn, "root", "");
     $pdo->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
   } catch (PDOException $e) {
     die("Błąd bazy: " . $e->getMessage());
   }

   // Funkcja sprawdzająca, czy użytkownik jest zalogowany:
   function isLoggedIn() {
     return isset($_SESSION["user_id"]);
   }
   ?>
   ```

3. **register.php**

   ```php
   <?php
   include "config.php";

   if ($_SERVER["REQUEST_METHOD"] == "POST") {
     $login = trim($_POST["login"]);
     $haslo = trim($_POST["haslo"]);

     // Prosta walidacja:
     if (empty($login) || empty($haslo)) {
       $error = "Wypełnij oba pola!";
     } else {
       // Sprawdź czy login już istnieje:
       $stmt = $pdo->prepare("SELECT id FROM users WHERE login = :login");
       $stmt->execute([':login' => $login]);
       if ($stmt->fetch()) {
         $error = "Ten login jest zajęty.";
       } else {
         // Dodaj użytkownika:
         $hash = password_hash($haslo, PASSWORD_DEFAULT);
         $ins = $pdo->prepare("INSERT INTO users (login, hash) VALUES (:login, :hash)");
         $ins->execute([':login' => $login, ':hash' => $hash]);
         header("Location: login.php");
         exit;
       }
     }
   }
   ?>

   <?php include "header.php"; ?>
   <h2>Rejestracja</h2>
   <?php if (!empty($error)) echo "<p style='color:red;'>$error</p>"; ?>
   <form method="post" action="register.php">
     Login: <input type="text" name="login"><br>
     Hasło: <input type="password" name="haslo"><br>
     <input type="submit" value="Zarejestruj">
   </form>
   <?php include "footer.php"; ?>
   ```

4. **login.php**

   ```php
   <?php
   include "config.php";

   if ($_SERVER["REQUEST_METHOD"] == "POST") {
     $login = trim($_POST["login"]);
     $haslo = trim($_POST["haslo"]);

     if (empty($login) || empty($haslo)) {
       $error = "Wypełnij oba pola!";
     } else {
       $stmt = $pdo->prepare("SELECT id, hash FROM users WHERE login = :login");
       $stmt->execute([':login' => $login]);
       $row = $stmt->fetch(PDO::FETCH_ASSOC);

       if ($row && password_verify($haslo, $row["hash"])) {
         $_SESSION["user_id"] = $row["id"];
         $_SESSION["login"] = $login;
         header("Location: dashboard.php");
         exit;
       } else {
         $error = "Niepoprawny login lub hasło.";
       }
     }
   }
   ?>

   <?php include "header.php"; ?>
   <h2>Logowanie</h2>
   <?php if (!empty($error)) echo "<p style='color:red;'>$error</p>"; ?>
   <form method="post" action="login.php">
     Login: <input type="text" name="login"><br>
     Hasło: <input type="password" name="haslo"><br>
     <input type="submit" value="Zaloguj">
   </form>
   <?php include "footer.php"; ?>
   ```

5. **dashboard.php**

   ```php
   <?php
   include "config.php";

   if (!isLoggedIn()) {
     header("Location: login.php");
     exit;
   }
   ?>

   <?php include "header.php"; ?>
   <h2>Witaj, <?php echo htmlspecialchars($_SESSION["login"]); ?>!</h2>
   <p>To jest strona dostępna tylko dla zalogowanych użytkowników.</p>
   <p><a href="logout.php">Wyloguj się</a></p>
   <?php include "footer.php"; ?>
   ```

6. **logout.php**

   ```php
   <?php
   include "config.php";
   session_unset();
   session_destroy();
   header("Location: login.php");
   exit;
   ?>
   ```

7. **header.php / footer.php**

   ```php
   <!-- header.php -->
   <!DOCTYPE html>
   <html>
   <head>
     <meta charset="UTF-8">
     <title>Prosty System Logowania</title>
   </head>
   <body>
   <h1>Moja Aplikacja</h1>
   <hr>
   ```

   ```php
   <!-- footer.php -->
   <hr>
   <p>Stopka © 2025</p>
   </body>
   </html>
   ```

---

## 19. Podsumowanie najważniejszych elementów PHP

| Kategoria               | Element / Funkcja                                           | Zastosowanie / Uwagi                                         |                       |                    |
| ----------------------- | ----------------------------------------------------------- | ------------------------------------------------------------ | --------------------- | ------------------ |
| **Składnia**            | `<?php … ?>`                                                | Otwieranie i zamykanie kodu PHP w pliku.                     |                       |                    |
|                         | `;`                                                         | Kończy każde wyrażenie.                                      |                       |                    |
|                         | Komentarze (`//`, `#`, `/*…*/`)                             | Dokumentowanie kodu.                                         |                       |                    |
| **Zmienne i typy**      | `$zmienna`                                                  | Definicja zmiennych (brak deklaracji typu).                  |                       |                    |
|                         | `define("STALA", wartość)`                                  | Stała globalna.                                              |                       |                    |
|                         | `const NAZWA = wartość;`                                    | Stała w klasie lub pliku.                                    |                       |                    |
| **Operatory**           | Arytmetyczne (`+`, `-`, `*`, `/`, `%`, `**`)                | Podstawowe działania matematyczne.                           |                       |                    |
|                         | Przypisania (`=`, `+=`, `-=` itp.)                          | Modyfikacja wartości zmiennych.                              |                       |                    |
|                         | Porównania (`==`, `===`, `!=`, `!==`, `<`, `>`)             | Porównywanie wartości i typów.                               |                       |                    |
|                         | Logiczne (`&&`, \`                                          |                                                              | `, `!`, `and`, `or\`) | Operacje logiczne. |
|                         | Łańcuch (`.`)                                               | Łączenie stringów.                                           |                       |                    |
| **Struktury sterujące** | `if…elseif…else`, `switch…case…default`                     | Instrukcje warunkowe.                                        |                       |                    |
|                         | `while`, `do…while`, `for`, `foreach`                       | Pętle i iteracja po tablicach.                               |                       |                    |
|                         | `break`, `continue`                                         | Sterowanie przebiegiem pętli.                                |                       |                    |
| **Tablice (arrays)**    | Indeksowana: `array(...)` lub `[...]`                       | Kolekcja elementów pod kolejne indeksy.                      |                       |                    |
|                         | Asocjacyjna: `["klucz" => "wartość"]`                       | Para klucz ⇒ wartość.                                        |                       |                    |
|                         | `count()`, `sort()`, `array_merge()`, itp.                  | Podstawowe operacje na tablicach.                            |                       |                    |
| **Funkcje**             | `function nazwa($a, $b) { … }`                              | Definiowanie funkcji.                                        |                       |                    |
|                         | Argumenty domyślne, typowanie, `...$args`                   | Elastyczność w przekazywaniu parametrów.                     |                       |                    |
|                         | `return`                                                    | Zwracanie wartości.                                          |                       |                    |
|                         | Funkcje anonimowe (closures)                                | Przekazywanie funkcji jako zmiennych.                        |                       |                    |
| **Superglobalne**       | `$_GET`, `$_POST`, `$_REQUEST`                              | Dostęp do danych z formularzy i URL.                         |                       |                    |
|                         | `$_SERVER`                                                  | Informacje o serwerze i środowisku.                          |                       |                    |
|                         | `$_SESSION`, `$_COOKIE`                                     | Przechowywanie danych sesyjnych i ciasteczek.                |                       |                    |
|                         | `$_FILES`                                                   | Obsługa uploadu plików.                                      |                       |                    |
| **Formularze**          | `filter_input()`, `filter_var()`                            | Walidacja i filtrowanie danych wejściowych.                  |                       |                    |
|                         | `htmlspecialchars()`                                        | Ochrona przed XSS.                                           |                       |                    |
| **Sesje / Ciasteczka**  | `session_start()`, `$_SESSION`, `session_destroy()`         | Przechowywanie danych między żądaniami (np. dane logowania). |                       |                    |
|                         | `setcookie()`, `$_COOKIE`                                   | Przechowywanie danych po stronie klienta.                    |                       |                    |
| **Include/Require**     | `include`, `require`, `include_once`, `require_once`        | Dołączanie wspólnego kodu (nagłówki, funkcje).               |                       |                    |
| **Pliki**               | `fopen()`, `fgets()`, `fwrite()`, `fclose()`                | Odczyt i zapis do plików.                                    |                       |                    |
|                         | `file()`, `file_get_contents()`, `file_put_contents()`      | Szybsze metody odczytu/zapisu.                               |                       |                    |
| **Wyjątki**             | `try…catch`, `throw new Exception()`                        | Obsługa błędów i wyjątków.                                   |                       |                    |
| **OOP (podstawy)**      | `class`, `public/protected/private`, `__construct()`, `new` | Tworzenie klas i obiektów.                                   |                       |                    |
|                         | Dziedziczenie (`extends`), interfejsy (`implements`)        | Hierarchia klas, wielokrotne interfejsy.                     |                       |                    |
| **PDO (baza danych)**   | `new PDO()`, `prepare()`, `execute()`, `fetch()`            | Bezpieczne operacje CRUD z bazą.                             |                       |                    |
|                         | `beginTransaction()`, `commit()`, `rollBack()`              | Transakcje (atomiczne zmiany w bazie).                       |                       |                    |
| **Bezpieczeństwo**      | `htmlspecialchars()`, przygotowane zapytania                | Unikanie XSS i SQL Injection.                                |                       |                    |
|                         | `password_hash()`, `password_verify()`                      | Bezpieczne haszowanie haseł.                                 |                       |                    |

---

*Powyższa notatka stanowi zbiór najważniejszych zagadnień i przykładów w PHP. Dzięki niej opanujesz podstawy języka, pracę z formularzami, bazami danych, sesjami oraz elementy bezpieczeństwa – co z pewnością pomoże na egzaminie INF.03!*



Poniżej znajduje się kompletny, przykładowy skrypt PHP, który w jednym pliku:

1. Łączy się z bazą danych MySQL (używając rozszerzenia **mysqli**).
2. Wczytuje wszystkie rekordy z wybranej tabeli i wyświetla je w HTML-owej tabeli.
3. Zawiera formularz HTML do dodawania nowych rekordów do tej tabeli.
4. Obsługuje zapis przesłanych danych (metodą POST) do bazy.

---

## Założenia

* Baza danych: `moja_baza`
* Tabela: `users`
* Struktura tabeli `users` (przykładowo):

  ```sql
  CREATE TABLE `users` (
    `id` INT NOT NULL AUTO_INCREMENT,
    `name` VARCHAR(100) NOT NULL,
    `email` VARCHAR(100) NOT NULL,
    PRIMARY KEY (`id`)
  ) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;
  ```
* Skrypt zapisujemy jako np. `index.php` w katalogu obsługiwanym przez serwer (np. `htdocs` lub `www`).

Poniższy kod można skopiować do pliku `index.php` i dostosować dane dostępowe (host, użytkownik, hasło, nazwa bazy).

```php
<?php
// index.php

// -------------------------------------------
// 1. Dane dostępowe do bazy danych
// -------------------------------------------
$host     = 'localhost';      // adres serwera MySQL (zwykle 'localhost')
$db_user  = 'root';           // nazwa użytkownika bazy
$db_pass  = '';               // hasło do bazy
$db_name  = 'moja_baza';      // nazwa bazy danych

// -------------------------------------------
// 2. Utworzenie połączenia z bazą (mysqli)
// -------------------------------------------
$conn = new mysqli($host, $db_user, $db_pass, $db_name);

// Sprawdzenie, czy połączenie powiodło się
if ($conn->connect_error) {
    die("Błąd połączenia z bazą: " . $conn->connect_error);
}
$conn->set_charset("utf8mb4"); // ustawienie kodowania na UTF-8

// -------------------------------------------
// 3. Obsługa przesłanego formularza (metoda POST)
// -------------------------------------------
if ($_SERVER['REQUEST_METHOD'] === 'POST') {
    // Pobranie wartości z formularza (bezpieczniejsza metoda: filtracja/escape)
    $name  = trim($_POST['name']);
    $email = trim($_POST['email']);

    // Prosta walidacja: sprawdź, czy pola nie są puste
    if (!empty($name) && !empty($email)) {
        // Przygotowanie zapytania z parametrami (prepared statement)
        $stmt = $conn->prepare("INSERT INTO users (name, email) VALUES (?, ?)");
        $stmt->bind_param("ss", $name, $email);

        if ($stmt->execute()) {
            // Po poprawnym dodaniu rekordu przekierowujemy z powrotem (aby uniknąć ponownego wysłania formularza przy odświeżeniu)
            header("Location: " . $_SERVER['PHP_SELF']);
            exit;
        } else {
            $error_msg = "Błąd przy dodawaniu rekordu: " . $stmt->error;
        }

        $stmt->close();
    } else {
        $error_msg = "Proszę wypełnić oba pola.";
    }
}

// -------------------------------------------
// 4. Pobranie wszystkich rekordów z tabeli
// -------------------------------------------
$sql    = "SELECT id, name, email FROM users ORDER BY id DESC";
$result = $conn->query($sql);

?>
<!DOCTYPE html>
<html lang="pl">
<head>
    <meta charset="UTF-8">
    <title>Lista użytkowników i dodawanie nowych</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 20px;
        }
        table {
            width: 60%;
            border-collapse: collapse;
            margin-bottom: 30px;
        }
        table, th, td {
            border: 1px solid #666;
        }
        th, td {
            padding: 8px 12px;
            text-align: left;
        }
        th {
            background-color: #eee;
        }
        .error {
            color: red;
            margin-bottom: 15px;
        }
        form {
            width: 300px;
        }
        label {
            display: block;
            margin-top: 10px;
        }
        input[type="text"], input[type="email"] {
            width: 100%;
            padding: 6px;
            box-sizing: border-box;
        }
        input[type="submit"] {
            margin-top: 15px;
            padding: 8px 12px;
        }
    </style>
</head>
<body>

    <h1>Lista użytkowników</h1>

    <?php if (isset($error_msg)): ?>
        <div class="error"><?= htmlspecialchars($error_msg, ENT_QUOTES, 'UTF-8') ?></div>
    <?php endif; ?>

    <!-- Tabela z rekordami -->
    <table>
        <thead>
            <tr>
                <th>ID</th>
                <th>Imię</th>
                <th>Email</th>
            </tr>
        </thead>
        <tbody>
            <?php if ($result && $result->num_rows > 0): ?>
                <?php while ($row = $result->fetch_assoc()): ?>
                    <tr>
                        <td><?= htmlspecialchars($row['id'], ENT_QUOTES, 'UTF-8') ?></td>
                        <td><?= htmlspecialchars($row['name'], ENT_QUOTES, 'UTF-8') ?></td>
                        <td><?= htmlspecialchars($row['email'], ENT_QUOTES, 'UTF-8') ?></td>
                    </tr>
                <?php endwhile; ?>
            <?php else: ?>
                <tr>
                    <td colspan="3">Brak rekordów w bazie.</td>
                </tr>
            <?php endif; ?>
        </tbody>
    </table>

    <!-- Formularz do dodawania nowych rekordów -->
    <h2>Dodaj nowego użytkownika</h2>
    <form action="<?= htmlspecialchars($_SERVER['PHP_SELF'], ENT_QUOTES, 'UTF-8') ?>" method="post">
        <label for="name">Imię i nazwisko:</label>
        <input type="text" id="name" name="name" required>

        <label for="email">Email:</label>
        <input type="email" id="email" name="email" required>

        <input type="submit" value="Dodaj">
    </form>

</body>
</html>
<?php
// -------------------------------------------
// 5. Zamknięcie połączenia z bazą
// -------------------------------------------
$conn->close();
?>
```

---

### Krótkie omówienie poszczególnych fragmentów:

1. **Dane dostępowe i połączenie z bazą**
   Na początku definiujemy zmienne `$host`, `$db_user`, `$db_pass`, `$db_name`, a następnie tworzymy nowe połączenie `$conn = new mysqli(...)`. Sprawdzamy, czy nie wystąpił błąd (`$conn->connect_error`) i ustawiamy kodowanie na UTF-8.

2. **Obsługa formularza (metoda POST)**

   * Jeśli formularz został przesłany (`$_SERVER['REQUEST_METHOD'] === 'POST'`), zaczytujemy wartości `$_POST['name']` oraz `$_POST['email']`.
   * Sprawdzamy, czy oba pola nie są puste.
   * Korzystamy z **prepared statement** (`$conn->prepare(...)`), aby bezpiecznie wstawić dane do tabeli `users`.
   * Po udanym wstawieniu przekierowujemy przeglądarkę z powrotem na ten sam plik (żeby uniknąć ponownego wysłania danych przy odświeżeniu).

3. **Pobieranie rekordów z tabeli**

   * Wykonujemy zapytanie `SELECT id, name, email FROM users ORDER BY id DESC`.
   * Wynik zapytania zapisujemy w `$result`.
   * W HTML-u w sekcji `<tbody>` iterujemy po `$result->fetch_assoc()` i wyświetlamy wszystkie wiersze w tabeli.

4. **Formularz HTML**

   * Formularz ma dwa pola: tekstowe dla imienia (name="name") i email (name="email").
   * Pola oznaczone jako `required`, więc przeglądarka nie wyśle formularza, jeśli pozostaną puste.

5. **Bezpieczeństwo wyświetlania**

   * Przy echo każdej wartości z bazy stosujemy `htmlspecialchars(..., ENT_QUOTES, 'UTF-8')`, aby uniknąć potencjalnego ataku XSS.

6. **Zamknięcie połączenia**

   * Po wygenerowaniu całego HTML-a zamykamy połączenie z bazą: `$conn->close();`.

---

### Jak uruchomić

1. **Utwórz bazę i tabelę** (jeśli jeszcze nie istnieją). Przykład w MySQL:

   ```sql
   CREATE DATABASE moja_baza CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
   USE moja_baza;

   CREATE TABLE users (
     id INT NOT NULL AUTO_INCREMENT,
     name VARCHAR(100) NOT NULL,
     email VARCHAR(100) NOT NULL,
     PRIMARY KEY (id)
   ) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;
   ```
2. **Wstaw plik `index.php`** do katalogu swojego serwera WWW (np. `C:\xampp\htdocs\` w XAMPP czy `/var/www/html/` w Linux/Apache).
3. **Dostosuj dane dostępowe** (host, użytkownik, hasło, nazwa bazy) w nagłówku pliku PHP.
4. **Otwórz w przeglądarce** adres `http://localhost/index.php` (lub odpowiednio, jeśli masz inny wirtualny host).

Po wejściu na stronę zobaczysz listę wszystkich użytkowników z tabeli `users` (jeśli są rekordy), a pod nią formularz do dodawania nowych wpisów. Po wypełnieniu formularza i kliknięciu „Dodaj” zostaniesz przekierowany z powrotem na tę samą stronę, a nowy rekord pojawi się w tabeli.

---

W razie potrzeby możesz zmodyfikować:

* Nazwy tabeli i kolumn (np. `products(name, price)`, jeśli chcesz inną tabelę).
* Stylowanie CSS (wbudowane w `<style>` w nagłówku) według własnych potrzeb.
* Sposób walidacji lub dodatkowe pola w formularzu (np. `tel`, `textarea` itd.).

To pełny, minimalny przykład, który można dowolnie rozbudowywać (np. obsługa edycji, usuwania czy paginacji).
