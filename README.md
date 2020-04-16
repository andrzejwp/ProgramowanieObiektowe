# Programowanie Obiektowe

W ramach kursu będziemy pracować nad programem imitującym arkusz kalkulacyjny. 

## Lab 1

Oczekiwania odnośnie programu:
- mogę zmieniać rozmiar tablicy
- mogę aktualizować zawartość tablicy
- mogę wyświetlać zawartość tablicy na ekranie
- chcę komunikować się z programem przy pomocy tekstowego interfejsu użytkownika.

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

## Lab 3

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
