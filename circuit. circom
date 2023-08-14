pragma circom 2.0.0;

/*This circuit template checks that c is the multiplication of a and b.*/  

template Multiplier2 () {  

    // signal inputs A and b
    signal input a;
    signal input b;
    

    // Signals from the gates 
    signal x;
    signal y;


    // final signal output 
    signal output q;


    // The components which we will be using 

    component andGate = AND();  
    component orGate = OR();  
    component notGate = NOT(); 

    //circuit logic


    
    andGate.a <== a;
    andGate.b <== b;

    x <== andGate.out;


    

    notGate.in <== b;

    y <== notGate.out;


    

    orGate.a <== x;
    orGate.b <== y;

    q <== orGate.out;




}


// Below are the templates of the gates i will be using in my circuit logic 

template AND() {
    signal input a;
    signal input b;
    signal output out;

    out <== a*b;

    
}

template OR() {
    signal input a;
    signal input b;
    signal output out;

    out <== a + b - a*b;
}

template NOT() {
    signal input in;
    signal output out;

    out <== 1 + in - 2*in;
}

component main = Multiplier2();
