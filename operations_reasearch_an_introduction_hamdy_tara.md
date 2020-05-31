### 2.4.1 glpk solve

```2.4.1.mod
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

### 2.4.2 glpk solve

```2.4.2.mod
var x1; # parka
var x2; # goose
var x3; # pants
var x4; # gloves

var s1; # parke lack
var s2; # goose lack
var s3; # pants lack
var s4; # gloves lack

maximize z: 30*x1 + 40*x2 + 20*x3 + 10*x4 - (15*s1 + 20*s2 + 10*s3 + 8*s4);

s.t. cutting   : 0.3*x1 + 0.3*x2 + 0.25*x3 + 0.15*x4 <= 1000;
s.t. insulating: 0.25*x1 + 0.35*x2 + 0.3*x3 + 0.1*x4 <= 1000;
s.t. sewing    : 0.45*x1 + 0.5*x2 + 0.4*x3 + 0.22*x4 <= 1000;
s.t. packaging : 0.15*x1 + 0.15*x2 + 0.1*x3 + 0.05*x4 <= 1000;

s.t. parka : x1 + s1 = 800;
s.t. goose : x2 + s2 = 750;
s.t. pants : x3 + s3 = 600;
s.t. gloves: x4 + s4 = 500;

s.t. nn1: x1 >= 0;
s.t. nn2: x2 >= 0;
s.t. nn3: x3 >= 0;
s.t. nn4: x4 >= 0;

s.t. nn5: s1 >= 0;
s.t. nn6: s2 >= 0;
s.t. nn7: s3 >= 0;
s.t. nn8: s4 >= 0;

end;                                                                     
```

幸好四个值只有一个是非整数，此数取floor值即可。
