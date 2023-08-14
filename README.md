# Implementation of Logical Operations in a Polygon zkSNARK Circuit

## Overview:
Welcome to the GitHub repository dedicated to the implementation of a Polygon zkSNARK Circuit focusing on logical operations. This project aims to create and deploy a Zero-Knowledge Succinct Non-Interactive Argument of Knowledge (zkSNARK) circuit on the Polygon blockchain network. This custom circuit will incorporate a logical gate to enable secure and privacy-preserving computations.

The primary goal of this repository is to develop the circuit using the circom programming language, which is renowned for its efficiency and adaptability in zkSNARK circuit design. The logical gate integrated within the circuit will empower users to perform confidential operations while keeping their sensitive inputs concealed from public observation.

## Getting Started

### Setup

To engage with this project, you should adhere to these steps:

1. Download the Circom programming language from the official website: [Circom](https://www.circom.io/).
2. Install Circom on your system by following the instructions provided in the documentation.

### Running the Program

To execute the circuit, adhere to these instructions:

1. Launch your terminal or command prompt and navigate to the designated project directory.
2. Compile the circuit by executing the subsequent command:

```bash
npm install
```

3. Upon a successful installation, proceed to compile the circuit:

```bash
npx hardhat circom
```

4. Deployment: The circuit is being deployed on the Polygon Mumbai testnet; however, you can opt for any other suitable testnet:

```bash
npx hardhat run scripts/deploy.ts --network mumbai
```

## Circuit Logic

The circuit logic is established using Circom and comprises three templates for fundamental logic gates: AND, OR, and NOT. The pivotal customized circuit named 'LooseCircuit' is constructed using these gate templates.

### AND Gate

The AND gate template takes two input signals, 'a' and 'b,' generating an output signal 'out' that symbolizes the logical AND operation between 'a' and 'b.'

```circom
template AND() {
    signal input a;
    signal input b;
    signal output out;

    out <== a * b;
}
```

### OR Gate

The OR gate template accepts two input signals, 'a' and 'b,' and generates an output signal 'out' representing the logical OR operation between 'a' and 'b.'

```circom
template OR() {
    signal input a;
    signal input b;
    signal output out;

    out <== a + b - a * b;
}
```

### NOT Gate

The NOT gate template takes an input signal 'in' and produces an output signal 'out' signifying the logical NOT operation applied to 'in.'

```circom
template NOT() {
    signal input in;
    signal output out;

    out <== 1 + in - 2 * in;
}
```

### Custom Circuit - Multiplier2

The primary customized circuit, 'Multiplier2,' leverages the AND, NOT, and OR gates to actualize the logic for multiplying input values 'a' and 'b,' ultimately generating the output 'q.'

```circom
pragma circom 2.0.0;

/* This circuit template verifies that 'c' results from the multiplication of 'a' and 'b'. */

template Multiplier2 () {

    // Input signals 'a' and 'b'
    signal input a;
    signal input b;

    // Signals from the gates
    signal x;
    signal y;

    // Final output signal 'q'
    signal output q;

    // Components utilized in the circuit
    component andGate = AND();
    component orGate = OR();
    component notGate = NOT();

    // Circuit logic

    andGate.a <== a;
    andGate.b <== b;
    x <== andGate.out;

    notGate.in <== b;
    y <== notGate.out;

    orGate.a <== x;
    orGate.b <== y;
    q <== orGate.out;
}

// Below are the templates of the gates utilized in the circuit logic

template AND() {
    signal input a;
    signal input b;
    signal output out;

    out <== a * b;
}

template OR() {
    signal input a;
    signal input b;
    signal output out;

    out <== a + b - a * b;
}

template NOT() {
    signal input in;
    signal output out;

    out <== 1 + in - 2 * in;
}

component main = Multiplier2();
```

Following the installation and execution steps will culminate in the successful implementation of the circuit, ultimately yielding the desired output 'q' based on the provided 'a' and 'b' inputs.

## Assistance
If you encounter any challenges or have inquiries regarding the program, consult the official Circom documentation or seek assistance from the community.

# Author
[Sutirtho Chakravorty](somanshusharma888@gmail.com)

License
This project is licensed under the MIT License.
