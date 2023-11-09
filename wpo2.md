
## oefening 3
```scheme
#lang r7rs
(define-library
  (fraction)
  (export new numer denom fraction? + - / *)
  (import (prefix (scheme write) io:)
          (rename (scheme base)
                  (+ b:+)
                  (- b:-)
                  (/ b:/)
                  (* b:*))
          (scheme cxr))
  (begin
    (define tag 'fraction)
    (define (new n d)
      (define gg (gcd n d))
      (list tag (b:/ n gg) (b:/ d gg)))
    (define (numer f) (cadr f))
    (define (denom f) (caddr f))
    (define (fraction? v)
      (if (pair? v) (eq? (car v) tag) #f))
    (define (+ f1 f2)
      (new (b:+ (b:* (numer f1) (denom f2)) (b:* (numer f2) (denom f1)))
           (b:* (denom f1) (denom f2))))

    (define (- f1 f2)
      (new (b:- (b:* (numer f1) (denom f2)) (b:* (numer f2) (denom f1)))
           (b:* (denom f1) (denom f2))))
    (define (/ f1 f2)
      (new  (b:* (numer f1) (denom f2)) (b:* (numer f2) (denom f1))))
    
    (define (* f1 f2)
      (new  (b:* (numer f1) (numer f2)) (b:* (denom f2) (denom f1))))))

;implementation
#lang r7rs
(import (scheme base)
        (prefix (wpo2 fraction) fraction:))

(define (fraction:= f1 f2)
  (and (= (fraction:numer f1) (fraction:numer f2)) (= (fraction:denom f1) (fraction:denom f2))))
```

## oefening 5
* Dic<string,string>
* Dic<string,pair>
* Dic<string,number>
* Dic<string,boolean>
* Dic<student,Dic<string, number>>

## oefening 9
* A procedure to compute n - m:
```scheme
(define (subtract n m)
  (if (= m 0)
      n
      (subtract (- n 1) (- m 1))))      
```
w-c O(m)

* A procedure that zips two lists in a pairwise fashion:
```scheme
(define (zip l1 l2)
  (if (or (null? l1) (null? l2))
      '()
      (cons (cons (car l1)
                  (car l2))
            (zip (cdr l1) (cdr l2)))))
```
n=len(l1) m=len(l2) <br>
w-c O((min)(n , m))


## oefening 10
```scheme
(define (all-i-to-j n)
  ;O(j)
  (define (i-to-j i j)
    (if (= j 0)
        1
        (* i (i-to-j i (- j 1)))))
  ;O(i) * O(i)
  (define (sum i)
    (if (= i 0)
        0                  ;O(i)
        (+ (sum (- i 1)) (i-to-j i i))))
  (sum n))
; 5 4 3 2 1 
; 4 3 2 1 
; 3 2 1 
; 2 1 
; 1
``` 
w-c O((n^2+n)/2) -> O(n^2)