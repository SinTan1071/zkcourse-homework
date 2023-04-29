# 第2课 课后作业

## 第1题 转换为bit位 Num2Bits

```
pragma circom 2.1.4;

  template Num2Bits(nBits) {
      signal input in;
      signal output b[nBits];
    
      var acc;
      for (var i = 0; i < nBits; i++){
          b[i] <== ( in \ 2 ** i ) % 2
          0 === b[i] * ( 1 - b[i] );
          acc += b[i] * ( 2 ** i);
      }

      in === acc;

  }

  template Main(){
      signal input in;
      signal output o;

      component n2b = Num2Bits(5);
      n2b.in <== in;
      o <== n2b.b[2];
  }

  /* INPUT = {
      "in": "11"
  } */
```

## 第2题 判零 IsZero

```
pragma circom 2.1.4;

template IsZero () {
    signal input in;
    signal output out;
    signal inv;
    
    inv <-- in == 0 ? 0 : 1/in; 
    out <== -in * inv + 1;
    in * out === 0;
}

component main = IsZero();

/* INPUT = {
    "in": "0"
} */
```

## 第3题 相等 IsEqual

```
pragma circom 2.1.4;

template IsZero () {
    signal input in;
    signal output out;

    signal inv;
    inv <-- in == 0 ? 0: 1/ in;

    out  <== - in * inv + 1;
    in * out === 0;
}

template IsEqual () {
    signal input in[2];
    signal output equal;

    component isZero = IsZero();
    isZero.in <== -in[0] + in[1];
    equal <== isZero.out;
}

component main = IsEqual ();

/* INPUT = {
    "in": ["4", "4"],
    "out": "1"
} */
```

## 第4题 选择器 Selector

```
pragma circom 2.1.4;

template Selector(nChoices) {
    signal input in[nChoices];
    signal input index;
    signal output out;

    component isEqual[nChoices];
    var sum = 0;
    signal internalValues[nChoices];
    for(var i = 0; i < nChoices; i++) {
        isEqual[i] = IsEqual();
        isEqual[i].in[0] <== i;
        isEqual[i].in[1] <== index;
        internalValues[i] <== isEqual[i].out * in[i];
        sum += internalValues[i];
    }

    out <== sum;
}

component main = Selector(6);

/* INPUT = {
    "in": ["0", "1", "2", "3", "4", "5"],
    "index": "6"
} */
```

## 第5题 判负 IsNegative

```
pragma circom 2.1.4;

template Num2Bits(n) {
    signal input in;
    signal output out[n];
    var lc1=0;

    var e2=1;
    for (var i = 0; i<n; i++) {
        out[i] <-- (in >> i) & 1;
        out[i] * (out[i] -1 ) === 0;
        lc1 += out[i] * e2;
        e2 = e2+e2;
    }

    lc1 === in;
}


// Returns 1 if in (in binary) > ct
template CompConstant(ct) {
    signal input in[254];
    signal output out;

    signal parts[127];
    signal sout;

    var clsb;
    var cmsb;
    var slsb;
    var smsb;

    var sum=0;

    var b = (1 << 128) -1;
    var a = 1;
    var e = 1;
    var i;

    for (i=0;i<127; i++) {
        clsb = (ct >> (i*2)) & 1;
        cmsb = (ct >> (i*2+1)) & 1;
        slsb = in[i*2];
        smsb = in[i*2+1];

        if ((cmsb==0)&&(clsb==0)) {
            parts[i] <== -b*smsb*slsb + b*smsb + b*slsb;
        } else if ((cmsb==0)&&(clsb==1)) {
            parts[i] <== a*smsb*slsb - a*slsb + b*smsb - a*smsb + a;
        } else if ((cmsb==1)&&(clsb==0)) {
            parts[i] <== b*smsb*slsb - a*smsb + a;
        } else {
            parts[i] <== -a*smsb*slsb + a;
        }

        sum = sum + parts[i];

        b = b -e;
        a = a +e;
        e = e*2;
    }

    sout <== sum;

    component num2bits = Num2Bits(135);

    num2bits.in <== sout;

    out <== num2bits.out[127];
}


template IsNegative() {
    signal input in;
    signal output out;

    var p = 21888242871839275222246405745257275088548364400416034343698204186575808495617;
    // (p - 1) \ 2 = 10944121435919637611123202872628637544274182200208017171849102093287904247808
    component num2bits = Num2Bits(254);
    component compconstant = CompConstant((p - 1) \ 2);
    num2bits.in <== in;
    compconstant.in <== num2bits.out; 
    out <== compconstant.out;

}

component main = IsNegative(); 

/* INPUT = {
    "in": "21888242871839275222246405745257275088548364400416034343698204186575808495616"
} */
```

## 第6题 少于 LessThan

```
pragma circom 2.1.4;

template LessThan(k) {
    signal input in[2];
    signal output out;
    assert(k <= 252);

    // use internal Num2Bits template
    component n2b = Num2Bits(k + 1);
    n2b.in <== (1 << k) + in[1] - in[0];
    out <== n2b.b[k]; 
}

component main = LessThan(3);

/* INPUT = {
    "in": ["1", "2"]
} */
```

## 第7题 整数除法 IntegerDivide

```
TODO
```
