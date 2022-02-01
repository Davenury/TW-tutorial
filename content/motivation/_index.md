---
title: "Motywacja"
draft: false
weight: 10
---

### Po co teoria współbieżności?

* Przetwarzanie współbieżne jest obecnie podstawowym paradygmatem działania systemów komputerowych. Wyjątkami mogą być proste sterowniki wbudowane.
* Podstawowe cechy przetwarzania współbieżnego:
  * współdzielenie zasobów (systemy operacyjne)
  * działanie w sieci komputerowej (przetwarzanie rozproszone)
  * jednoczesne wykorzystanie wielu procesorów (przetwarzanie równoległe)
* Wytwarzanie systemów współbieżnych nie daje się zautomatyzować w dostatecznym stopniu, w przeciwieństwie do tworzenia systemów sekwencyjnych.

Teoria współbieżności to część inżynierii oprogramowania, która pozwala zrozumieć istotę działania systemów współbieżnych. Dodatkowo wprowadza ich formalny opis oraz tworzy modele służące analizie i projektowaniu.

---

### Poziomy opisu modelowania i programowania systemów

* Poziom rejestrów - zmiana stanu rejestru (to, co na pierwszych labach z mikroprocków)
* Poziom zmiennych - zmiana wartości
* Poziom funkcji - zmiana wartości parametru, wywołanie, powrót
* Poziom procesu - utworzenie, usunięcie zawieszenie, odwieszenie, wysłanie i odbiór komunikatu
* Poziom obiektów, komponentów, agentów - kreacja, destrukcja, wysłanie i odbiór komunikatu

Uwaga! Jeśli modelujemy coś współbieżnego, to nie patrzymy na poziom rejestrów i zmiennych (to by była mordęga, jak nauka do tego egzaminu...).

---

### Semafory, bariery, monitory

Ogólnie chodzi o to, żeby operacje na jakichś współdzielonych strukturach danych nie były wykonywane w tym samym czasie, bo robi to w chuja problemów (problem wyścigu, etc.).

Operacja atomiczna - taka, że musi być wykonana w całości przez jedną jednostkę (na przykład proces), a w trakcie jej wykonywania nikt nie ma dostępu do tej struktury.

Operacje na strukturze (P, V - zajęcie i zwolnienie semafora, wait, signal) są wzajemnie wykluczane.

Komunikacja blokująca - synchronizacja w systemach z pamięcią lokalną i współdzieloną oraz w sieciowych środowiskach rozproszonych.


* Prymitywy komunikacyjne - funkcje działające w pamięci lokalnej sterujące działaniem jednostki przetwarzającej (procesu, itp.)
* Wysyłanie poprzez send (nieblokujące) lub bsend (blokujące). Obydwa przyjmują destination address oraz msg - wiadomość do wysłania.
* Odbieranie przez receive i breceive (analogicznie nieblokujące i blokujące). Przyjmują adres wysyłającego, wskaźnik na bufor, gdzie zapisać wiadomość. Receive przyjmuje dodatkowo trzeci argument, w którym zapisze, czy wiadomość przyszła (1), czy jednak nie (0). Jeśli w breceive nie nadejdzie komunikat, to funkcja zawiesza działanie jednostki, dopóki komunikat nie przyjdzie.

Przekazywanie komunikatów w pamięci dzielonej odbywa się za pośrednictwem skrzynki pocztowej, która jest dzielona przez jednostki korespondujące. Oczywiście operacje na tej skrzynce wzajemnie się wykluczają (nie można równocześnie wkładać do skrzynki i wyciągać z niej).

W środowisku rozproszonym przekazywanie komunikatów realizują protokoły komunikacyjne. Wiadomości są lokalnie buforowane.

