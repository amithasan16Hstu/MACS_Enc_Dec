<p align="center">
  <img src="HSTU.png" alt="HSTU Logo" width="250" height="300">
</p>
<h1 align="center">
  <b> The PrimeX Cipher: A Modular Arithmetic and Permutation-Based Symmetric Encryption Algorithm for Educational Use
</b>
</h1>
<h3 align="center">
  <br>
  <b>Level-3 Semester-II Proposed Algorithm Report</b>  
</h3>
<h3 align="center">
  Course Code: CSE 361
  Course Title: Mathematical Analysis for Computer Science 
</h3>
<br>
<h3 align="center">
  Submitted by 
</h3>
<h3 align="center">
<b>Amit Hasan Sikder (ID: 2102043) </b> </h3>
<br>

<h3 align="center">
  Submitted To 
</h3>

<h3 align="center"><b>Pankaj Bhowmik  </b></h3>
<h3 align="center"><b>Lecturer, Department of CSE</b></h3>
<br>
<h3 align="center"> <b>Department of Computer Science and Engineering </b></h3>
<h3 align="center"><b>Hajee Mohammad Danesh Science and Technology University  
Dinajpur-5200</b></h3>

---


## Abstract

This paper presents the **PrimeX Cipher**, a custom-designed symmetric encryption algorithm that integrates fundamental concepts of modular arithmetic and block permutation to securely encrypt textual data. Developed with educational clarity and computational simplicity in mind, PrimeX demonstrates core cryptographic principles including substitution, permutation, and key-dependent transformations. The cipher utilizes a user-defined prime number and permutation array as its key, applying modular shifts and rearrangements to achieve reversible encryption and decryption. This work details the algorithm’s design, mathematical underpinnings, and implementation methodology, followed by a discussion of its security features and potential applications in teaching computer security concepts. PrimeX offers a practical platform for understanding the mechanics behind symmetric ciphers and the role of number theory in cryptography.

---


## 📑 Table of Contents

- [1. Introduction](#1-introduction)
- [2. Background and Motivation](#2-background-and-motivation)
- [3. Algorithm Overview](#3-algorithm-overview)
  - [3.1 Key Components](#31-key-components)
  - [3.2 Data Representation](#32-data-representation)
  - [3.3 Encryption Process](#33-encryption-process)
    - [3.3.1 Modular Shift (Substitution)](#331-modular-shift-substitution)
    - [3.3.2 Permutation](#332-permutation)
    - [3.3.3 Modular Multiplication](#333-modular-multiplication)
  - [3.4 Decryption Process](#34-decryption-process)
    - [3.4.1 Modular Multiplication Inverse](#341-modular-multiplication-inverse)
    - [3.4.2 Inverse Permutation](#342-inverse-permutation)
    - [3.4.3 Modular Subtraction](#343-modular-subtraction)
- [4. Mathematical Foundations](#4-mathematical-foundations)
  - [4.1 Modular Arithmetic](#41-modular-arithmetic)
  - [4.2 Modular Inverse](#42-modular-inverse)
  - [4.3 Permutations and Their Inverses](#43-permutations-and-their-inverses)
- [5. Implementation Details](#5-implementation-details)
  - [5.1 Key Generation](#51-key-generation)
  - [5.2 Encryption Algorithm (Pseudocode)](#52-encryption-algorithm-pseudocode)
  - [5.3 Decryption Algorithm (Pseudocode)](#53-decryption-algorithm-pseudocode)
- [6. Example](#6-example)
- [7. Security Considerations](#7-security-considerations)
- [8. Educational Value and Applications](#8-educational-value-and-applications)
- [9. Conclusion](#9-conclusion)
- [References](#references)

---
## List of Figures

- [Figure 3.1: PrimeX Cipher – Encryption Flowchart](#fig-encryption)
- [Figure 3.2: PrimeX Cipher – Decryption Flowchart](#fig-decryption)
- [Figure 3.3: Overview of the Encryption and Decryption Process](#fig-overview)




## 1. Introduction

In today’s digital world, securing information has become a paramount concern. Cryptographic algorithms underpin much of the trust and safety mechanisms within communication systems, financial transactions, and data storage. While industry standards such as AES (Advanced Encryption Standard) and RSA dominate practical applications, a foundational understanding of cryptographic principles is crucial for students, researchers, and enthusiasts pursuing computer science and cybersecurity.

The PrimeX Cipher is designed as a lightweight, symmetric encryption algorithm that clearly illustrates the interplay of substitution, permutation, and modular arithmetic — essential building blocks of many cryptographic systems. By combining these mathematical operations in a simple yet effective manner, PrimeX enables learners to explore how plaintext can be transformed securely into ciphertext and reliably reverted, using keys based on prime numbers and permutations.

This paper elaborates on the motivation behind PrimeX, its step-by-step encryption and decryption processes, the mathematical foundations it employs, and its relevance as an educational tool.

https://github.com/user-attachments/assets/3bff6564-0f8f-4471-a97d-f36a084e91c1


---

## 2. Background and Motivation

Cryptographic primitives generally rely on two key concepts: **substitution** and **permutation**. Substitution replaces elements of the plaintext with other elements, typically through key-dependent transformations. Permutation rearranges the elements’ order to obscure patterns.

Modern symmetric ciphers apply these steps multiple times, often in rounds, using complex key schedules and mathematical operations. However, such complexity can obscure understanding when introducing cryptography to beginners.

PrimeX embraces simplicity by implementing:

- **A modular arithmetic–based substitution** using a prime number to shift numeric representations of characters.  
- **A user-defined permutation** that rearranges blocks of data.  
- **Modular multiplication** to further scramble the data, with all operations reversible through the properties of modular inverses and inverse permutations.

This construction preserves core cryptographic concepts and encourages hands-on experimentation with keys and transformations, reinforcing understanding of how mathematical operations ensure security and reversibility.

---

## 3. Algorithm Overview

### 3.1 Key Components

The PrimeX Cipher’s encryption key consists of:

1. **Prime Number (p)**: A user-chosen prime that defines the modulus for arithmetic operations.  
2. **Permutation Array (π)**: A bijective mapping defining how positions of characters in a block are rearranged.

### 3.2 Data Representation

- The plaintext message is first normalized to uppercase alphabetic characters (A–Z), each mapped to an integer from 0 to 25 (A=0, B=1, ..., Z=25).  
- For convenience, the algorithm processes data in fixed-size blocks corresponding to the length of the permutation array.

### 3.3 Encryption Process

For each block of plaintext characters `(x₀, x₁, ..., xₙ₋₁)`:

#### 3.3.1. **Modular Shift (Substitution)**  
   Add the key `k` to each character value:  
   `sᵢ = (xᵢ + k) mod 26`  
   where `k` is derived from the prime `p` (e.g., `k = p mod 26`).

#### 3.3.2. **Permutation**  
   Rearrange the shifted values using a permutation π:  
   `s′[π(i)] = sᵢ`

#### 3.3.3. **Modular Multiplication**  
   Multiply each permuted value by the prime `p`, modulo 26:  
   `cᵢ = (s′ᵢ × p) mod 26`  

The ciphertext block is `(c₀, c₁, ..., cₙ₋₁)`.

<a name="fig-encryption"></a>
<p align="center">
  <img src="https://raw.githubusercontent.com/amithasan16Hstu/MACS_Enc_Dec/main/encryption_flowchart.png" width="400">
</p>
<p align="center"><i>Figure 3.1: PrimeX Cipher – Encryption Flowchart</i></p>


### 3.4 Decryption Process

To recover plaintext, reverse each encryption step:

#### 3.4.1 Modular Multiplication Inverse
Compute the modular inverse of `p`, denoted as `p⁻¹`, such that:  
`p × p⁻¹ ≡ 1 mod 26`  
Then compute:  
`s'_i = (c_i × p⁻¹) mod 26`

#### 3.4.2 Inverse Permutation
Rearrange the values `s'_i` according to the inverse permutation `π⁻¹`:  
`s_i = s'_{π⁻¹(i)}`

#### 3.4.3 Modular Subtraction
Subtract the key `k` from each `s_i`, modulo 26, to recover the original numeric values:  
`x_i = (s_i - k) mod 26`  
Finally, convert each `x_i` back to its corresponding alphabet letter to obtain the original plaintext.

<a name="fig-decryption"></a>
<p align="center">
  <img src="https://raw.githubusercontent.com/amithasan16Hstu/MACS_Enc_Dec/main/Decreption_flowchart.png" width="400">
</p>
<p align="center"><i>Figure 3.2: PrimeX Cipher – Decryption Flowchart</i></p>


<a name="fig-overview"></a>
<p align="center">
  <img src="https://raw.githubusercontent.com/amithasan16Hstu/MACS_Enc_Dec/main/process.png" width="500">
</p>
<p align="center"><i>Figure 3.3: Overview of the Encryption and Decryption Process</i></p>



---

## 4. Mathematical Foundations

### 4.1 Modular Arithmetic

Modular arithmetic forms the backbone of substitution and multiplication steps, ensuring all operations remain within a finite field defined by modulus 26 (alphabet size). This wrapping behavior prevents overflow and maintains reversibility.

### 4.2 Modular Inverse

The modular inverse `p⁻¹` is essential for decrypting the modular multiplication step. It exists only if `p` and the modulus are coprime — which is guaranteed when `p` is a prime number and shares no common factors with 26.

The **Extended Euclidean Algorithm** efficiently computes `p⁻¹`.

---

### 4.3 Permutations and Their Inverses

The permutation array `π` is a bijection from `{0, ..., n−1}` onto itself, ensuring each index in the block is uniquely mapped.

The inverse permutation `π⁻¹` satisfies:  
`π⁻¹(π(i)) = i`  
This allows for exact reversal of the rearranged positions during decryption.

---

## 5. Implementation Details

### 5.1 Key Generation

1. User inputs a prime number `p` such that `gcd(p, 26) = 1`.  
2. User defines or is provided a permutation array `π` of length `n`.  
3. Compute `k = p mod 26` to use in the modular shift during encryption.
### 5.2 Encryption Algorithm (Pseudocode)

```python
function encrypt(plaintext, p, permutation):
    k = p mod 26
    block_size = length(permutation)
    ciphertext = ""

    for each block in plaintext of size block_size:
        x = map letters to numbers (0–25)
        s = [(x[i] + k) mod 26 for i in range(block_size)]
        s_perm = [0] * block_size
        for i in range(block_size):
            s_perm[permutation[i]] = s[i]
        c = [(s_perm[i] * p) mod 26 for i in range(block_size)]
        ciphertext += map numbers to letters(c)
    return ciphertext
```

---

### 5.3 Decryption Algorithm (Pseudocode)

```python
function decrypt(ciphertext, p, permutation):
    k = p mod 26
    block_size = length(permutation)
    p_inv = modular_inverse(p, 26)
    inv_permutation = inverse_of(permutation)
    plaintext = ""

    for each block in ciphertext of size block_size:
        c = map letters to numbers (0–25)
        s_perm = [(c[i] * p_inv) mod 26 for i in range(block_size)]
        s = [0] * block_size
        for i in range(block_size):
            s[i] = s_perm[inv_permutation[i]]
        x = [(s[i] - k) mod 26 for i in range(block_size)]
        plaintext += map numbers to letters(x)
    return plaintext
```

---

## 6. Example

Consider:
- **p = 5** (a prime)
- Permutation **π = [2, 0, 1]** for block size 3
- Plaintext block: "CAT"

**Mapping letters to numbers:**
- C = 2
- A = 0
- T = 19

**Step 1: Modular shift**  
k = 5 mod 26 = 5  
s = [(2 + 5), (0 + 5), (19 + 5)] mod 26 = [7, 5, 24]

**Step 2: Permutation**  
s = [7, 5, 24]  
Using π = [2, 0, 1]:  
s' = [s[1], s[2], s[0]] = [5, 24, 7]

**Step 3: Modular multiplication by p = 5**  
c = [(5×5), (24×5), (7×5)] mod 26 = [25, 16, 9]

**Mapping back to letters:**  
25 → Z  
16 → Q  
9 → J  

**Ciphertext block:** "ZQJ"

Decryption reverses these steps to recover "CAT".

---

## 7. Security Considerations

While PrimeX is not designed for production use or high-security environments, it incorporates core cryptographic transformations:

- **Key Space:** Wide variety of keys based on prime and permutation, though limited by block size and modulus.
- **Confusion and Diffusion:** Achieved through substitution and permutation.
- **Reversibility:** Guaranteed via modular inverses and bijective permutations.
- **Weaknesses:** Small modulus (26) and fixed block size make it vulnerable to frequency and known-plaintext attacks.

PrimeX is best suited as an educational cipher.

---

## 8. Applications

PrimeX is useful in academic settings for:

- Demonstrating modular arithmetic and inverses.
- Teaching substitution-permutation networks.
- Practicing symmetric encryption principles.
- Developing student coding assignments.
- Comparing with industrial ciphers like AES or DES.

Students can modify keys, permutations, and plaintexts to explore effects on ciphertext.

### 🔐Table 8.1 PrimeX Cipher vs Other Algorithms: Key Differences

| Feature                | **PrimeX Cipher**                                             | **Caesar Cipher**                        | **Vigenère Cipher**                      | **AES (Advanced Encryption Standard)**                |
|------------------------|--------------------------------------------------------------|-------------------------------------------|-------------------------------------------|-------------------------------------------------------|
| **Type**               | Custom, symmetric                                             | Classical, symmetric                      | Classical, polyalphabetic                 | Modern, symmetric block cipher                        |
| **Key Structure**      | Prime number + permutation array                              | Single shift value (integer)              | Keyword (string)                          | 128/192/256-bit key                                   |
| **Substitution Logic** | Modular addition with prime-derived key                       | Simple letter shift                       | Letter shift based on keyword             | Complex S-box substitution                            |
| **Permutation**        | Yes (user-defined permutation array)                          | ❌                                         | ❌                                         | Implicit permutation in rounds                        |
| **Modular Arithmetic** | Core concept: addition & multiplication mod 26                | Addition mod 26                           | Addition mod 26                           | Finite field (GF(2^8)) operations                     |
| **Decryption Needs**   | Modular inverse and inverse permutation                       | Reverse shift                             | Reverse shift by keyword                  | Reverse rounds using inverse functions                |
| **Educational Purpose**| Designed for learning encryption principles                   | Historical interest only                  | Historical, basic cryptography            | Industrial-grade, real-world application              |
| **Security Strength**  | Moderate (for educational use)                                | Very weak                                 | Weak (easy to break)                      | Strong (globally accepted standard)                   |
| **Block-Based?**       | Yes (works on character blocks)                               | No                                        | No                                        | Yes (128-bit blocks)                                  |
| **Customizability**    | High (custom key = prime + permutation)                       | Low                                       | Medium                                    | Low (standardized and fixed configuration)            |


---

## 9. Conclusion

PrimeX Cipher is an educational symmetric encryption algorithm that uses number theory and permutation principles. Though not secure for real-world use, it illustrates essential cryptographic concepts. Its simplicity supports learning through implementation and testing.

Future enhancements may include:
- Larger alphabets
- Multi-round structure
- Non-linear operations

These additions can extend PrimeX's teaching potential.

---

## References

- Stallings, W. (2017). *Cryptography and Network Security: Principles and Practice*. Pearson.  
  [View on Pearson](https://www.pearson.com/en-us/subject-catalog/p/cryptography-and-network-security-principles-and-practice/P200000007945/9780134444284)  
  [Preview on Google Books](https://books.google.com/books?id=4VDNDgAAQBAJ)

- Paar, C., & Pelzl, J. (2010). *Understanding Cryptography*. Springer.  
  [View on Springer](https://link.springer.com/book/10.1007/978-3-642-04101-3)  
  [PDF Preview (Springer)](https://link.springer.com/content/pdf/10.1007%2F978-3-642-04101-3.pdf)

- Menezes, A., van Oorschot, P., & Vanstone, S. (1996). *Handbook of Applied Cryptography*. CRC Press.  
  [View on CRC Press](https://www.routledge.com/Handbook-of-Applied-Cryptography/Menezes-van-Oorschot-Vanstone/p/book/9780849385230)  
  [Free Full PDF (Official)](https://cacr.uwaterloo.ca/hac/about/chapters.html)
