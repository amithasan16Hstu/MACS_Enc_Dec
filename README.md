<p align="center">
  <img src="HSTU.png" alt="HSTU Logo" width="250" height="300">
</p>
<h1 align="center">
  <b> PrimeX Cipher: Leveraging Prime Numbers for Text Encryption and Decryption</b>
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

<p align="justify">
The <strong>PrimeX Cipher</strong> is a custom-designed symmetric cryptographic algorithm that integrates modular arithmetic and block permutation to achieve secure and reversible text encryption. Developed with simplicity and clarity in mind, the cipher utilizes a user-defined prime number and permutation array as the encryption key. The process involves converting plaintext characters into numeric representations, applying a modular shift using the prime number, rearranging the sequence through permutation, and then performing modular multiplication for final encryption. Decryption reverses each step using the inverse permutation and the modular inverse of the prime number, ensuring accurate retrieval of the original plaintext. This algorithm highlights fundamental cryptographic principles such as substitution, permutation, and key-dependent transformation. <strong>PrimeX</strong> is ideal for educational purposes, demonstrating how mathematical operations can be applied to create a basic but effective encryption scheme. Its implementation fosters a deeper understanding of symmetric encryption, number theory, and algorithm design.
</p>

---

## Introduction

<p align="justify">
In the ever-evolving field of information security, cryptographic algorithms play a critical role in ensuring the confidentiality, integrity, and authenticity of digital data. While modern encryption techniques such as AES and RSA are widely adopted in industry, learning and understanding the foundational concepts behind encryption is essential for students and enthusiasts entering the field of computer science and cybersecurity. The <strong>PrimeX Cipher</strong> is a lightweight, symmetric cryptographic algorithm designed with educational clarity and computational simplicity in mind. It combines basic number theory with block-level permutation to demonstrate how mathematical transformations can securely encode and decode textual information.
The PrimeX Cipher operates by transforming plaintext into ciphertext through a series of reversible steps involving modular arithmetic and custom permutations. Each character of the plaintext is first converted into a numeric value based on its alphabetical position. These values are then shifted using a prime number, rearranged using a predefined permutation array, and further transformed through modular multiplication. The decryption process follows the inverse path, using the modular inverse and inverse permutation to accurately recover the original message.This algorithm is particularly useful for academic projects, cryptographic demonstrations, and introductory courses in computer security. Its structure offers an excellent platform for understanding core principles such as substitution, permutation, key dependency, and modular operations. By abstracting the complexity of industrial-grade algorithms, the PrimeX Cipher provides a hands-on learning experience while still maintaining the logical rigor of cryptographic systems.
</p>


