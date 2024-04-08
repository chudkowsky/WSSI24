## Zad1.1
### A - X i Y rodzeństwo
### B - X i Y to rodzeństwo cioteczne 
### C - X i Y to dziadkowie wspolnego wnuka
### D - Y jest macochą/ojczymem X
### E - X i Y jest rodzeństwem przyrodnim
### F - Przyjmując, że posiadanie dziecka oznacza ślub to X to szwagier/szwagierka Y 
### G - 
## Zad1.2

## ćwiczenie 
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
    
