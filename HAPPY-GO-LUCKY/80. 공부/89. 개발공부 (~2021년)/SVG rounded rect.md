---
tags:
  - Svg
Created: Invalid date
Updated: Invalid date
---
$scope.rounded_rect = **function** (x, y, w, h, r, tl, tr, bl, br) {  
    **var** retval;  
    retval  = **"M"** + (x + r) + **","** + y;  
    retval += **"h"** + (w - 2*r);  
    **if** (tr) { retval += **"a"** + r + **","** + r + **" 0 0 1 "** + r + **","** + r; }  
    **else** { retval += **"h"** + r; retval += **"v"** + r; }  
    retval += **"v"** + (h - 2*r);  
    **if** (br) { retval += **"a"** + r + **","** + r + **" 0 0 1 "** + -r + **","** + r; }  
    **else** { retval += **"v"** + r; retval += **"h"** + -r; }  
    retval += **"h"** + (2*r - w);  
    **if** (bl) { retval += **"a"** + r + **","** + r + **" 0 0 1 "** + -r + **","** + -r; }  
    **else** { retval += **"h"** + -r; retval += **"v"** + -r; }  
    retval += **"v"** + (2*r - h);  
    **if** (tl) { retval += **"a"** + r + **","** + r + **" 0 0 1 "** + r + **","** + -r; }  
    **else** { retval += **"v"** + -r; retval += **"h"** + r; }  
    retval += **"z"**;  
    **return** retval;  
};