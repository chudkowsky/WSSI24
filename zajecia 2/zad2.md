:- set_prolog_flag(occurs_check, error).        % disallow cyclic terms
:- set_prolog_stack(global, limit(8 000 000)).  % limit term space (8Mb)
:- set_prolog_stack(local,  limit(2 000 000)).  % limit environment space

rodzic(pawel, kasia).
rodzic(pawel, jan).
 
rodzic(joanna, kasia).
rodzic(joanna, jan).

rodzic(kasia,ania).
rodzic(jan, basia).

mezczyzna(jan).
mezczyzna(pawel).
mezczyzna(tomek).

kobieta(X) :-
	\+ (mezczyzna(X)).
ojciec(X, Y) :- 
    rodzic(X, Y),
    mezczyzna(X).

matka(X, Y) :-
    rodzic(X, Y),
    kobieta(X).
corka(X,Y) :-
    rodzic(Y,X),
    kobieta(X).

siostra_rodzona(X, Y) :-
    ojciec(T, X),
    ojciec(T, Y),
    matka(M, X),
    matka(M, Y),
    X \= Y,               
    X \= T,
    Y \= T,
    Y \= M,
	X \= M,
    M \= T.

brat_rodzony(X, Y) :-
    ojciec(T, X),
    ojciec(T, Y),
    matka(M, X),
    matka(M, Y),
    X \= Y,               
    X \= T,
    Y \= T,
    Y \= M,
	X \= M,
    mezczyzna(X).

brat_przyrodni(X, Y) :-
    rodzic(Z, X),         
    rodzic(Z, Y),         
    mezczyzna(X),         
    X \= Y.           

kuzyn(X, Y) :- 
    rodzic(Z, X),
    rodzic(W, Y),
    (brat_rodzony(Z, W);siostra_rodzona(Z,W)).

dziadek_od_strony_ojca(X,Y) :-
    ojciec(X,Z),
    ojciec(Z,Y),
    X\=Y,
	Z\=Y,
	X\=Z.
dziadek_od_strony_matki(X,Y) :-
    ojciec(X,Z),
    matka(Z,Y),
    X\=Y,
	Z\=Y,
	X\=Z.
dziadek(X,Y):-
    ojciec(X,Z),
    rodzic(Z,Y),
    X\=Y,
	Z\=Y,
	X\=Z.
pradziadek(X,Y):-
    ojciec(X,Z),
   	dziadek(Z,Y),
    X\=Y,
	Z\=Y,
	X\=Z.
babcia(X,Y) :-
    matka(X,Z),
    rodzic(Z,Y),
    X\=Y,
	Z\=Y,
	X\=Z.
prababcia(X,Y):-
	matka(X,Z),
   	dziadek(Z,Y),
    X\=Y,
	Z\=Y,
	X\=Z.

wnuczka(X,Y) :-
    babcia(Y,X),
    kobieta(X).
przodek_do2pokolenia_wstecz(X,Y) :-
    dziadek(X,Y);babcia(X,Y);
    ojciec(X,Y);matka(X,Y).

przodek_do3pokolenia_wstecz(X,Y) :-
    pradziadek(X,Y);prababcia(X,Y);
    dziadek(X,Y);babcia(X,Y);
    ojciec(X,Y);matka(X,Y).
                         
