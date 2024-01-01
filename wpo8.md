# hs5

## imports
```scheme 
(import (scheme base)
        (scheme write))

(define (println t) (display t)(newline))
```

## oefening 1
```scheme
(define (bubble-sort l compare)
  (define len (length l))
  (define nlen len)
  (define (swap lst e1 e2)
    (set-car! lst e2)
    (set-car! (cdr lst) e1))
  (let loop ((lst l)
             (swapped #f))
    (cond ((= len 0) l)
          ((null? (cdr lst)) (set! len (- len 1)) (loop l #f))
          ((compare (car lst) (cadr lst)) (swap lst (car lst) (cadr lst))
                                          (loop (cdr lst) #t))
          ((not (= nlen len)) (set! nlen len) (loop l #f))
          (else (loop (cdr lst) swapped)))))


(println "oefening 1")
(println (bubble-sort '(3 2 2 5 1 0) <) )
(println (bubble-sort '(3 2 2 5 1 0) >) )
```

## oefenning 2
```scheme
(define (insertion-sort vector <<?)
  (define (>=? x y) (not (<<? x y)))
  (let outer-loop
    ((outer-idx 1))
    (let
        ((current (vector-ref vector outer-idx)))
      (vector-set!
       vector
       (let inner-loop
         ((inner-idx (- outer-idx 1)))
         (cond
           ((or (<= inner-idx -1)
                (>=? current
                     (vector-ref vector inner-idx)))
            (+ inner-idx 1))
           (else
            (vector-set! vector (+ inner-idx 1) (vector-ref vector inner-idx))
            (inner-loop (- inner-idx 1)))))
       current)
      (if (< outer-idx  (- (vector-length vector) 1))
          (outer-loop (+ outer-idx 1))))))

(define t (vector 4 5 8 2 5 1))
(insertion-sort t >)
(println "oefening 2")
(println t)
```

## oefening 4
```scheme
(define (selection-sort vector <<?)
  (define index-vec (make-vector (vector-length vector) 0))

  (define (swap vector i j)
    (let ((keep (vector-ref vector i)))
      (vector-set! vector i (vector-ref vector j))
      (vector-set! vector j keep)))

  (let loop((i 0))
    (vector-set! index-vec i i)
    (if (< i (- (vector-length vector) 1 )) (loop (+ i 1))))

  (let outer-loop
    ((outer-idx 0))
    (swap
     index-vec
     outer-idx
     (let inner-loop
       ((inner-idx (+ outer-idx 1))
        (smallest-idx outer-idx))
       (cond
         ((>= inner-idx (vector-length vector))
          smallest-idx)
         ((<<? (vector-ref vector (vector-ref index-vec inner-idx))
               (vector-ref vector  (vector-ref index-vec smallest-idx)))
          (inner-loop (+ inner-idx 1) inner-idx))
         (else
          (inner-loop (+ inner-idx 1) smallest-idx)))))
    (if (< outer-idx (- (vector-length vector) 1))
        (outer-loop (+ outer-idx 1))))
  index-vec)
(println "oefening 4")
(define v (vector 5 6 2 1 3))
(println (selection-sort v  <))
(println v)
```

## oefening 9
```scheme
(define (merge-sort lst <<?)
  (define (split lst)
    (define l (length lst))
    (define (iter c left right)
      (if (< c (/ l 2))
          (iter (+ c 1)
                (cons (car right) left)
                (cdr right))
          (cons left right)) )
    (iter 0 '() lst))
  (define (merge l r)
    (cond ((null? l) r)
          ((null? r) l)
          ((<<? (car l) (car r)) (cons (car l) (merge (cdr l) r)))
          (else (cons (car r) (merge l (cdr r))))))

  (define (merge-sort-rec lst)
    (if ( > (length lst) 1)
        (let* ((s (split lst))
               (left (merge-sort-rec (car s)))
               (right (merge-sort-rec (cdr s))))
          (merge left right))
        lst))

  (merge-sort-rec lst))
(println "oefening 9")
(println (merge-sort '( 5 3 8 1 8 0 9) <))
```