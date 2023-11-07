
## 1
cons: (any any -> pair) <br>
car: (pair -> any)<br>
cdr: (pair -> any)<br>
vector-ref: ( number vector -> any)<br>
vector-set!: (number vector any -> void)<br>
member: (any pair -> (pair U #f) )<br>

## 2
map: ((any -> any) pair -> pair)<br>
sum: ((number -> number) (number ->) number number -> number)<br>
compose: ((any -> any) (any -> any) -> (any-> any))<br>


## 6
```scheme
(define (last-of-list l)
  (cond ((null? l) l)
        ((null? (cdr l)) (car l))
        (else (last-of-list (cdr l)))))
(last-of-list '(1 2 3))
```
w-c O(n)<br>
b-c O(n)<br>
a-c O(n)<br>

```scheme
(define (last-of-vector v)
  (vector-ref v (- (vector-length v) 1) ))
(last-of-vector (vector 1 2 3 ))
```
w-c O(1)<br>
b-c O(1)<br>
a-c O(1)<br>

## 7
len list <br>
w-c O(n) <br>
b-c O(n) <br>
a-c O(n) <br>

len vector<br>
w-c O(1)<br>
b-c O(1)<br>
a-c O(1)<br>

## 8
```scheme
(define (all-but-first-n l n)
  (define (iterate current counter)
    (if (or (= counter 0)
            (null? current))
        current
        (iterate (cdr current) (− counter 1))))
  (iterate n l))
```

