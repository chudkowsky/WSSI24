## Zad1.1
### A - X i Y rodzeństwo
### B - X i Y to rodzeństwo cioteczne 
### C - X i Y to dziadkowie wspolnego wnuka
### D - Y jest macochą/ojczymem X
### E - X i Y jest rodzeństwem przyrodnim
### F - Przyjmując, że posiadanie dziecka oznacza ślub to X to szwagier/szwagierka Y 
### G - kazirodczy przypadek rodzeństwa przyrodniego
## Zad1.2
```
rodzenstwo(X, Y) :-
    rodzic(Z, X),
    rodzic(Z, Y),  
    X \= Y.      

rodzenstwo_cioteczne(X, Y) :-
    rodzenstwo(Z, W), 
    rodzic(Z, X),       
    rodzic(W, Y),       
    X \= Y,
    Z \= W.

dziadkowie_wspolnego_wnuka(X,Y) :-
    rodzic(X,Z),
    rodzic(Y,W),
    rodzic(Z,Q),
    rodzic(W,Q),
    W \= Q,
    Z \= Q,
    Y \= W,
    X \= Z.

macocha_lub_ojczym(X,Y) :-
    rodzic(Z,Y),
    rodzic(Z,W),
    rodzic(X,W),
    Z \= X,
    Z \= Y,
    Z \= W,
    W \= Y,
    W \= X,
    Y \= X.
rodzenstwo_przyrodnie(X, Y) :-
    rodzic(Z, X),
    rodzic(Z, Y),
    X \= Y,
    \+ rodzenstwo(X, Y).

szwagier_lub_szwagierka(X, Y) :-
    rodzic(Z, X),
    rodzic(Z, Y),
    X \= Y,
    \+ rodzenstwo(X, Y).
```
 
## ćwiczenie 
```
lubi(pawel, kasia).
lubi(kasia,ania).
lubi(kasia,pawel).
lubi(jan, ania).
lubi(ania, jan).

mezczyzna(jan).
mezczyzna(pawel).
kobieta(ania).
kobieta(kasia).

przyjazn(X, Y) :-
    lubi(X, Y),
    lubi(Y,X).

nieprzyjazn(X, Y) :-
    \+ (lubi(X, Y)),
    \+ (lubi(Y, X)).
       
niby_przyjazn(X, Y) :-
    lubi(X,Y);
    lubi(Y,X).

loves(X, Y) :-
    przyjazn(X, Y),
    \+ (lubi(X, Z), Z \= Y),
    \+ (lubi(Y, W), W \= X).

true_love(X, Y) :-
    loves(X, Y),
    mezczyzna(X) \= mezczyzna(Y).
```
    
