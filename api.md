# iteratori

## struttura di un iteratore

ogni iteratore è formato da un `pair` dello stato
e di una funzione che prende come input lo stesso
e che restituisce un `pair` contenente il valore
dell'iterazione e lo stato da usare nell'iterazione
successiva.

esempio di iteratore:
```guile

(define seq
        (cons 0
              (lambda (stato)
                      (cons stato
                            (+ stato 1)))))

```
questo iteratore, leggendolo con `generate`,
restituisce un `pair` contenente il valore attuale
ed un nuovo iteratore da usare nell'iterazione
successiva.
```guile

scheme@(guile-user)> (generate seq)
$2 = (0 1 . #<procedure 582a243dd258 at <unknown port>:5:14 (stato)>)
scheme@(guile-user)> (value $2)
$3 = 0
scheme@(guile-user)> (generate (next $2))
$4 = (1 2 . #<procedure 582a243dd258 at <unknown port>:5:14 (stato)>)
scheme@(guile-user)> (value $4)
$5 = 1
scheme@(guile-user)> (generate (next $4))
$6 = (2 3 . #<procedure 582a243dd258 at <unknown port>:5:14 (stato)>)
scheme@(guile-user)> (value $6)
$7 = 2
scheme@(guile-user)> (generate (next $6))
$8 = (3 4 . #<procedure 582a243dd258 at <unknown port>:5:14 (stato)>)
scheme@(guile-user)> (value $8)
$9 = 3

```
così si può vedere che questo iteratore produce una sequenza crescente di interi
