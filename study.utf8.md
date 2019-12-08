---
author: |
    | William Findlay
title: |
    | COMP4109 Final Exam Practice
date: \today
#bibliography: untitled.bib
biblio-style: ieee
subparagraph: yes
classoption: 12pt
header-includes:
    - \usepackage{findlayrmd}
output:
    pdf_document:
        citation_package: biblatex
        number_sections: true
        fig_crop: true
        fig_caption: true
        keep_tex: false
        pandoc_args: ["--listings"]
---

<!-- Setup -->
\pagestyle{fancy}
\setlength{\headheight}{15pt}
\counterwithin{lstlisting}{section}
\renewcommand{\maketitle}{\oldmaketitle}

<!-- Title page -->
\maketitle
\thispagestyle{empty}

<!-- Table of contents -->
\newpage
\pagenumbering{roman}
\tableofcontents

<!-- List of figs, tables, listings -->
\newpage
\listoffigures
\newpage
\listoftables
\newpage
\lstlistoflistings

<!-- Setup the rest of the document -->
\newpage
\pagenumbering{arabic}
\setcounter{page}{1}

# List of Topics

\begin{table}
\caption[Topics for the final]{Topics for the final with percentages and approximate number of questions.\newline
N.b.\ total number of questions is 44, but total approximate only adds up to 39.}
\begin{tabular}{|c|l|l|}
\hline
\textbf{Topic} & \textbf{Percentage} & \textbf{$\approx$ Questions}\\
\hline
\hline
Classical Crypto & ($10\%$) & 4\\
\hline
Secret Key Crypto & ($10\%$) & 4\\
\hline
Security Models and Goals & ($18\%$) & 8\\
\hline
Public Key Crypto and Efficiency & ($15\%$) &7\\
\hline
Hash Functions & ($7\%$) &3\\
\hline
Hashes/MACs/DSS & ($10\%$) &4\\
\hline
Secret Sharing & ($2\%$) &1\\
\hline
WEP & ($5\%$) &2\\
\hline
Secure Internet Connections & ($10\%$) &4\\
\hline
Zero Knowledge Proofs & ($5\%$) &2\\
\hline
\end{tabular}
\end{table}

\part{Notes}

# Midterm 1

## Classical Crypto

## Secret Key Crypto

## Security Models and Goals

# Midterm 2

## Public Key Crypto

## Hash Functions

## Hashes/MACs/DSS

# Post-Midterms

## Secret Sharing

## WEP

- security goals
    - confidentiality (nope)
    - access control (nope)
    - data integrity (nope)
- how it works
    - random 24-bit IV $v$
    - compute 32-bit checksum of $m$
    - $c = \text{RC4}(v, k) \oplus (m || \text{checksum}(m))$
- many problems
    - $\text{RC4}(v, k)$ not good due to $k$ and $v$ themselves (without even exploiting how crappy RC4 is)
        - really only depends on $v$
        - because $k$ rarely changes and is often shared by everyone in LAN
        - guaranteed collision in $v$ after $\approx$ 16 millions transmissions
        - birthday attack on random $v$ only needs 4096
        - $v$ often tracked with counter and reset when device is started
        - so small $v$ $\implies$ lots of collisions
    - collision + KPA means:
        - if we have $<v,c>$, we can decrypt $<v, c'>$ if we can find a collision in $v$
    - decryption dictionary
        - $\text{RC4}(v_i, k)$, watch transmissions in the network
        - full dictionary only needs 24GB of space
    - malleability
        - message modification is easy since checksums suck
        - only good at detecting one or two flipped bits, errors can cancel each other
    - authentication spoofing
        - base station sends plaintext challenge $z$
        - client sends back the WEP encryption of $z$
        - observer has the plaintext, ciphertext pair for free
    - double encryption
        - you can just send $q$ to yourself from another station
        - oracle encrypts $q', v' = \text{WEP}(q)$
        - if $v = v'$, we can decrypt $q'$ to $q$

## Secure Internet Connections

## Zero Knowledge Proofs

\part{Practice Questions}

# Provided Multiple Choice Questions

1. A stream cipher provides which of the following?
    (a) Indistinguishability
    (a) Unpredictability
    (a) Synchronicity
    (a) A and B
    (a) None of the above
\vskip 1em
1. The security of RSA is believed to be based on...
    (a) The difficulty of factoring the modulus
    (a) The computational DH problem
    (a) The discrete log problem
    (a) B and C
    (a) None of the above
\vskip 1em
1. What is $17^{122} \bmod 23$?
    (a) $17 \times 122 \bmod 23$
    (a) $17^{7} \bmod 23$
    (a) $17^{12} \bmod  23$
    (a) $17^{12} \bmod 22$
    (a) None of the above
\vskip 1em
1. Consider the following ciphertext $c = \text{wud}$. The shift (Caesar) cipher was used. What is the plaintext?
    (a) foo
    (a) the
    (a) ack
    (a) gen
    (a) None of the above
\vskip 1em
1. Changing a single bit of the plaintext should change about 1/2 the bits of the ciphertext?
What security goal is this?
    (a) Diffusion
    (a) Confusion
    (a) Unpredictability
    (a) Non-Malleability
    (a) None of the above
\vskip 1em
1. What information does a collision reveal when using ECB (electronic code book)? When $c_i = c_j$, what do we know?
    (a) It will leak information about the plaintext
    (a) It reveals the contents of all the blocks
    (a) It causes an existential forgery
    (a) It leaks information about the secret key
    (a) None of the above
\vskip 1em
1. Which of the following does a MAC provide that a hash function does not?
    (a) Data origin authentication (anyone)
    (a) Data integrity authentication (those with the key)
    (a) Data origin authentication (those with the key)
    (a) Non-repudiation (those with the key)
    (a) None of the above
\vskip 1em
1. Assume the padding scheme outlined in class for CBC mode. The cipher has block length 2 bytes.
How do we pad the following plaintext? `a1 b2 33 12`
    (a) Append `02` 4 times
    (a) Append `02` 2 times
    (a) Append `00` 2 times
    (a) Do nothing
    (a) None of the above
\vskip 1em

For the next two questions, consider the following connection encrypted line:
\begin{center}
\lstinline{TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384, 256 bit keys, TLS 1.2}
\end{center}

9. Which digital signature scheme is used?
    (a) ECDHE
    (a) RSA
    (a) AES
    (a) SHA384
    (a) None of the above
\vskip 1em
1. Which security protocol is used?
    (a) ECDHE
    (a) TLS 1.2
    (a) AES
    (a) GCM
    (a) None of the above

# Custom Multiple Choice Questions

<!--
1. This is a template question?
    (a)
    (a)
    (a)
    (a)
    (a) None of the above
\vskip 1em
-->

1. Which of the following is not a security flaw in WEP?
    (a) Easy to find collisions in $v$
    (a) $k$ is often shared across the entire LAN
    (a) An attacker can mount a chosen plaintext attack by sending $m$ to himself
    (a) An attacker can mount a known plaintext attack by finding a collision in $v$
    (a) All of the above **are** security flaws in WEP
\vskip 1em
1. How does WEP encrypt messages?
    (a) $\text{RC4}(\text{checksum}(m), k) \oplus (v || m)$
    (a) WEP does not encrypt messages
    (a) $\text{RSA}(v, k) \oplus (m || \text{checksum}(m))$
    (a) $\text{RC4}(v, k) \oplus (m || \text{checksum}(m))$
    (a) None of the above
\vskip 1em
1. Which security goal of WEP is broken by the ability to easily find collisions in $v$?
    (a) Indistinguishability
    (a) Confidentiality
    (a) Access control
    (a) Data integrity
    (a) None of the above
\vskip 1em
1. How many bits is $v$ in WEP?
    (a) 32
    (a) 8
    (a) 48
    (a) 24
    (a) None of the above
\vskip 1em
1. How many bits is the checksum in WEP?
    (a) 32
    (a) 8
    (a) 48
    (a) 24
    (a) None of the above
\vskip 1em
1. Why are checksums not a good choice for data integrity in WEP?
    (a) Vulnerable to an addition attack
    (a) Easily malleable
    (a) Errors can cancel
    (a) B and C
    (a) None of the above
\vskip 1em
1. Which of the following is not a security goal of WEP?
    (a) Confidentiality
    (a) Data integrity
    (a) Indistinguishability
    (a) Access control
    (a) None of the above
\vskip 1em
1. What is the definition of a symmetric key encryption scheme?
    (a) Three efficient algorithms: $G,E_e,D_d$
    (a) Five-tuple: $K,P,C,E,D$
    (a) An encryption scheme where the key is always the same size
    (a) Three-tuple: $K,P,C$
    (a) None of the above
\vskip 1em
1. A \_\_\_\_\_\_\_\_\_\_ allows us to encrypt messages longer than the plaintext length.
    (a) Symmetric key encryption scheme
    (a) Block cipher
    (a) Mode of operation
    (a) Public key encryption scheme
    (a) None of the above
\vskip 1em
1. What is the plaintext length in an unmodified Caesar cipher?
    (a) The key length
    (a) Any size
    (a) 26
    (a) 1
    (a) None of the above
\vskip 1em
1. What is the plaintext length in an unmodified Vigen&egrave;re cipher?
    (a) The key length
    (a) Any size
    (a) 26
    (a) 1
    (a) None of the above
\vskip 1em
1. How is a Vigen&egrave;re cipher similar to one-time pad?
    (a) One-time pad is like Vigen&egrave;re except it has key length = plaintext length
    (a) They are the same thing
    (a) One-time pad is like Vigen&egrave;re except the key changes each time
    (a) A and C
    (a) None of the above
\vskip 1em
1. The one-time pad \_\_\_\_\_\_\_\_\_\_.
    (a) Is unconditionally secure
    (a) Provides perfect secrecy
    (a) Is extremely efficient
    (a) A and B
    (a) None of the above
\vskip 1em
1. Which of the following is a problem with the one time pad?
    (a) It is malleable
    (a) It is vulnerable to chosen plaintext attacks
    (a) It can only be used for very large messages
    (a) The keyspace is finite
    (a) None of the above
\vskip 1em
1. Which of the following symmetric key encryption schemes provides information theoretic security IND-KPA?
    (a) AES in CBC mode
    (a) Affine cipher
    (a) One-time pad
    (a) AES in CTR mode
    (a) None of the above
\vskip 1em
1. Which of the following is not a security goal?
    (a) Non-malleability
    (a) Access control
    (a) Indistinguishability
    (a) Data integrity
    (a) All of the above **are** security goals
\vskip 1em
1. Which of the following is not an attack model?
    (a) Known plaintext attack
    (a) Chosen plaintext attack
    (a) Ciphertext only attack
    (a) Chosen message attack
    (a) All of the above **are** attack models
\vskip 1em
1. Which of the following is not a security level?
    (a) Complexity theoretic
    (a) Polynomial
    (a) Computational
    (a) Information theoretic
    (a) All of the above **are** security levels
\vskip 1em
1. An attacker knows one or more plaintext, ciphertext pairs and tries to find $k$. What attack is this?
    (a) Chosen plaintext attack
    (a) Ciphertext only attack
    (a) Known plaintext attack
    (a) Ciphertext stealing
    (a) None of the above
\vskip 1em
1. An attacker has access to an oracle that can encrypt messages. What attack is this?
    (a) Chosen plaintext attack
    (a) Ciphertext only attack
    (a) Known plaintext attack
    (a) Ciphertext stealing
    (a) None of the above
\vskip 1em
1. An attacker tries to decrypt ciphertext with no other information. What attack is this?
    (a) Chosen plaintext attack
    (a) Ciphertext only attack
    (a) Known plaintext attack
    (a) Ciphertext stealing
    (a) None of the above
\vskip 1em
1. Which of the following best describes unicity distance?
    (a) The number of times you have to encrypt random plaintext before getting a collision in the ciphertext
    (a) The theoretical complexity difference between two encryption schemes
    (a) The expected minimum ciphertext length required to uniquely compute the key
    (a) The size of a given ciphertext space
    (a) None of the above
\vskip 1em
1. What is a spurious key?
    (a) A key that does not exist in our keyspace
    (a) A key that uniquely maps plaintext to a given ciphertext
    (a) Another key that decrypts ciphertext to an alternative, yet valid, plaintext
    (a) A key that results in gibberish decryption
    (a) None of the above
\vskip 1em
1. If $c = \texttt{Dpssphtzbe}$ is the ciphertext generated by one-time pad, what is the corresponding plaintext?
    (a) `Andybuigod`
    (a) `Triisgreat`
    (a) `Williamsux`
    (a) `Amandabest`
    (a) Not enough information
\vskip 1em
1. If $c = \texttt{Dpssphtzbe}$ is the ciphertext generated by a Caesar cipher, what is the corresponding plaintext?
    (a) `Andybuigod`
    (a) `Triisgreat`
    (a) `Williamsux`
    (a) `Amandabest`
    (a) Not enough information
\vskip 1em
1. Which of the following is the current standard for block ciphers?
    (a) 2DES
    (a) 3DES
    (a) AES
    (a) DES
    (a) None of the above
\vskip 1em
1. A meet in the middle attack reduces 2DES from \_\_\_\_\_\_\_\_\_\_ to \_\_\_\_\_\_\_\_\_\_.
    (a) An NP-Hard problem, a P problem
    (a) 128 bit block length, 112 bit effective block length
    (a) 112 bit block length, 57 bit effective block length
    (a) 64 bit block length, 60 bit effective block length
    (a) None of the above
\vskip 1em
1. A meet in the middle attack reduces 3DES from \_\_\_\_\_\_\_\_\_\_ to \_\_\_\_\_\_\_\_\_\_.
    (a) An NP-Complete problem, an NP-Hard problem
    (a) 168 bit block length, 57 bit effective block length
    (a) 256 bit block length, 128 bit effective block length
    (a) 168 bit block length, 112 bit effective block length
    (a) None of the above
\vskip 1em
1. DES suffers from \_\_\_\_\_\_\_\_\_\_.
    (a) Inefficient encryption
    (a) Short block length
    (a) Long key length
    (a) B and C
    (a) None of the above
\vskip 1em
1. 3DES works by doing which of the following?
    (a) $D_{k_3}(D_{k_2}(E_{k_1}(m)))$
    (a) $D_{k_3}(E_{k_2}(D_{k_1}(m)))$
    (a) $E_{k_3}(E_{k_2}(E_{k_1}(m)))$
    (a) $E_{k_3}(D_{k_2}(E_{k_1}(m)))$
    (a) None of the above
\vskip 1em
1. 2DES works by doing which of the following?
    (a) $E_{k_2}(D_{k_1}(m))$
    (a) $D_{k_2}(D_{k_1}(m))$
    (a) $E_{k_2}(E_{k_1}(m))$
    (a) $D_{k_2}(E_{k_1}(m))$
    (a) None of the above
\vskip 1em
1. In 3DES, which of the following are possible?
    (a) $k_1 \ne k_2 \ne k_3$
    (a) $k_1 = k_2 = k_3$
    (a) $k_1 \ne k_2, k_2 = k_3$
    (a) A and B
    (a) All of the above
\vskip 1em
1. According to the PKCS#7 padding scheme we saw in class, how would you pad `ae 12 64` with a block length of 6 bytes?
    (a) `ae 12 64 06 06 06`
    (a) `06 06 06 ae 12 64`
    (a) `ae 12 64 03 03 03`
    (a) `03 03 03 ae 12 64`
    (a) None of the above
\vskip 1em
1. According to the PKCS#7 padding scheme we saw in class, how would you pad `ae 12 64` with a block length of 3 bytes?
    (a) `ae 12 64`
    (a) `03 03 03 ae 12 64`
    (a) `ae 12 64 03 03 03`
    (a) `ae 12 64 00 00 00`
    (a) None of the above
\vskip 1em
1. Ciphertext stealing works with which of the following modes of operation?
    (a) CBC
    (a) GCM
    (a) ECB
    (a) CTR
    (a) None of the above
\vskip 1em
1. Which mode of operation has no semantic security?
    (a) CBC
    (a) GCM
    (a) ECB
    (a) CTR
    (a) None of the above
\vskip 1em
1. CTR mode generates keys by \_\_\_\_\_\_\_\_\_\_.
    (a) Encrypting an increasing value each time, starting at zero
    (a) Incrementing and then encrypting a nonce each time
    (a) Decrementing a nonce, encrypting it, and then incrementing it each time
    (a) Encrypting a nonce and then incrementing it each time
    (a) None of the above
\vskip 1em
1. How does CTR mode generate ciphertext?
    (a) Each block of plaintext is XORed with the encrypted nonce
    (a) Each plaintext block is encrypted using the nonce as a key
    (a) Each block of plaintext is XORed with the previous ciphertext and then encrypted
    (a) Each plaintext block is run through the encryption algorithm and then XORed with the nonce
    (a) None of the above
\vskip 1em
1. Which of the following describes ECB?
    (a) Block length does not matter
    (a) Encrypt each block individually
    (a) Computationally IND-CPA secure
    (a) ECB is technically a stream cipher
    (a) None of the above
\vskip 1em
1. Which of the following describes CBC?
    (a) Suffers from a lack of diffusion
    (a) Vulnerable to meet in the middle attacks
    (a) XOR plaintext block with previous ciphertext block and then encrypt
    (a) Does not require padding
    (a) None of the above
\vskip 1em
1. In ciphertext stealing we do which of the following?
    (a) Pad last block with `0`s until it meets block length, encrypt as normal, then swap first and last blocks
    (a) Pad last block with `1`s until it meets block length, encrypt as normal, then swap first and last blocks
    (a) Pad last block with `1`s until it meets block length, encrypt as normal, then swap last two blocks
    (a) Pad last block with `0`s until it meets block length, encrypt as normal, then swap last two blocks
    (a) None of the above
\vskip 1em
1. What is $20^{73} \bmod 37$?
    (a) 20
    (a) 37
    (a) $20^{36} \bmod 37$
    (a) 1
    (a) None of the above
\vskip 1em
1. Which of the following is in the correct order of reducibility?
    (a) $\text{DL} > \text{DDH} > \text{CDH}$
    (a) $\text{DL} > \text{CDH} > \text{DDH}$
    (a) $\text{DDH} > \text{CDH} > \text{DL}$
    (a) $\text{CDH} > \text{DDH} > \text{DL}$
    (a) None of the above
\vskip 1em
1. Which of the following describes the CDH problem?
    (a) Given $(p, g, g^a, g^b, n)$, try to determine if $n = g^{ab} \bmod p$ or $n = g^x \bmod p$
    (a) Given $(p, g, g^a)$, try to find $a \bmod p$.
    (a) Given $(p, g, g^a, g^b)$, try to compute $g^{ab} \bmod p$
    (a) Given $(p, g, g^a, b)$, try to compute $g^{ab} \bmod p$
    (a) None of the above
\vskip 1em
1. Which of the following describes the DDH problem?
    (a) Given $(p, g, g^a, g^b, n)$, try to determine if $n = g^{ab} \bmod p$ or $n = g^x \bmod p$
    (a) Given $(p, g, g^a)$, try to find $a \bmod p$.
    (a) Given $(p, g, g^a, g^b)$, try to compute $g^{ab} \bmod p$
    (a) Given $(p, g, g^a, b)$, try to compute $g^{ab} \bmod p$
    (a) None of the above
\vskip 1em
1. Which of the following describes the DL problem?
    (a) Given $(p, g, g^a, g^b, n)$, try to determine if $n = g^{ab} \bmod p$ or $n = g^x \bmod p$
    (a) Given $(p, g, g^a)$, try to find $a \bmod p$.
    (a) Given $(p, g, g^a, g^b)$, try to compute $g^{ab} \bmod p$
    (a) Given $(p, g, g^a, b)$, try to compute $g^{ab} \bmod p$
    (a) None of the above
\vskip 1em
1. The security of Diffie-Hellman relies on which of the following?
    (a) Discrete log problem
    (a) Computational Diffie-Hellman problem
    (a) Decisional Diffie-Hellman problem
    (a) B and C
    (a) All of the above
\vskip 1em
1. In Diffie-Hellman, what is public information?
    (a) $g, p, g^a, g^b$
    (a) $g, p, a, b$
    (a) $g, p$
    (a) $g^a, g^b$
    (a) None of the above
\vskip 1em
1. Which of the below corresponds to a vulnerability of Diffie-Hellman?
    (a) Ciphertext stealing
    (a) Existential forgery
    (a) Meet in the middle
    (a) Man in the middle
    (a) None of the above
\vskip 1em
1. What is the definition of a public key encryption scheme?
    (a) Five-tuple: $K,P,C,E,D$
    (a) Three-tuple: $K,P,C$
    (a) Three efficient algorithms: $G,E_e,D_d$
    (a) An encryption scheme where the key is always public
    (a) None of the above
\vskip 1em
1. Which of the following is not a public key encryption scheme?
    (a) RSA
    (a) ElGamal
    (a) Diffie-Hellman
    (a) All of the above are public key encryption schemes
    (a) None of the above are public key encryption schemes
\vskip 1em
1. When $N=pq$, where $p,q$ are prime, what is $\phi(N)$?
    (a) Undefined
    (a) $N-1$
    (a) $(p-1)(q-1)$
    (a) $1$
    (a) None of the above
\vskip 1em
1. When $n$ is prime, what is $\phi(n)$?
    (a) Undefined
    (a) $n$
    (a) $0$
    (a) $n-1$
    (a) none of the above
\vskip 1em
1. How do we calculate $e, d$ in RSA?
    (a) Find $e, d$ such that $ed \equiv 1 \bmod \phi(N)$
    (a) Find $e, d$ such that $ed \equiv 0 \bmod \phi(N)$
    (a) Find $e, d$ such that $ed \equiv 0 \bmod N$
    (a) Find $e, d$ such that $ed \equiv 1 \bmod N$
    (a) None of the above
\vskip 1em
1. How do we calculate $N$ in RSA?
    (a) Take $N=ed$
    (a) Take $N=pq$ where $p, q$ are two large random numbers
    (a) Take $N=pq$ where $p, q$ are two large primes
    (a) Take $N$ as some random large number
    (a) None of the above
\vskip 1em
1. Which of the following would yield $m$ in RSA?
    (a) $(m^d)^e \bmod N$
    (a) $c^d \bmod \phi(N)$
    (a) $(m^e)^e \bmod N$
    (a) $(m^e)^d \bmod N$
    (a) None of the above
\vskip 1em
1. What is our public key in RSA?
    (a) $(e, N)$
    (a) $(e, p, q)$
    (a) $(e, \phi(N))$
    (a) $(d, N)$
    (a) None of the above
\vskip 1em
1. What is our private key in RSA?
    (a) $(d, \phi(N))$
    (a) $(d, N)$
    (a) $(d, p, q)$
    (a) $(e, N)$
    (a) None of the above
\vskip 1em
1. What is a generator in $\mathbb{Z}_p^*$?
    (a) Some integer in the group that can create every other group member when raised to various powers
    (a) Any member of the group
    (a) A way of creating other groups
    (a) The source of the group's power
    (a) None of the above
\vskip 1em
1. What is the cryptographic significance of the Euclidean Algorithm?
    (a) Helps us calculate $N$
    (a) Helps us calculate $p, q$
    (a) Helps us calculate $\phi(N)$
    (a) Forms the basis for Wiener's attack
    (a) None of the above
\vskip 1em
1. What is the cryptographic significance of the Extended Euclidean Algorithm?
    (a) Good for fast modular exponentiation
    (a) Helps us find modular inverse
    (a) Forms the basis for Wiener's attack
    (a) An integral part of the meet in the middle attack on 2DES
    (a) None of the above
\vskip 1em
1. Which of the following describes Wiener's attack?
    (a) Attempts to find $k$ in ElGamal
    (a) Attempts to find $d$ in RSA
    (a) Attempts to find $p, q$ in RSA
    (a) Attempts to find $a$ in ElGamal
    (a) None of the above
\vskip 1em
1. Generation in ElGamal involves which of the following?
    (a) Finding two primes $p, q$ such that $p = 2q + 1$
    (a) Finding two random large primes
    (a) Computing $a, b$ such that $a, b$ are primitive elements in $\mathbb{Z}_p^*$
    (a) Finding $e, d$
    (a) None of the above
\vskip 1em
1. Generation in ElGamal involves which of the following?
    (a) Factoring the modulus
    (a) Finding a generator $g$ in $\mathbb{Z}_p^*$ and computing $g^a \bmod p$ for random $a$
    (a) Finding a three-tuple of efficient equations
    (a) Finding $a, b$ such that $a$ and $b$ are coprime
    (a) None of the above
\vskip 1em
1. What is a primitive element in $\mathbb{Z}_p^*$?
    (a) An element with order equal to the size of the group
    (a) An element equal to $1 \bmod p$
    (a) A prime number in the group
    (a) The $p$ in $\mathbb{Z}_p^*$
    (a) None of the above
\vskip 1em
1. What is a generator in $\mathbb{Z}_p^*$?
    (a) An element with order equal to the size of the group
    (a) An element equal to $1 \bmod p$
    (a) A prime number in the group
    (a) The $p$ in $\mathbb{Z}_p^*$
    (a) None of the above
\vskip 1em
1. What is $\phi(37)$?
    (a) 4
    (a) 38
    (a) 36
    (a) 12
    (a) None of the above
\vskip 1em
1. What is $\phi(45)$?
    (a) 44
    (a) 16
    (a) 24
    (a) 12
    (a) None of the above
\vskip 1em
1. Which of the following is not a security property of cryptographic hash functions?
    (a) Weak collision resistance
    (a) Preimage resistance
    (a) Collision resistance
    (a) Second preimage resistance
    (a) All of the above **are** security properties of cryptographic hash functions
\vskip 1em
1. Which of the following describes preimage resistance?
    (a) Hard to find any $m' \ne m$ such that $H(m) = H(m')$
    (a) Hard to find $m' \ne m$ given $m$ such that $H(m) = H(m')$
    (a) Hard to find $H(H(m))$
    (a) Hard to find $m$ given $H(m)$
    (a) None of the above
\vskip 1em
1. Which of the following describes second preimage resistance?
    (a) Hard to find any $m' \ne m$ such that $H(m) = H(m')$
    (a) Hard to find $m' \ne m$ given $m$ such that $H(m) = H(m')$
    (a) Hard to find $H(H(m))$
    (a) Hard to find $m$ given $H(m)$
    (a) None of the above
\vskip 1em
1. Which of the following describes collision resistance?
    (a) Hard to find any $m' \ne m$ such that $H(m) = H(m')$
    (a) Hard to find $m' \ne m$ given $m$ such that $H(m) = H(m')$
    (a) Hard to find $H(H(m))$
    (a) Hard to find $m$ given $H(m)$
    (a) None of the above
\vskip 1em
1. What type of forgery might you create given a hash function that has all security properties except second preimage resistance?
    (a) Selective
    (a) Perfect
    (a) Existential
    (a) Universal
    (a) None of the above
\vskip 1em
1. What type of forgery might you create given a hash function that has no collision resistance?
    (a) Selective
    (a) Perfect
    (a) Existential
    (a) Universal
    (a) None of the above
\vskip 1em
1. What type of forgery might you create given a hash function that always returns the first $x$ bytes of $m$?
    (a) Selective
    (a) Perfect
    (a) Existential
    (a) Universal
    (a) None of the above
\vskip 1em
1. Which of the following is impossible for a hash function?
    (a) It never returns `10101` for any message
    (a) It returns `10101` for one message and `1010101` for another
    (a) It always returns the first $x$ bytes of the message
    (a) It returns `10101` for one message and `10101` for another
    (a) None of the above
\vskip 1em
1. All hash functions have which of the following properties?
    (a) Preimage resistance, second preimage resistance, collision resistance
    (a) Compression and extension
    (a) Compression and difficulty of computation
    (a) Compression and ease of computation
    (a) None of the above
\vskip 1em
1. All cryptographic hash functions have which of the following properties in addition to the properties of hash functions?
    (a) The ability use them to encrypt data
    (a) Preimage resistance, second preimage resistance, collision resistance
    (a) The ability to create inverse hashes
    (a) Extension and difficulty of reversal
    (a) None of the above
\vskip 1em
1. If $H(x) = f(g(x)||g(x))$ is collision resistant, which of the following must be true? Select the **most complete answer**.
    (a) $g$ is collision resistant
    (a) Neither $f$ nor $g$ is necessarily collision resistant
    (a) $f$ is collision resistant
    (a) Both $f$ and $g$ are collision resistant
    (a) None of the above
\vskip 1em
1. If we have $H(m)$ that always returns the first $x$ bytes of $m$,
how many of the three properties of cryptographic hash functions are broken?
    (a) 0
    (a) 1
    (a) 2
    (a) 3
    (a) None of the above
\vskip 1em
1. A function defined as $H(x) = 10101$ is a hash function.
    (a) True
    (a) False
\vskip 1em
1. A function defined as $H(x) = 10101$ is a cryptographic hash function.
    (a) True
    (a) False
\vskip 1em
1. A function defined as $H(x) = x$ is a hash function.
    (a) True
    (a) False
\vskip 1em
1. A function defined as $H(x) = x$ is a cryptographic hash function.
    (a) True
    (a) False
\vskip 1em
1. How many hashes do we need to store at any given time in the Rho method of finding collisions?
    (a) 2
    (a) 4
    (a) 20
    (a) 56
    (a) None of the above
\vskip 1em
1. What does a length extension attack allow us to do?
    (a) Create an existential forgery
    (a) Create the hash of a message that we do not explicitly know
    (a) Defeat MD5
    (a) All of the above
    (a) None of the above
\vskip 1em
1. What is the problem with Merkle-Damgard constructions?
    (a) They have limited compression
    (a) They are not really hash functions
    (a) They are susceptible to length extension attacks
    (a) They allow universal forgeries
    (a) None of the above
\vskip 1em
1. Which of the following is considered immune to length extension attacks?
    (a) SHA-1
    (a) SHA-2
    (a) SHA-3
    (a) All of the above
    (a) None of the above
\vskip 1em
1. Which of the following uses a sponge construction?
    (a) SHA-1
    (a) SHA-2
    (a) SHA-3
    (a) All of the above
    (a) None of the above
\vskip 1em
1. A MAC is which of the following?
    (a) A five-tuple $(G,S,V,E,D)$
    (a) A triple of efficient algorithms, $(G,S,V)$
    (a) A triple of efficient algorithms, $(G,E,D)$
    (a) A hash function without a key
    (a) None of the above
\vskip 1em
1. Which of the following is true about a CBC-MAC?
    (a) It has no compression property, unlike HMACs
    (a) It was invented by the CBC for tagging their broadcast data
    (a) It works by taking the entire ciphertext from a block cipher in CBC mode
    (a) It works by taking the last ciphertext block from a block cipher in CBC mode
    (a) None of the above
\vskip 1em
1. If you had a CBC-mode block cipher that produced `101 010 111 010 111 010` and it had a block length of 3 bits,
what would be your CBC-MAC tag?
    (a) `010 111 010`
    (a) `101`
    (a) `101 010 111 010 111 010`
    (a) `010`
    (a) Not enough information
\vskip 1em
1. How does an EMAC work when the key for the original block cipher was $k_1$?
    (a) $E_{k_1}(c_\ell)$
    (a) $E_{k_2}(c_\ell)$
    (a) $E_{k_1}(E^{-1}_{k_2}(c_\ell))$
    (a) $E^{-1}_{k_1}(c_\ell)$
    (a) Either B or C
    (a) Either A or C
\vskip 1em
1. What makes an EMAC better than a CBC-MAC?
    (a) It adds extra security by adding diffusion
    (a) It allows arbitrary length messages
    (a) It has a faster runtime
    (a) It is actually worse because it is less efficient
    (a) None of the above
\vskip 1em
1. What is the preferred method of authenticated encryption?
    (a) Encrypt then MAC
    (a) Encrypt and MAC
    (a) Encrypt then hash
    (a) MAC then encrypt
    (a) None of the above
\vskip 1em
1. How does HMAC work?
    \vskip .2em
    (a) $H\Big((k \oplus \text{opad}) || H\big((m \oplus \text{ipad})\big)\Big)$
    \vskip .2em
    (a) $H\Big((m \oplus \text{opad}) || H\big((k \oplus \text{ipad})\big)\Big)$
    \vskip .2em
    (a) $H\Big((k \oplus \text{opad}) || H\big((k \oplus \text{ipad}) || m\big)\Big)$
    \vskip .2em
    (a) $H\Big((k \oplus \text{opad}) || H\big((k \oplus \text{ipad})\big) || m\Big)$
    \vskip .7em
    (a) None of the above
\vskip 1em
1. In an HMAC, the security is based on what?
    (a) The size of $m$
    (a) The underlying hash function used
    (a) The difference between opad and ipad
    (a) The number of times we run the algorithm
    (a) None of the above
\vskip 1em

For the next 5 questions, consider the following connection encrypted line from \url{rbc.com}:
\begin{center}
\lstinline{TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384, 256 bit keys, TLS 1.2}
\end{center}

98. What is the security protocol?
    (a) TLS 1.3
    (a) RSA
    (a) TLS ECDHE
    (a) TLS 1.2
    (a) None of the above
\vskip 1em
1. What block cipher is used to encrypt the message stream?
    (a) AES with 128 bit key and 256 bit block length
    (a) AES with 256 bit key and 256 bit block length
    (a) SHA with 384 bit block length and 256 bit key length
    (a) AES with 256 bit key and 128 bit block length
    (a) None of the above
\vskip 1em
1. What is the authentication scheme?
    (a) ElGamal public key encryption scheme
    (a) ElGamal signature scheme
    (a) RSA public key encryption scheme
    (a) RSA signature scheme
    (a) None of the above
\vskip 1em
1. What is the mode of operation for the block cipher?
    (a) GCM
    (a) CTR
    (a) CBC
    (a) ECB
    (a) None of the above
\vskip 1em
1. What is used to generate the MAC tag?
    (a) SHA-3 with 384 bit output
    (a) SHA-1 with 384 bit output
    (a) SHA-3 with 84 bit output
    (a) SHA-2 with 384 bit output
    (a) None of the above
\vskip 1em
1. What is a digital signature scheme?
    (a) Three-tuple $(G,S,V)$
    (a) Five-tuple $(G,E,D,S,V)$
    (a) Three-tuple $(G,E,D)$
    (a) A way or securely writing your name on a PDF
    (a) None of the above
\vskip 1em
1. In a DSS, the signing key is \_\_\_\_\_\_\_\_\_\_ and the verifying key is \_\_\_\_\_\_\_\_\_\_?
    (a) private, private
    (a) private, public
    (a) public, public
    (a) public, private
    (a) None of the above
\vskip 1em
1. Which of the following describes the generation algorithm in RSA DSS?
    (a) Take $N = pq$ and find $e, d$ such that $ed = 1 \bmod \phi(N)$
    (a) Generate a random $e, d$
    (a) Take $N$ as some large composite number and find $e, d$ its prime factors
    (a) Generate a random $N$ and take $e = \phi(N)$ and $d = N/e$
    (a) None of the above
\vskip 1em
1. Which of the following describes the signing algorithm in RSA DSS (assume public exponent is $e$ and private is $d$)?
    (a) Compute $M = H(m)$ and $\sigma = M^d \bmod N$
    (a) Compute $M = H(m)$ and $\sigma = M^e \bmod N$
    (a) Compute $M = H(m)$ and $\sigma = M^d \bmod \phi(N)$
    (a) Compute $M = H(m)$ and $\sigma = M^e \bmod \phi(N)$
    (a) None of the above
\vskip 1em
1. Which of the following describes the verifying algorithm in RSA DSS?
    (a) Compute $M = H(m)$ and check if $\sigma^e \equiv M \bmod N$
    (a) Compute $M = H(m)$ and check if $\sigma^d \equiv M \bmod N$
    (a) Compute $M = H(m)$ and check if $\sigma^d \equiv M \bmod \phi(N)$
    (a) Compute $M = H(m)$ and check if $\sigma^e \equiv M \bmod \phi(N)$
    (a) None of the above
\vskip 1em
1. Which of the following is the secret key in ElGamal DSS?
    (a) $x$
    (a) $g, x, p$
    (a) $g, x$
    (a) $g^x$
    (a) None of the above
\vskip 1em
1. Which of the following is the public key in ElGamal DSS?
    (a) $g, g^x, p$
    (a) $g, p$
    (a) $x$
    (a) $g, x, p$
    (a) None of the above
\vskip 1em
1. How do you verify a signature in ElGamal DSS?
    (a) Check if $H(m)^g = (g^x)^rr^s \bmod p$
    (a) Check if $g^{H(m)} = xr^s \bmod p$
    (a) Check if $g^{H(m)} = (g^x)^rr^s \bmod p$
    (a) Check if $g^{H(m)} = x^rr^s \bmod p$
    (a) None of the above
\vskip 1em
1. The security of the ElGamal signature scheme relies on which of the following?
    (a) Computational DH
    (a) Decisional DH
    (a) Factoring large numbers mod $p$
    (a) Discrete log problem
    (a) None of the above
\vskip 1em
1. What is $g$ in the ElGamal signature scheme?
    (a) A generator in $\mathbb{Z}_p^*$
    (a) A large prime number
    (a) A random base
    (a) A random exponent
    (a) None of the above
\vskip 1em
1. How many keys are needed for $n$ parties to communicate with each other using secret key crypto without a PKI?
    (a) $O(n^2)$
    (a) $O(n \log_2 n)$
    (a) $O(n)$
    (a) $O(\log_2 n)$
    (a) None of the above
\vskip 1em
1. How many keys are needed for $n$ parties to communicate with each other using public key crypto without a PKI?
    (a) $O(n^2)$
    (a) $O(n \log_2 n)$
    (a) $O(n)$
    (a) $O(\log_2 n)$
    (a) None of the above
\vskip 1em
1. What does a PKI do?
    (a) Allows you to quickly share secret keys
    (a) Allows you to check which public key belongs to whom
    (a) Allows you to quickly generate public keys
    (a) Allows you to communicate securely without cryptography
    (a) None of the above
\vskip 1em
1. Which of the following is **not** an example of a PKI?
    (a) WoT
    (a) sPKI
    (a) CA
    (a) TLS
    (a) All of the above **are** examples of PKIs
\vskip 1em
1. CAs are generally presented as a hierarchy.
    (a) True
    (a) False
\vskip 1em
1. Self-signing a certificate at the top level of a hierarchy is generally good practice.
    (a) True
    (a) False
\vskip 1em
1. In a web of trust, you generally sign your own keys.
    (a) True
    (a) False
\vskip 1em
1. In a web of trust, other users generally sign your keys.
    (a) True
    (a) False
\vskip 1em
1. How many signatures do you need to trust to accept a key in a web of trust?
    (a) At least 1
    (a) None
    (a) At least $n^2/2$ where $n$ is the number of WoT members
    (a) At least $n/2$ where $n$ is the number of WoT members
    (a) None of the above
\vskip 1em
1. In a $(4,8)$ secret sharing scheme, how many shares do we need to fully reconstruct the secret?
    (a) 8
    (a) 2
    (a) 24
    (a) 4
    (a) None of the above
\vskip 1em
1. What is one caveat of Threshold ElGamal?
    (a) It allows existential forgeries of the secret shares
    (a) It requires a trusted third party
    (a) It has no caveats
    (a) It is much slower than Shamir Secret Sharing for high thresholds
    (a) None of the above
\vskip 1em
1. Which of the following does Shamir Secret Sharing rely on?
    (a) The difficulty of factoring the modulus
    (a) A trusted third party
    (a) Lagrange interpolation at $f(1)$
    (a) Lagrange interpolation at $f(0)$
    (a) None of the above
\vskip 1em
1. What is completeness in a zero knowledge proof?
    (a) The verifier will learn the prover's knowledge
    (a) The prover will not convince the verifier if they are not telling the truth
    (a) The prover will convince the verifier if they are telling the truth
    (a) The verifier does not learn anything about the prover's knowledge
    (a) None of the above
\vskip 1em
1. What is soundness in a zero knowledge proof?
    (a) The verifier will learn the prover's knowledge
    (a) The prover will not convince the verifier if they are not telling the truth
    (a) The prover will convince the verifier if they are telling the truth
    (a) The verifier does not learn anything about the prover's knowledge
    (a) None of the above
\vskip 1em
1. What is zero-knowledgeness in a zero knowledge proof?
    (a) The verifier will learn the prover's knowledge
    (a) The prover will not convince the verifier if they are not telling the truth
    (a) The prover will convince the verifier if they are telling the truth
    (a) The verifier does not learn anything about the prover's knowledge
    (a) None of the above
\vskip 1em
1. What is the binding property in a commitment scheme?
    (a) The statement should remain revealed until the user hides it
    (a) The statement should remain hidden until the user reveals it
    (a) When a user commits to a statement, they cannot change it
    (a) A user cannot change whom they are communicating with after committing to it
    (a) None of the above
\vskip 1em
1. What is the hiding property in a commitment scheme?
    (a) The statement should remain revealed until the user hides it
    (a) The statement should remain hidden until the user reveals it
    (a) When a user commits to a statement, they cannot change it
    (a) A user cannot change whom they are communicating with after committing to it
    (a) None of the above
\vskip 1em
1. A commitment scheme can be build with cryptographic hash functions.
    (a) True
    (a) False
\vskip 1em

<!-- References -->
\clearpage