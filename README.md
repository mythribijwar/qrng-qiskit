# Quantum Random Number Generator (QRNG)
*Built with Qiskit on Google Colab*

---

## Problem Statment

Python's `random.randint()` is not actually random. It uses a formula called Mersenne Twister — give it the same starting seed, you get the exact same numbers. That means a attacker who knows the seed can predict every "random" number your program generates.

Quantum mechanics— randomness that doesn't come from a formula, but from physics itself.

---




The **Hadamard gate** creates this state mathematically:

```
|0⟩  →  (|0⟩ + |1⟩) / √2
```

This means: take a qubit that is definitely 0, and put it into an equal mix of 0 and 1. The √2 just keeps the total probability at 100%.

When you **measure** this qubit, the superposition collapses — the qubit becomes either 0 or 1 with exactly 50% chance each. Nothing caused that choice. No seed. No formula. This is why quantum randomness is fundamentally different from anything a classical computer can produce.

---

## What we built in Colab

We applied the Hadamard gate to N qubits, measured each one, and collected the results as a bitstring. That bitstring — born from N separate quantum collapse events — is our random number.

```
|0⟩ → [H] → superposition → measure → 1
|0⟩ → [H] → superposition → measure → 0
|0⟩ → [H] → superposition → measure → 1
...
→ random bitstring: 10110010 → random number: 178
```

We ran this on Qiskit's Aer simulator, which accurately simulates quantum behavior locally without needing a real quantum computer.

---

## Quantum gates used

**H (Hadamard)** — puts a qubit into superposition. Core of everything here.

**X (Pauli-X)** — flips the qubit. 0 becomes 1, 1 becomes 0. Quantum version of NOT.

**CNOT** — uses two qubits. If the first is 1, it flips the second. This is how entanglement is created.

**Toffoli** — like CNOT but needs two controllers. Only flips target if both controllers are 1.

The only gate actively doing the work in QRNG is the Hadamard. The rest are included here for context.

---

## Encryption using quantum keys

We used the quantum-generated bits as a One-Time Pad (OTP) key. The idea is simple — XOR your message bits with the key bits:

```
Message : 01001000  (H)
Key     : 11010110  (quantum random)
Result  : 10011110  (ciphertext — meaningless without the key)
```

XOR the ciphertext with the same key again and recover the original message.


---

## Features

- Random bit, bitstring, and integer generation using Hadamard gates
- 128-bit and 256-bit encryption key generation
- One-Time Pad encryption and decryption
- Quantum vs classical randomness distribution comparison
- Circuit diagram visualization

---

## How to run

Open in Google Colab, run the first cell to install dependencies, then run all cells in order.

```bash
pip install qiskit qiskit-aer matplotlib
```

---

## Project structure

```
qrng-qiskit/
├── QRNG_project.ipynb
└── README.md
```

---
