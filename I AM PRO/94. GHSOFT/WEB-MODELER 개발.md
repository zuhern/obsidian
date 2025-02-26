---
Created: Invalid date
Updated: Invalid date
---
print 할 때 요소 중에 text가 다른 text로 프린트가 되는 경우

@media print {

body:before {

/* content: 'JointJS : Business Process Model and Notation'; */

font-size: 6mm;

}

.joint-halo, .joint-free-transform {

display: none !important;

}

}