**Notatka: Najpotrzebniejsze atrybuty i metody obiektów DOM w JavaScript**
*Przydatne na egzamin zawodowy INF.03*

---

## 1. Wybieranie elementów w dokumencie

1. **`document.getElementById(id)`**

   * Zwraca pojedynczy element o zadanym atrybucie `id`.
   * Zastosowanie: szybkie pobranie elementu, gdy znamy jego unikalne `id`.

   ```javascript
   const box = document.getElementById('myBox');
   // Zakładamy w HTML: <div id="myBox">Zawartość</div>
   console.log(box); // <div id="myBox">Zawartość</div>
   ```

2. **`document.getElementsByClassName(className)`**

   * Zwraca „HTMLCollection” (żywą kolekcję) wszystkich elementów mających zadaną klasę.
   * Zastosowanie: gdy chcemy jednocześnie operować na kilku elementach z tą samą klasą.

   ```javascript
   const items = document.getElementsByClassName('menu-item');
   // HTML: <li class="menu-item">A</li><li class="menu-item">B</li>
   console.log(items.length); // 2
   ```

3. **`document.getElementsByTagName(tagName)`**

   * Zwraca HTMLCollection wszystkich elementów o danym tagu (np. `div`, `p`, `li`).
   * Zastosowanie: gdy chcemy pobrać wszystkie elementy danego typu.

   ```javascript
   const paragraphs = document.getElementsByTagName('p');
   console.log(paragraphs[0].textContent); // tekst pierwszego <p>
   ```

4. **`document.querySelector(selector)`**

   * Zwraca pierwszy element pasujący do danego selektora CSS.
   * Zastosowanie: bardzo uniwersalne – można znaleźć po id, klasie, tagu lub dowolnym złożonym selektorze.

   ```javascript
   const firstRed = document.querySelector('.color-red');
   // Pobiera pierwszy element z klasą "color-red"
   ```

5. **`document.querySelectorAll(selector)`**

   * Zwraca statyczną listę (`NodeList`) wszystkich elementów pasujących do selektora CSS.
   * Zastosowanie: gdy chcemy przejść pętlą po wielu elementach wybranych za pomocą selektora.

   ```javascript
   const buttons = document.querySelectorAll('button.submit');
   buttons.forEach(btn => {
     console.log(btn.innerText);
   });
   ```

---

## 2. Atrybuty (właściwości) elementów

1. **`.id`**

   * Pobiera lub ustawia wartość atrybutu `id` elementu.

   ```javascript
   const el = document.querySelector('div');
   console.log(el.id);    // np. "header"
   el.id = 'mainHeader';  // zmiana na "mainHeader"
   ```

2. **`.className`**

   * Pobiera lub ustawia cały ciąg klas (jako string).

   ```javascript
   const el = document.querySelector('.card');
   console.log(el.className); // "card highlighted"
   el.className = 'card selected'; // nadpisanie klas
   ```

3. **`.classList`**

   * Zwraca obiekt `DOMTokenList`, umożliwiający manipulację pojedynczymi klasami.
   * Metody:

     * `.add('nazwa-klasy')` – dodaje klasę, jeśli jej nie ma,
     * `.remove('nazwa-klasy')` – usuwa klasę,
     * `.toggle('nazwa-klasy')` – przełącza stan (dodaje/usuwa),
     * `.contains('nazwa')` – sprawdza, czy klasa istnieje.

   ```javascript
   const box = document.getElementById('box');
   box.classList.add('visible');
   box.classList.toggle('highlight'); // jeśli było – usuwa, jeśli nie było – dodaje
   if (box.classList.contains('visible')) {
     console.log('Box jest widoczny');
   }
   ```

4. **`.innerHTML`**

   * Pobiera lub ustawia całą zawartość HTML elementu (wraz z tagami).
   * Uwaga: wstawiane treści mogą być traktowane jako kod, więc ostrożnie z bezpieczeństwem (XSS).

   ```javascript
   const container = document.querySelector('#container');
   container.innerHTML = '<h2>Nowy tytuł</h2><p>Opis...</p>';
   // Zamienia całą zawartość kontenera na podany kod HTML
   ```

5. **`.textContent`**

   * Pobiera lub ustawia jedynie tekst wewnątrz elementu (bez tagów).
   * Bezpieczniejsze niż `innerHTML`, gdy operujemy na samym tekście.

   ```javascript
   const title = document.querySelector('h1');
   console.log(title.textContent); // np. "Witaj świecie"
   title.textContent = 'Nowy nagłówek';
   ```

6. **`.value`** (dla pól formularza)

   * Pobiera lub ustawia wartość pól `<input>`, `<textarea>`, `<select>` itp.

   ```javascript
   const input = document.querySelector('input[name="email"]');
   console.log(input.value); // adres email wpisany przez użytkownika
   input.value = 'kontakt@przyklad.pl'; // nadpisanie wartości
   ```

7. **`.style`**

   * Bezpośredni dostęp do stylów inline (CSS) elementu.
   * Przykład: ustawianie koloru, wielkości czcionki, marginesów itp.

   ```javascript
   const box = document.getElementById('box');
   box.style.backgroundColor = 'yellow';
   box.style.marginTop = '20px';
   // Zwróć uwagę: własności CSS w JavaScript piszemy w camelCase, np. backgroundColor
   ```

8. **`.attributes`**

   * Zwraca kolekcję (`NamedNodeMap`) wszystkich atrybutów danego elementu.
   * Rzadziej używane w prostych scenariuszach, ale przydatne, gdy trzeba dynamicznie przejrzeć wszystkie atrybuty.

   ```javascript
   const img = document.querySelector('img');
   for (let attr of img.attributes) {
     console.log(attr.name, '=', attr.value);
   }
   ```

9. **`.dataset`**

   * Obiekt umożliwiający odczyt i zapis wartości atrybutów `data-*`.
   * Własności w `dataset` odpowiadają nazwom po „data-” w camelCase.

   ```html
   <!-- HTML -->
   <div id="product" data-id="123" data-name="Notes">...</div>
   ```

   ```javascript
   const prod = document.getElementById('product');
   console.log(prod.dataset.id);   // "123"
   console.log(prod.dataset.name); // "Notes"
   prod.dataset.category = 'notebooks'; // ustawia atrybut data-category="notebooks"
   ```

---

## 3. Nawigacja po strukturze drzewa DOM

1. **`.parentNode`**

   * Zwraca rodzica (nadrzędny węzeł) danego elementu.

   ```javascript
   const li = document.querySelector('li.active');
   const parentUl = li.parentNode;
   console.log(parentUl.tagName); // "UL"
   ```

2. **`.childNodes`**

   * Zwraca „NodeList” zawierającą wszystkie bezpośrednie węzły potomne (także tekstowe lub komentarze).

   ```javascript
   const div = document.getElementById('wrapper');
   console.log(div.childNodes); 
   // Może zawierać: tekst (whitespace), elementy, komentarze
   ```

3. **`.children`**

   * Zwraca kolekcję (`HTMLCollection`) wyłącznie bezpośrednich elementów potomnych (bez węzłów tekstowych).

   ```javascript
   const ul = document.querySelector('ul');
   console.log(ul.children); // tylko elementy <li>, bez tekstów
   ```

4. **`.firstChild`** i **`.lastChild`**

   * `firstChild` – zwraca pierwszy węzeł potomny (może to być tekst),
   * `lastChild` – zwraca ostatni węzeł potomny.

   ```javascript
   const container = document.querySelector('#container');
   console.log(container.firstChild); // może być np. tekst (spacja) lub element
   console.log(container.lastChild);  // analogicznie
   ```

5. **`.firstElementChild`** i **`.lastElementChild`**

   * Zwracają odpowiednio pierwszy i ostatni bezpośredni element (pomijają węzły tekstowe).

   ```javascript
   const list = document.querySelector('ol');
   console.log(list.firstElementChild.tagName); // np. "LI"
   console.log(list.lastElementChild.tagName);  // np. "LI"
   ```

6. **`.nextSibling`** i **`.previousSibling`**

   * `nextSibling` – zwraca sąsiedni węzeł (może być tekst).
   * `previousSibling` – zwraca poprzedni węzeł.

   ```javascript
   const item = document.getElementById('item2');
   console.log(item.nextSibling);     // może być tekst (whitespace) albo #text albo element
   console.log(item.previousSibling); // analogicznie
   ```

7. **`.nextElementSibling`** i **`.previousElementSibling`**

   * Zwracają sąsiednie elementy (pomijają węzły tekstowe).

   ```javascript
   const current = document.querySelector('.current');
   console.log(current.nextElementSibling);     // następny <li> lub inny element
   console.log(current.previousElementSibling); // poprzedni <li>
   ```

---

## 4. Tworzenie i modyfikacja struktury DOM

1. **`document.createElement(tagName)`**

   * Tworzy nowy, pusty element o zadanym tagu.
   * Zastosowanie: budowanie nowych elementów przed wstawieniem ich do drzewa DOM.

   ```javascript
   const newDiv = document.createElement('div');
   newDiv.id = 'alertBox';
   newDiv.className = 'alert warning';
   newDiv.textContent = 'Uwaga! Coś się stało.';
   ```

2. **`document.createTextNode(text)`**

   * Tworzy nowy węzeł tekstowy (niezależnie od `innerHTML`).
   * Zastosowanie: gdy chcemy mieć precyzyjną kontrolę nad wstawianiem tekstu.

   ```javascript
   const textNode = document.createTextNode('To jest ważna wiadomość.');
   const p = document.createElement('p');
   p.appendChild(textNode);
   document.body.appendChild(p);
   ```

3. **`.appendChild(node)`**

   * Dodaje węzeł („node” może być elementem lub tekstem) jako ostatniego potomka.
   * Zastosowanie: wstawianie nowo utworzonych elementów do rodzica.

   ```javascript
   const ul = document.querySelector('ul');
   const li = document.createElement('li');
   li.textContent = 'Nowa pozycja';
   ul.appendChild(li);
   ```

4. **`.insertBefore(newNode, referenceNode)`**

   * Wstawia `newNode` przed `referenceNode` w tej samej kolekcji potomków.
   * Zastosowanie: kontrolowane wstawianie w konkretne miejsce.

   ```javascript
   const ul = document.querySelector('ul');
   const li = document.createElement('li');
   li.textContent = 'Pozycja na początku';
   ul.insertBefore(li, ul.firstElementChild);
   // Wstawia li jako pierwszy <li> w liście
   ```

5. **`.removeChild(node)`**

   * Usuwa wskazany węzeł potomny z rodzica.

   ```javascript
   const box = document.getElementById('oldBox');
   box.parentNode.removeChild(box);
   // Usuwa element <div id="oldBox">...</div> z drzewa DOM
   ```

6. **`.replaceChild(newNode, oldNode)`**

   * Zastępuje `oldNode` przez `newNode` wśród potomków danego rodzica.

   ```javascript
   const oldImg = document.querySelector('img#logo');
   const newImg = document.createElement('img');
   newImg.src = 'logo2.png';
   oldImg.parentNode.replaceChild(newImg, oldImg);
   ```

---

## 5. Manipulacja atrybutami poszczególnych elementów

1. **`.getAttribute(name)`**

   * Pobiera wartość dowolnego atrybutu (nie tylko standardowego).

   ```javascript
   const link = document.querySelector('a');
   console.log(link.getAttribute('href')); // np. "https://przyklad.pl"
   ```

2. **`.setAttribute(name, value)`**

   * Ustawia lub tworzy dowolny atrybut z podaną wartością.

   ```javascript
   const img = document.createElement('img');
   img.setAttribute('src', 'zdjecie.jpg');
   img.setAttribute('alt', 'Przykładowy obrazek');
   document.body.appendChild(img);
   ```

3. **`.removeAttribute(name)`**

   * Usuwa wskazany atrybut z elementu.

   ```javascript
   const input = document.getElementById('username');
   input.removeAttribute('disabled');
   // Usunięcie atrybutu "disabled" sprawia, że pole staje się aktywne
   ```

4. **`.hasAttribute(name)`**

   * Sprawdza, czy element posiada dany atrybut.

   ```javascript
   const btn = document.querySelector('button');
   if (!btn.hasAttribute('disabled')) {
     console.log('Przycisk jest aktywny');
   }
   ```

---

## 6. Obsługa zdarzeń (eventów)

1. **`.addEventListener(eventType, handler)`**

   * Rejestruje funkcję (`handler`) do obsługi zdarzenia (`eventType`) na danym elemencie.
   * Najczęściej spotykane typy: `"click"`, `"input"`, `"submit"`, `"keydown"`, `"mouseover"` itp.

   ```javascript
   const btn = document.getElementById('saveButton');
   btn.addEventListener('click', function(event) {
     alert('Przycisk kliknięty!');
   });
   ```

2. **`.removeEventListener(eventType, handler)`**

   * Usuwa wcześniej zarejestrowany nasłuchiwacz (handler) zdarzenia.

   ```javascript
   function onClick(e) {
     console.log('Kliknięto');
   }
   btn.addEventListener('click', onClick);
   // ... potem:
   btn.removeEventListener('click', onClick);
   ```

3. **Atrybuty typu `onclick`, `onchange` (bezpośrednie)**

   * Można przypisać „inline” lub przez JavaScript, ale odradza się tę metodę na rzecz `addEventListener`.

   ```html
   <button id="b1" onclick="alert('Klik!')">Kliknij mnie</button>
   ```

   ```javascript
   const b2 = document.getElementById('b2');
   b2.onclick = function() {
     console.log('Inny handler');
   };
   ```

---

## 7. Inne przydatne właściwości i metody

1. **`.children.length`**

   * Zwraca liczbę elementów potomnych (bez węzłów tekstowych).

   ```javascript
   const ul = document.querySelector('ul');
   console.log(ul.children.length); // ile jest <li> w liście
   ```

2. **`.cloneNode(deep)`**

   * Tworzy kopię węzła.
   * `deep = true` – kopiuje również wszystkie potomki (rekurencyjnie),
   * `deep = false` – tylko sam element, bez potomków.

   ```javascript
   const original = document.getElementById('card');
   const copy = original.cloneNode(true); 
   document.body.appendChild(copy);
   ```

3. **`.toggleAttribute(name)`** (współczesne przeglądarki)

   * Przełącza istnienie atrybutu na elemencie: jeśli go nie ma – doda, jeśli jest – usunie.

   ```javascript
   const img = document.querySelector('img');
   img.toggleAttribute('hidden'); // dodaje albo usuwa atrybut hidden
   ```

4. **`.scrollIntoView(options)`**

   * Przewija stronę, aby dany element znalazł się w widoku.
   * `options` może określać zachowanie przewijania (np. `{ behavior: "smooth" }`).

   ```javascript
   const section = document.getElementById('section3');
   section.scrollIntoView({ behavior: 'smooth', block: 'start' });
   ```

5. **`.focus()` i `.blur()`**

   * `focus()` – ustawia fokus (np. na polu tekstowym),
   * `blur()` – usuwa fokus.

   ```javascript
   const input = document.querySelector('input#search');
   input.focus(); // kursor od razu w polu tekstowym
   ```

---

## 8. Przykładowy mini-scenariusz zastosowania kilku atrybutów naraz

Załóżmy, że tworzymy prosty formularz umożliwiający dodawanie nowych zadań do listy:

```html
<!-- HTML -->
<form id="taskForm">
  <input type="text" id="newTask" placeholder="Wpisz nowe zadanie" required>
  <button type="submit" id="addButton">Dodaj zadanie</button>
</form>
<ul id="taskList"></ul>
```

```javascript
// JavaScript:
const form = document.getElementById('taskForm');
const input = document.getElementById('newTask');
const list = document.getElementById('taskList');

form.addEventListener('submit', function(e) {
  e.preventDefault(); // zapobiega przeładowaniu strony

  // 1. Pobranie wartości z pola:
  const text = input.value.trim();
  if (text === '') {
    alert('Podaj treść zadania');
    return;
  }

  // 2. Utworzenie nowego elementu <li>:
  const li = document.createElement('li');
  li.textContent = text;            // .textContent – tekst zadania
  li.classList.add('task-item');    // .classList – nadanie klasy

  // 3. Dodanie przycisku „Usuń” do <li>:
  const removeBtn = document.createElement('button');
  removeBtn.textContent = 'Usuń';
  removeBtn.setAttribute('type', 'button');    // .setAttribute – ustawiamy type
  removeBtn.classList.add('remove-btn');
  li.appendChild(removeBtn);                   // .appendChild – wstawienie dziecka

  // 4. Podpięcie nasłuchiwacza do usuwania zadania:
  removeBtn.addEventListener('click', function() {
    list.removeChild(li);  // .removeChild – usuwanie <li> z listy
  });

  // 5. Wstawienie <li> na koniec listy:
  list.appendChild(li);

  // 6. Wyczyszczenie pola i ustawienie focus:
  input.value = '';
  input.focus();          // .focus() – ustawienie kursora z powrotem w polu
});
```

**Omówienie użytych atrybutów i metod:**

* `getElementById` – szybkie pobranie istniejących elementów formularza.
* `.value` – odczytanie wpisanej treści zadania.
* `createElement` – dynamiczne tworzenie nowych `<li>` i `<button>`.
* `.textContent` – wstawianie tekstu (bez ryzyka XSS).
* `.classList.add` – nadawanie klas CSS do odpowiedniego formatowania.
* `.setAttribute` – ustawianie atrybutu `type="button"` na elemencie `<button>`.
* `.appendChild` – „sklejanie” elementów w strukturze DOM: dodanie przycisku do `<li>`, a następnie `<li>` do `<ul>`.
* `addEventListener` – podpięcie zachowania usuwania zadania po kliknięciu.
* `.removeChild` – usuwanie węzła `<li>` z listy zadań.
* `.focus()` – automatyczne ustawienie kursora z powrotem w polu, by użytkownik mógł od razu wpisać kolejne zadanie.

---

## 9. Podsumowanie najważniejszych atrybutów/metod

| Kategoria                         | Atrybut / Metoda                                 | Cel / Zastosowanie                                       |
| --------------------------------- | ------------------------------------------------ | -------------------------------------------------------- |
| **Wybieranie elementów**          | `getElementById(id)`                             | Pobranie jednego elementu po `id`.                       |
|                                   | `getElementsByClassName(cls)`                    | Pobranie kolekcji elementów po klasie (HTMLCollection).  |
|                                   | `getElementsByTagName(tag)`                      | Pobranie kolekcji elementów po tagu.                     |
|                                   | `querySelector(sel)`                             | Pierwszy element pasujący do selektora CSS.              |
|                                   | `querySelectorAll(sel)`                          | Wszystkie elementy pasujące do selektora CSS (NodeList). |
| **Atrybuty elementu**             | `.id`                                            | Pobranie/ustawienie `id`.                                |
|                                   | `.className`                                     | Pobranie/ustawienie ciągu klas (string).                 |
|                                   | `.classList`                                     | Manipulacja pojedynczymi klasami (dodaj, usuń, toggle).  |
|                                   | `.innerHTML`                                     | Pobranie/ustawienie całej zawartości HTML.               |
|                                   | `.textContent`                                   | Pobranie/ustawienie zawartości tekstowej (bez HTML).     |
|                                   | `.value`                                         | Pobranie/ustawienie wartości pól formularza.             |
|                                   | `.style`                                         | Modyfikacja stylów inline (camelCase dla właściwości).   |
|                                   | `.attributes`                                    | Kolekcja wszystkich atrybutów (NamedNodeMap).            |
|                                   | `.dataset`                                       | Odczyt/zapis atrybutów `data-*`.                         |
| **Nawigacja w drzewie DOM**       | `.parentNode`                                    | Rodzic (nadrzędny węzeł).                                |
|                                   | `.childNodes`                                    | Wszystkie węzły potomne (w tym tekstowe).                |
|                                   | `.children`                                      | Tylko elementy potomne.                                  |
|                                   | `.firstChild`, `.lastChild`                      | Pierwszy/ostatni węzeł potomny.                          |
|                                   | `.firstElementChild`, `.lastElementChild`        | Pierwszy/ostatni element potomny.                        |
|                                   | `.nextSibling`, `.previousSibling`               | Sąsiednie węzły (w tym tekstowe).                        |
|                                   | `.nextElementSibling`, `.previousElementSibling` | Sąsiednie elementy.                                      |
| **Tworzenie i wstawianie węzłów** | `createElement(tag)`                             | Tworzenie pustego elementu.                              |
|                                   | `createTextNode(text)`                           | Tworzenie węzła tekstowego.                              |
|                                   | `.appendChild(node)`                             | Dodawanie węzła jako ostatniego potomka.                 |
|                                   | `.insertBefore(newNode, refNode)`                | Wstawianie węzła przed innym węzłem.                     |
|                                   | `.removeChild(node)`                             | Usuwanie wskazanego węzła potomnego.                     |
|                                   | `.replaceChild(newNode, oldNode)`                | Zastępowanie węzłów potomnych.                           |
|                                   | `.cloneNode(deep)`                               | Klonowanie węzła (z lub bez potomków).                   |
| **Manipulacja atrybutami**        | `.getAttribute(name)`                            | Pobranie wartości atrybutu.                              |
|                                   | `.setAttribute(name, value)`                     | Ustawienie/utworzenie atrybutu.                          |
|                                   | `.removeAttribute(name)`                         | Usunięcie atrybutu.                                      |
|                                   | `.hasAttribute(name)`                            | Sprawdzenie istnienia atrybutu.                          |
|                                   | `.toggleAttribute(name)`                         | Przełączenie istnienia atrybutu.                         |
| **Obsługa zdarzeń**               | `.addEventListener(evt, handler)`                | Rejestracja funkcji obsługi zdarzenia.                   |
|                                   | `.removeEventListener(evt, handler)`             | Usunięcie zarejestrowanego nasłuchiwacza zdarzenia.      |
|                                   | `[element].onclick = fn`                         | (starsza metoda) Przypisanie obsługi zdarzenia “klik”.   |
| **Inne przydatne**                | `.scrollIntoView(options)`                       | Przewinięcie strony do elementu.                         |
|                                   | `.focus()`, `.blur()`                            | Ustawienie/pozbawienie elementu focusu.                  |

---

### Uwagi końcowe

1. **Bezpieczeństwo**:

   * Stosując `.innerHTML`, pamiętaj o potencjalnym ryzyku wstrzyknięcia złośliwego kodu (XSS). Jeśli potrzebujesz tylko tekstu, użyj `.textContent`.
2. **Wydajność**:

   * Pobieranie elementu przez `getElementById` jest najszybsze.
   * Metody zwracające kolekcję (np. `getElementsByClassName`, `getElementsByTagName`) zwracają „żywe” listy (HTMLCollection), które aktualizują się na bieżąco; z kolei `querySelectorAll` zwraca listę statyczną (NodeList).
3. **Nowoczesne API**:

   * Warto znać również funkcje `Element.closest(selector)` (wyszukiwanie najbliższego przodka pasującego do selektora) czy `Element.matches(selector)` (sprawdzenie, czy element pasuje do selektora).

   ```javascript
   const span = document.querySelector('span');
   if (span.closest('.container')) {
     console.log('Ten <span> ma przodka z klasą .container');
   }
   if (span.matches('.highlight')) {
     console.log('Ten <span> ma klasę .highlight');
   }
   ```

Powyższe właściwości i metody stanowią fundament pracy z DOM w JavaScript. Opanowanie ich pozwoli Ci efektywnie manipulować strukturą dokumentu, reagować na zdarzenia i dynamicznie modyfikować zawartość strony – co będzie niezbędne na egzaminie INF.03!
