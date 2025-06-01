# Kompendium wiedzy z JavaScript

## Wprowadzenie

Kompendium ma na celu przygotowanie do egzaminu zawodowego INF.03 z zakresu programowania w JavaScript. Zawiera przegląd najważniejszych zagadnień, przykładów kodu oraz wskazówek egzaminacyjnych.

---

## 1. Podstawy języka

### 1.1. Wprowadzenie do JavaScript

* Historia i zastosowania JS
* Miejsce JS w stosie technologicznym (frontend, backend)
* Środowiska uruchomieniowe (przeglądarka, Node.js)

### 1.2. Struktura skryptu

```html
<script>
  // instrukcje JavaScript
</script>
```

* Dołączanie pliku zewnętrznego: `<script src="app.js"></script>`

### 1.3. Składnia podstawowa

* Instrukcje i wyrażenia
* Komentarze: `//`, `/* ... */`
* Zmienne: `let`, `const`, `var` (różnice)
* Typy danych: Number, String, Boolean, null, undefined, Symbol, Object

---

## 2. Operatory i wyrażenia

### 2.1. Operatory arytmetyczne

* `+`, `-`, `*`, `/`, `%`, `**`

### 2.2. Operatory porównania

* `==` vs `===`, `!=` vs `!==`, `<`, `>`, `<=`, `>=`

### 2.3. Operatory logiczne

* `&&`, `||`, `!`

### 2.4. Operator warunkowy (ternary)

```js
const wynik = (x > 0) ? 'dodatnia' : 'ujemna';
```

### 2.5. Operator przypisania oraz skróty

* `=`, `+=`, `-=`, `*=`, `/=`, `%=`

---

## 3. Sterowanie przepływem

### 3.1. Instrukcja warunkowa

* `if`, `else if`, `else`
* Przykład:

```js
if (wiek >= 18) {
  console.log('Pełnoletni');
} else {
  console.log('Niepełnoletni');
}
```

### 3.2. Instrukcja `switch`

```js
switch (kolor) {
  case 'czerwony': console.log('Stop'); break;
  case 'zielony': console.log('Jedź'); break;
  default: console.log('Nieznany kolor');
}
```

### 3.3. Pętle

* `for`
* `while`
* `do...while`
* Przykład pętli `for`:

```js
for (let i = 0; i < 5; i++) {
  console.log(i);
}
```

---

## 4. Funkcje

### 4.1. Deklaracja i wywołanie funkcji

```js
function dodaj(a, b) {
  return a + b;
}
const suma = dodaj(2, 3);
```

### 4.2. Funkcje wyrażeniowe i strzałkowe

```js
const mnoz = function(a, b) {
  return a * b;
};
const dziel = (a, b) => a / b;
```

### 4.3. Parametry domyślne i resztowe

```js
function przywitaj(imie = 'Gość') {
  console.log(`Cześć, ${imie}!`);
}
function sumaWszystkich(...liczby) {
  return liczby.reduce((acc, val) => acc + val, 0);
}
```

---

## 5. Programowanie obiektowe

### 5.1. Obiekty literalne

```js
const osoba = { imie: 'Jan', wiek: 30 };
```

### 5.2. Prototypy i dziedziczenie

```js
const zwierze = { zyje: true };
const kot = Object.create(zwierze);
kot.miau = () => console.log('Miau');
```

### 5.3. Klasy ES6

```js
class Czlowiek {
  constructor(imie, wiek) {
    this.imie = imie;
    this.wiek = wiek;
  }
  przedstawSie() {
    console.log(`Jestem ${this.imie}`);
  }
}
const ja = new Czlowiek('Anna', 25);
ja.przedstawSie();
```

---

## 6. Manipulacja DOM

### 6.1. Selekcja elementów

```js
const btn = document.getElementById('mojPrzycisk');
const paragrafy = document.querySelectorAll('p');
```

### 6.2. Zmiana treści i atrybutów

```js
btn.textContent = 'Kliknij mnie!';
img.setAttribute('src', 'obraz.jpg');
```

### 6.3. Tworzenie i usuwanie elementów

```js
const li = document.createElement('li');
li.textContent = 'Nowy element';
ul.appendChild(li);
ul.removeChild(li);
```

---

## 7. Obsługa zdarzeń

```js
element.addEventListener('click', (e) => {
  console.log('Kliknięto element', e.target);
});
```

* Najczęstsze zdarzenia: `click`, `input`, `submit`, `load`
* Delegacja zdarzeń

---

## 8. Nowoczesne funkcje ES6+

* Destrukturyzacja tablic i obiektów
* Spread i rest (`...`)
* Template strings (`` `tekst ${zmienna}` ``)
* `let`, `const` vs `var`
* Moduły: `import`, `export`

---

## 9. Programowanie asynchroniczne

### 9.1. Callbacks

```js
setTimeout(() => console.log('Po 1s'), 1000);
```

### 9.2. Promisy

```js
const obietnica = new Promise((resolve, reject) => {
  if(sukces) resolve('OK'); else reject('Błąd');
});
obietnica.then(msg => console.log(msg)).catch(err => console.error(err));
```

### 9.3. Async/Await

```js
async function pobierzDane() {
  try {
    const resp = await fetch('https://api.example.com');
    const data = await resp.json();
    console.log(data);
  } catch(err) {
    console.error(err);
  }
}
```

---

## 10. Fetch API i AJAX

```js
fetch('dane.json')
  .then(response => response.json())
  .then(data => console.log(data));
```

* Obsługa błędów
* CORS

---

## 11. Moduły i bundlery

* Moduły ES: `export`, `import`
* Bundlery: Webpack, Rollup (podstawy konfiguracji)

---

## 12. Najlepsze praktyki i wzorce

* DRY (Don't Repeat Yourself)
* SOLID (podstawowe zasady)
* Unikanie globalnego scope
* Linting (ESLint), formatowanie (Prettier)

---

## 13. Przygotowanie do egzaminu

* Typowe zadania: manipulacja DOM, funkcje, pętle, warunki, praca z tablicami
* Przykładowe pytania egzaminacyjne
* Polecane materiały:

  * MDN Web Docs
  * Oficjalna dokumentacja ECMA
  * Kursy online (freeCodeCamp, Codecademy)

---

*Powodzenia na egzaminie!*
