# hs 4
## imports
```scheme
(import (scheme base)
        (scheme write)
        (prefix (a-d stack linked) s:)
        (prefix (a-d queue list) q:)
        (prefix (a-d queue linked) lq:))
(define (prtln t) (display t) (newline))
```
## oefening 1

```scheme
;oefening 1
(define (pop-all s)
  (if (not (s:empty? s))
      (cons (s:pop! s) (pop-all s)) '()))

(define (postfix-eval expr)
  (define s (s:new))
  (let loop ((l  expr))
    (cond ((null? l) (s:pop! s))
          ((number? (car l)) (begin (s:push! s (car l))
                                    (loop (cdr l))))
          ((procedure? (car l)) (begin (s:push! s  (apply (car l) (reverse (pop-all s))))
                                       (loop (cdr l)))))))

(prtln (postfix-eval (list 1 2 +)))
(prtln (postfix-eval (list 5 6 + 7 -)))                                      
```
## oefening 2
```scheme
(define (closing-tag? symbol)
  (define s (symbol->string symbol))
  (and (equal? (substring s 0 2) "</")
       (equal? (string-ref s (- (string-length s) 1)) #\>)))

(define (matches? symbol-a symbol-b)
  (define s-a (symbol->string symbol-a))
  (define s-b (symbol->string symbol-b))
  (and (opening-tag? symbol-a)
       (closing-tag? symbol-b)
       (equal? (substring s-a 1 (- (string-length s-a) 1))
               (substring s-b 2 (- (string-length s-b) 1)))))

(define (opening-tag? symbol)
  (define s (symbol->string symbol))
  (and (equal? (string-ref s 0) #\<)
       (not (equal? (string-ref s 1) #\/))
       (equal? (string-ref s (- (string-length s) 1)) #\>)))


(define (valid? doc)
  (define stack (s:new))
  (let loop ((current doc))
    (if (null? current)
        (s:empty? stack)
        (let ((element (car current)))
          (cond ((opening-tag? element)
                 (begin (s:push! stack element)
                        (loop (cdr current))))
                ((closing-tag? (car current))
                 (and (matches? (s:pop! stack) element)
                      (loop (cdr current))))
                (else (loop (cdr current))))))))


(prtln (valid? '(<html> <head> This is the head
                        </head> <body> And this is the body </body> </html>)))

(prtln (valid? '(<html> <head> <title> Document </title> </head> <body> </body> </html>)))
```

## oefening 3
```scheme
(define (enqueue-all queue)
  (if (q:empty? queue) '()
      (cons (q:serve! queue)
            (enqueue-all queue))))


(define (josephus lst m)
  (define queue (q:new))
  (define last '())
  (for-each (lambda (x) (q:enqueue! queue x)) lst)

  (let loop ( (c 1))
    (cond
      ((q:empty? queue) last)
      ((= c m) (set! last (q:serve! queue)) (loop 1))
      (else (set! last (q:serve! queue))
            (q:enqueue! queue last)
            (loop (+ 1 c))))))

(prtln (josephus '(a b c d e) 3))
(prtln (josephus '(1 2 3 4 5) 3))
```