---
toc: true
layout: post
title: Trimester 2 MCQ Review Reflection
description: Reflection on AP CSP multiple-choice mistakes from Trimester 2, including security vs licensing, bit-length calculations, reasonable time, simulation outputs, and edge cases in algorithms.
permalink: /tri2-mcqreview
categories: [CSP, Reflection]
---

![Collegeboard MCQ Score]({{ site.baseurl }}/images/collegeboard-mcq-score.png)

**Collegeboard MCQ Score**

## Questions that I got wrong

![Q9 – Transmit private data securely]({{ site.baseurl }}/images/tri2-mcq-q9.png)

![Q49 & Q50 – Bit sequences and reasonable time]({{ site.baseurl }}/images/tri2-mcq-q49-q50.png)

![Q52 – Bacteria population simulation]({{ site.baseurl }}/images/tri2-mcq-q52.png)

![Q64 – Error with multiplication using repeated addition]({{ site.baseurl }}/images/tri2-mcq-q64.png)

## 1. Security vs Licensing (Q9)

**Question**  
Which method provides the most security when transmitting private data?

- **My answer:** A — Certifying the data with a Creative Commons license  
- **Correct answer:** C — Sending the data using public-key encryption

**What I mixed up**  
I confused legal protection with technical security.

- A **Creative Commons license** controls how content can be legally shared and reused. It says what people are allowed to do with the content.
- **Public-key encryption** actually secures data during transmission by encrypting it so only the intended recipient can read it.

Licenses protect rights. Encryption protects data.

**Lesson learned**  
When a question includes words like **secure**, **private**, or **transmission**, I should immediately look for:

- Encryption
- Cryptographic methods
- Secure protocols

I should **not** pick answers about licensing, copyrights, or legal tools—those are about permission, not protection.

---

## 2. Bit-Length Calculation Error (Q49)

**Question**  
What is the minimum number of bits needed to assign a unique binary sequence to each of 100 staff members?

- **My answer:** B — 6 bits  
- **Correct answer:** C — 7 bits

**What went wrong**  
I underestimated how many combinations 6 bits can represent.

- \(6\) bits → \(2^6 = 64\) combinations  
- \(7\) bits → \(2^7 = 128\) combinations

Since \(64 < 100\), 6 bits are not enough.  
7 bits is the **smallest** number of bits where the total combinations (128) cover all 100 staff members.

**Lesson learned**  
For these questions I need to:

- Actually compute \(2^n\) and compare it to the required count.
- Memorize the first few powers of 2 for speed:
  - \(2^6 = 64\)
  - \(2^7 = 128\)
  - \(2^8 = 256\), etc.
- Practice converting between binary and decimal so this kind of reasoning feels natural.

---

## 3. Misunderstanding “Reasonable Time” (Q50 – Algorithm Complexity)

**Question**  
Which of the algorithms run in reasonable time?

I. Access each element twice  
II. Access each element \(n\) times  
III. Access only the first 10 elements

- **My answer:** B — III only  
- **Correct answer:** D — I, II, and III

**What I misunderstood**  
I thought accessing each element \(n\) times (which is \(n^2\) operations) was **not** reasonable.  
But in AP CSP, “reasonable time” means **polynomial time**, not “fast in the real world.”

- Algorithm I → \(2n\) → \(O(n)\) → polynomial → **reasonable**  
- Algorithm II → \(n^2\) → \(O(n^2)\) → polynomial → **reasonable**  
- Algorithm III → constant time → \(O(1)\) → **reasonable**

All three are polynomial (or better), so all are considered to run in reasonable time.

**Lesson learned**  
For questions like these, I need to memorize the Big O Chart to know which ones are reasonable and which ones are unreasonable

- **Reasonable time (yes):** \(O(n)\), \(O(n^2)\), \(O(n^3)\), or any polynomial  
- **Not reasonable (no):** \(O(2^n)\), \(O(n!)\), or exponential/factorial

If the time complexity is polynomial, AP CSP considers it **reasonable**, even if it seems slow in practice.

---

## 4. Misreading Output Meaning (Q52 – Bacteria Simulation)

**Question**  
Which of the following are true statements about the simulation?

I. The simulation continues until either 24 hours pass or the population reaches 0.  
II. The simulation displays the average change in population per hour over the course of the simulation.  
III. The simulation displays the total population at the end of the simulation.

- **My answer:** D — I and II  
- **Correct answer:** A — I only

**What I misread**  
The code’s final line displays:

```text
currentPop - startPop
```

This is the net change in population over the entire simulation, not the average change per hour.

To show an average per hour, it would need to compute something like:

```text
(currentPop - startPop) / hours
```

There was no division by the number of hours, so statement II was false.  
The code also did not display the final total population directly, so statement III was false as well.

**Lesson learned**  
When a question mentions an **“average per ___”**:

- Check if the expression divides by the number of units (hours, days, items, etc.).
- If there’s **no division**, the value is almost certainly a **total/net change**, not an average rate.

For simulations, I need to read the `DISPLAY(...)` expression literally and match it word-for-word to the answer choices.

---

## 5. Multiply Procedure and Negative `y` Values (Q64)

**Question**  
For which procedure calls does `Multiply(x, y)` NOT return the intended value? (Select two.)

- **My answer:** A — `Multiply(2, 5)`  
- **Correct answers:**  
  - B — `Multiply(2, -5)`  
  - D — `Multiply(-2, -5)`

**What the code actually does**  
The procedure starts with:

```text
count ← 0
result ← 0
REPEAT UNTIL count ≥ y
  ...
```

If `y` is **negative**, then `count` (0) is already **greater than or equal to** `y`.  
That means the loop body never runs and the procedure immediately returns `0`, which is wrong for all negative `y` values.

**Lesson learned**  
I assumed the algorithm worked for all integers without checking edge cases.

Going forward I will:

- Always test algorithms with **positive**, **negative**, and **zero** inputs.  
- Pay special attention to loop conditions like `count ≥ y` and think about what happens when `y` is negative.  
- Evaluate the loop condition **before** assuming the loop will run.

---

## 6. Role of Certificate Authorities (Q40)

**Question**  
Which of the following best explains how a certificate authority is used in protecting data?

- **My answer:** D — A certificate authority verifies the authenticity of encryption keys used in secured communications.  
- **Correct answer:** D — A certificate authority verifies the authenticity of encryption keys used in secured communications.

**What I didn’t fully understand**  
Even though I chose the correct answer, I did not fully understand **how** certificate authorities (CAs) protect data.

- CAs issue **digital certificates** that bind a public key to an organization or website.
- When my browser connects over HTTPS, it checks the website’s certificate against trusted CAs to verify that the **public key really belongs to that site**.
- This prevents attackers from swapping in their own keys and doing a man-in-the-middle attack.

So a certificate authority’s main job is to **verify the authenticity of public keys**, not to:

- Scan websites for viruses  
- Issue user passwords  
- Store mappings from domain names to IP addresses (that’s a DNS role)

**Lesson learned**  
When I see questions about **certificate authorities**, I should think:

- “They **verify and vouch for public keys** using digital certificates.”  
- “They are part of the **trust chain** that makes encrypted connections (like HTTPS) reliable.”

This is how they help protect data: by ensuring my encrypted connection is really with the intended site, not an impostor.

---

## 7. Data Represented by Bit Sequences (Q17)

**Question**  
Which of the following can be represented by a sequence of bits?

I. An integer  
II. An alphanumeric character  
III. A machine language instruction

- **My answer:** D — I, II, and III  
- **Correct answer:** D — I, II, and III

**What I clarified**  
I got this question correct, but it helped me solidify what “all digital data is bits” really means.

- At the lowest level, **every** piece of digital information is stored as 0s and 1s.  
- Integers are stored using binary number systems.  
- Alphanumeric characters are stored using encodings like ASCII or Unicode, which map characters to specific bit patterns.  
- Machine language instructions are stored as bit patterns that the processor decodes as operations.

So it’s not just numbers that are bits—**all** types of data in a computer are ultimately sequences of bits, just interpreted in different ways.

**Lesson learned**  
When I see questions asking “what can be represented as bits,” I should remember:

- If it’s digital data inside a computer (numbers, text, images, sound, instructions), it can be represented by a sequence of bits.  
- The key idea is not whether something is “numeric” but whether it’s stored/processed by a computer at all.

---

## Final Takeaways

Across these questions, my main patterns of error were:

- Mixing up concepts - example: security vs licensing, total vs average.  
- Not fully checking the math (\(2^n\) vs required count).  
- Misunderstanding AP CSP’s formal definitions (reasonable time = polynomial).  
- Skipping edge case analysis for algorithms.

I should slow down on the calculation problems and carefully check the answer choices before picking the correct answer. I should also check the AP CSP's official definitions of vocabularies and learn more about technological vocabs and concepts. Words like security licensing and encryption confused me on the test as I didn't fully understand what they meant .
