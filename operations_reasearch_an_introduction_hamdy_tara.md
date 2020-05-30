### 2.4.1 glpk solve

```
var x1; # personal
var x2; # car
var x3; # home
var x4; # farm
var x5; # commerical

maximize z: 0.026*x1 + 0.0509*x2 + 0.0864*x3 + 0.06875*x4 + 0.078*x5;

s.t. total:     x1 + x2 + x3 + x4 + x5 <= 12;
s.t. financial: 0.4*x1 + 0.4*x2 + 0.4*x3 - 0.6*x4 - 0.6*x5 <= 0;
s.t. housing:   0.5*x1 + 0.5*x2 - 0.5*x3 <= 0;
s.t. bad_debts: 0.06*x1 + 0.03*x2 - 0.01*x3 + 0.01*x4 - 0.02*x5 <= 0;
s.t. nonnegative: x1 >= 0; 
s.t. nn2:         x2 >= 0;
s.t. nn3:         x3 >= 0;
s.t. nn4:         x4 >= 0; 
s.t. nn5:         x5 >= 0;

end;
```
