## Oefening 1

- count
- equal
- vector or pair

## oefening 2
```scheme
(define (_prtln n)(display n) (newline))
(define l (plist:new equal?))

(plist:add-before! l "and")
(plist:add-after! l "me")
(plist:add-before! l "to" (plist:last l))
(plist:add-after! l "goodday" (plist:first l))
(plist:add-before! l "hello")
(plist:add-after! l "world" (plist:first l))

(plist:for-each l (lambda (x) (display (string-append x " "))))
(newline)

(define (count-e l)
  (define res 0)
  (plist:for-each l (lambda (x)
                      (if (match x "e") (set! res (+ 1 res)))))
  res
  )
(_prtln (count-e l))
```

## oefening 3
```scheme
(define (pair-eq? e1 e2)
  (eq? (cdr e1) (cdr e2)))

(define mapped (plist:map l (lambda (x) (cons x (string-length x))) pair-eq?))
(_prtln mapped)
(_prtln (plist:find mapped (cons "s" 7)))
```

## oefening 4
- (define make-list-node cons)
- (define list-node-val car)
- (define list-node-val! set-car!)
- (define list-node-next cdr)
- (define list-node-next! set-cdr!)

### to vector
- (define (make-list-node x1 x2) (vector x1 x2))
- (define (list-node-val v) (vector-ref v 0))
- (define (list-node-val! v) (vector-set! v 0 ))
- (define (list-node-next v) (vector-ref v 1))
- (define (list-node-next! v) (vector-set! v 1))

## oefening 5
```scheme
(define (accumulate plst f)
       (define (loop curr)
          (if (has-next? plst curr)
              (f (peek plst curr)
                 (loop (next plst curr)))
              (peek plst curr)))
      (if (not (empty? plst))
          (loop (first plst))
            -1))

(define z (plist:new equal?))
(define nums (list 1 2 3 4 ))
(for-each (lambda (x) (plist:add-after! z x)) nums)
(_prtln z)
(_prtln (plist:accumulate z +))
```

## oefening 6
```scheme
(define (intersect p1 p2)
  (define n (plist:new eq?))
  (plist:for-each p1 (lambda (x) (if (plist:find p2 x) (plist:add-after! n x))))
  n)

(define zz (plist:new equal?))
(define numss (list 1 2 3 ))
(for-each (lambda (x) (plist:add-after! zz x)) nums)
(_prtln (intersect zz z))
```

## oefening 8
```scheme 
(define (ternary-search slst key)
      (define ==? (equality slst))
      (define <<? (lesser slst))
      (define vect (storage slst))
      (define leng (size slst))
      (let ternary-search
        ((left 0)
         (right (- leng 1))) 
            (let ((mid1 (+ left (quotient (- right left) 3)))
                  (mid2 (- right (quotient (- right left) 3))))
              (cond
                ((< right left) (current! slst -1))
                ((==? (vector-ref vect mid1) key) 
                 (current! slst mid1))
                ((==? (vector-ref vect mid2) key) 
                 (current! slst mid2))
                ((<<? (vector-ref vect mid2) key)
                 (ternary-search (+ mid2 1) right))
                ((<<? key (vector-ref vect mid1))
                 (ternary-search left (- mid1 1)))
                (else
                 (ternary-search (+ mid1 1) (- mid2 1) )))) ) slst)
```