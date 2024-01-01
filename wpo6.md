# hs 4
## Oefening 9

```scheme
#lang r7rs

(import (scheme base)
        (scheme write)
        (prefix (a-d heap standard) h:))

;h4

;oefening 9
;greatest = root: <
;greatest = end of vector: >

;oefening 8
;(vector 25 2 17 20  84 5 7 12) <
;(2 12 5 20 84 17 7 25)
;parent index 12
;root
;leaves only left = midde element
;height log2(size)



(display (h:from-scheme-vector (vector 25 2 17 20 84 5 7 12) <))
```