# Programowanie Obiektowe

W ramach kursu będziemy pracować nad programem imitującym arkusz kalkulacyjny. 

## Lab 1

Oczekiwania odnośnie programu:
- mogę zmieniać rozmiar tablicy
- mogę aktualizować zawartość tablicy
- mogę wyświetlać zawartość tablicy na ekranie
- chcę komunikować się z programem przy pomocy tekstowego interfejsu użytkownika
- chcę aby zawartość arkusza mogła być zapisywana na dysk i wczytywana z dysku.

Program dzielimy na 4 pliki:
- main.cpp
- tablica.cpp
- tablica_wysw.cpp
- menu.cpp

1. upewniacie się Państwo, że potraficie zbudować program składający się z 4 plików (`g++ plik1.cpp plik2.cpp ...`).
2. uzupełniacie poszczególne funkcje w plikach, ale bez ich zawartości
3. zastanawiacie się nad tym jakie WEJSCIA i jakie WYJSCIA powinny posiadać poszczególne funkcje - uzupełniacie argumenty i typy zwracane
4. tworzycie plik Makefile, w którym opisujecie sposób budowania postaci binarnej waszego programu, który składa się z 4 obiektów (plików .o)
5. uzupełniacie funkcje w pliku menu.cpp, tak aby interfejs użytkownika działał zgodnie z oczekiwaniami
6. uzupełniacie funkcje w pliku tablica.cpp.


## Lab 2

Program rozbudowujemy o możliwość zapisu danych do pliku, wczytywania z pliku. Sugerowany format pliku:

```
3 (liczba wierszy)
2 (liczba koliumn)
1,23 (liczby oddzielone przecinikiem)
2,35
32,18
```

Proszę pamiętać o zachowaniu podstawowej higieny w kodzie źródłowym przesyłanych programów. 


### Przykładowe błędy:

Poniżej przykłady, z pozoru błahych, acz opłakanych w skutkach, zaniechań i błędów jakie popełniacie Państwo nagminnie:

1. Brak wcięć:

    ```
    #include <iostream>
    using namespace std;

    int main()
    {
    for(int i=0; i<10; i++){
    cout << i << endl;
    }
    }
    ```
2. Pętle i instrukcje warunkowe bez klamr:
    ```
    int main(){
    for(int i=0; i<10; i++)
    cout << i << endl;
    }
    ```
3. Brak inicjalizacji zmiennych:
    ```
    int main() {
        int rozmiar;
        int *arr[rozmiar];
    }
    ```
4. Niejawne korzystanie z referencji:

    ```
    int dodaj(int a, int &b){
        b = a+b;
        return b;
    }
    int main(){
        int a=2;
        int b=3;
        int wynik=0;
        
        wynik = dodaj(a,b); // spodziewamy sie wynik = 5 
        wynik = dodaj(a,b); // spodziewamy sie wynik = 5, a mamy 7.
    }
    ```
5. Brak plików nagłówkowych, includowanie plików `.cpp`:
   Pliki `.cpp` nie powinny być włączane przez `#include`, do tego służą pliki **nagłówkowe**. W plikach nagłówkowych powinny znaleźć się **deklaracje** funkcji, wraz z ich doc-blockami (zgodnymi z formatem Doxygen). Definicje funkcji mają pozostać w plikach `.cpp`.
   
   ```
   #include "menu.cpp"
   ```
   
   a powinno być:
   
   ```
   #include "menu.h"
   ```
   
6. Brak docblocków (zgodnych z formatem Doxygen) w plikach nagłówkowych
   Pliki nagłówkowe miały być przez Państwa uzupełnione o dokumentację "wejść" i "wyjść" Państwa funkcji:
   
   ```
   /**
    * @param[in,out] arr - tablica dwuwymiarowa
    * @param[in] x - numer wiersza
    * @param[in] y - numer kolumny
    * @param[in] wartosc - wartość
    * @return - kod błędu lub 0 w przypadku powodzenia
    */
   int ustaw_wartosc(int **arr, int x, int y, int wartosc);
   ```

7. Brak informacji o wystąpieniu błędów, która powinna być przesyłana między podprogramami

W przypadku gdy jedna z funkcji napotka na problem w działaniu - należy tę informację zwrócić jako kod błędu (a kiedyś - jako wyjątek). Kod ten powinien zostać "obsłużony" w programie wywołującym daną funkcję - czyli w tym przypadku w menu.cpp, które jest doskonałym miejscem aby poinformować użytkownika o występowaniu problemów.

Poniżej przedstawiam jeden ze sposobów implementacji, analogiczny do tego, w jaki sposób funkcjonuje to w środowisku UNIX (kod wyjścia programu):

```

int ustawWartoscKomorki(int **arr, int iloscWierzy, int iloscKolumn, int wartosc, int wiersz, int kolumna){

   if(wiersz > iloscWierszy || kolumna > iloscKolumn){
      return ERR_INVALID_SIZE;
   }

   ...
   return 0;
}
```

a w taki sposób można poradzić sobie z taką sytuacją w programie wywołującym podprogram `ustawWartoscKomorki()`:

```
// ...
  int wartosc;
  cin >> wartosc;
  // ...

   int err = ustawWartoscKomorki(arr, 5, 5, wartosc, 10, 12);
   if(err){
      cout << "Wystapil blad - wskazano niepoprawny adres komorki do zmiany..." << endl;
   }
   
```


## Lab 3, max termin oddania: 18 maja

Proszę zdefiniować w programach strukturę `Tablica`, w której umieścicie Państwo:

- tablicę
- ilość wierszy
- ilość kolumn

Proszę dokonać refactoringu kodu swoich programów tak, aby funkcje, które do tej pory miały następujące prototypy:

```
int setCellValue(int **arr, int arrHeight, int arrWidth, int cellX, int cellY);
```

zyskały teraz kształ prostszy, zbliżony do:
```
int setCellValue(Tablica arr, int cellX, int cellY);
```

Proszę pamiętać również o aktualizacji docblocków Doxygena.

Proszę przygotować się do odpowiedzi na pytanie - co zyskujemy dzięki zastosowaniu takiej struktury?

Proszę dodatkowo zaimplementować w programie następujące funkcjonalności:

* sumowanie wg kolumn
* sumowanie wg wierszy
* znajdowanie w kolumnach i wierszach wartości:
    * najmniejszej
    * największej
    * średniej

## Lab 4, max termin oddania: 22 maja

Proszę na bazie programu z zadania 3 wykonać program, w którym struktura zostanie zastąpiona prostą klasą.

Proszę przeanalizować 2 sposoby implementacji:

```
class Array {
    public:
    int sizeX;
    int sizeY;
    int **arr;
    
    int setSize(int X, int Y);
    int setValue(int X, int Y, int value);
    
    ...
    
};
```

i 

```
class Tablica {
    
    public:
    int setSize(int X, int Y);
    int setValue(int X, int Y, int value);
    
    ...
     
    private:
    int rozmiarX;
    int rozmiarY;
    int **arr;
};
```

jakie są wady i zalety wykorzystania jednego, a jakie drugiego? Który sposób jest poprawny, dlaczego? Proszę przygotować się do odpowiedzi na te pytania.


## Lab 5, max termin oddania: 25 maja

Proszę do programu wprowadzić dodatkowo klasę, która będzie reprezentować wartość w pojedynczej komórce:

```
class Cell {
    // ?
};
```

proszę zaprezentować sposób obsługi różnych typów danych (np. `int`, `string`) - **uwaga**, na początek ograniczamy się do 1 typu danych na cały arkusz, ale chcemy mieć możliwość utworzenia arkusza dla liczb i arkusza dla danych tekstowych.


## Lab 6, max termin oddania: 5 czerwca

Proszę zaprezentować sposób umieszczenia w 1 arkuszu kolumn różnego typu, np 3 kolumnowy arkusz, w którym będą kolumny: {Liczby, Tekst, Tekst}.
