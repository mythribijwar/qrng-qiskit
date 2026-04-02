# Quantum Random Number Generator (QRNG)
*Built with Qiskit on Google Colab*

---

## Why I built this

Python's `random.randint()` is not actually random. It uses a formula called Mersenne Twister — give it the same starting seed, you get the exact same numbers. That means a smart attacker who knows the seed can predict every "random" number your program generates.

Quantum mechanics gives us something genuinely different — randomness that doesn't come from a formula, but from physics itself.

---

## The physics behind it

A normal bit is like a coin already lying on a table. It's heads or tails — fixed, decided.

A qubit is like a coin spinning in the air. It is not heads *or* tails yet. It is genuinely both at the same time. This is called **superposition**, and it's not a metaphor — it's how quantum particles actually behave.

The **Hadamard gate** creates this state mathematically:

```
|0⟩  →  (|0⟩ + |1⟩) / √2
```

This means: take a qubit that is definitely 0, and put it into an equal mix of 0 and 1. The √2 just keeps the total probability at 100%.

When you **measure** this qubit, the superposition collapses — the qubit becomes either 0 or 1 with exactly 50% chance each. Nothing caused that choice. No seed. No formula. The universe just picked. This is why quantum randomness is fundamentally different from anything a classical computer can produce.

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

XOR the ciphertext with the same key again and you recover the original message. That's decryption.

Claude Shannon proved in 1949 that OTP is mathematically unbreakable — as long as the key is truly random and used only once. Classical PRNGs don't qualify. Quantum measurement does.

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
