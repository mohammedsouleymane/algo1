## oefening 8
- abracadabra
- hocus-pocus

## oefening 9
- abracadabra
- 10001010123

- h a a h i i h a a h a a h i i
- -1 0 0 0 1 0 0 1 2 3 4 2 3 4 5

## oefening 10
- (string -> (number -> number))

## oefening 11
```scheme
(import (scheme base))
(import (only (scheme write) display write))
(define (compute-failure-function p)
  (define n-p (string-length p))
  (define sigma-table (make-vector n-p 0))
  (let loop
    ((i-p 2)
     (k 0))
    (when (< i-p n-p)
      (cond
        ((eq? (string-ref p k) 
              (string-ref p (- i-p 1)))
         (vector-set! sigma-table i-p (+ k 1))
         (loop (+ i-p 1) (+ k 1)))
        ((> k 0)
         (loop i-p (vector-ref sigma-table k)))
        (else ; k=0
         (vector-set! sigma-table i-p 0)
         (loop (+ i-p 1) k)))))
  (vector-set! sigma-table 0 -1)
  (lambda (q)
    (vector-ref sigma-table q)))
 
(define (show i-p i-t t p)
  (display "---------------------") (newline)
  (for-each display (list "ip: " i-p)) (newline)
  (for-each display (list "it: " i-t)) (newline)
  (display t) (newline)
  (println i-t (substring p 0 (+ 1 i-p))))

(define (display-n n d)
  (cond ((> n 0) (display d)
                 (display-n (- n 1) d))))
 
(define (println aantalblanco tekst)
  (display-n aantalblanco " ")
  (display tekst)
  (newline))
(define (match t p)
  (define n-t (string-length t))
  (define n-p (string-length p))
  (define sigma (compute-failure-function p))
  (let loop
    ((i-t 0)
     (i-p 0)) 
    (cond 
      ((> i-p (- n-p 1))
       i-t)
      ((> i-t (- n-t n-p))
       #f)
      ((eq? (string-ref t (+ i-t i-p)) (string-ref p i-p))
       (begin (show i-p i-t t p)
              (loop i-t (+ i-p 1))))
      (else
       (show i-p i-t p t)
       (loop (+ i-t (- i-p (sigma i-p))) (if (> i-p 0)
                                             (sigma i-p)
                                             0))))))

(match "ABC ABCDAB ABCDABCDABDE" "ABCDABD")
```

## oefening 12
- stepping
- 87654321

- min-ascii 101 -> e
- max-ascii 116 -> t
- efghijklmnopqrst
- 6919399992949987
-           5

