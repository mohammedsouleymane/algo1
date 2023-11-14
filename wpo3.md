#lang r7rs


(import (scheme base)
        (scheme read)
        (scheme write)
        )

## oefening 1
- char->integer
- 48 to 57
- 97 to 122
- 65 to 90

## oefening 2
```scheme
(define (string->number str)
  (define l (string-length str))
  (define (loop i nm)
    (if (< i l) (loop (+ i 1)
                      (+ (* 10 nm)
                         ( - (char->integer (string-ref str i)) 48))) nm))
  (loop 0 0))
;(display (string->number "1234"))
;b-c O(n)
```

## oefening 3
- v is a prefix of t
- w is a suffix of t
- the length of w is 3 this is also denoted as |w| = 3
- Is v a proper prefix of t? Yes v is not equal to the string itself and not empty.

## oefening 4
### prefixes
- Hello
* proper prefixes
  - Hell
  - Hel
  - He
  - H

### suffixes
- hello
- proper suffixes
  - ello
  - llo
  - lo
  - o

## oefening 5
```scheme
(define (match t p)
  (define n-t (string-length t))
  (define n-p (string-length p))
  (let loop
    ((i-t 0)
     (i-p 0))
    (cond
      ((> i-p (- n-p 1))
       i-t)
      ((> i-t (- n-t n-p))
       #f)
      ((eq? (string-ref t (+ i-t i-p)) (string-ref p i-p))
       (loop i-t (+ i-p 1)))
      (else
       (loop (+ i-t 1) 0)))))
```
## oefening 6
```scheme
(define (match-multple t p)
  (define n-t (string-length t))
  (define n-p (string-length p))
  (let loop
    ((i-t 0)
     (i-p 0))
    (cond
      ((> i-p (- n-p 1))
       (cons i-t (loop ( + 1 i-t) 0)))
      ((> i-t (- n-t n-p))
       '())
      ((eq? (string-ref t (+ i-t i-p)) (string-ref p i-p))
       (loop i-t (+ i-p 1)))
      (else
       (loop (+ i-t 1) 0)))))
```

## oefening 7
```scheme
(define (match-holes t p i)
  (define n-t (string-length t))
  (if (not (null? p))
      (let loop
        ((i-t i)
         (i-p 0)
         (n-p (string-length (car p))))
        (cond ((> i-p (- n-p 1)) (and (match-holes t (cdr p) i-t) i-t))
              ((> i-t (- n-t n-p)) #f)
              ((eq? (string-ref t (+ i-t i-p)) (string-ref (car p) i-p))
               (loop i-t (+ i-p 1) n-p))
              (else (loop (+ i-t 1) 0 n-p))))))

(display (match-holes "012345678" (list "12" "45" "98") 0))
(newline)
(display (match-holes "012345678" (list "12" "45" "8") 0))
```
