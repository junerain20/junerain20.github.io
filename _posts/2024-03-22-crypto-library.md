---
layout: distill
title: Crypto-library
description: Commonly used post-quantum cryptography open source libraries
tags: code
categories: pqc
giscus_comments: false
date: 2024-03-22
featured: true
---

# libpqcrypto

`libpqcrypto` is a new cryptographic software library produced by the PQCRYPTO project.

PQCRYPTO, working jointly with many other researchers around the world, submitted 22 proposals to NIST's ongoing post-quantum standardization project. Each submission specifies a family of cryptographic systems, offering various tradeoffs between performance and security. Each submission includes software: a (portable) reference C implementation, and in many cases additional (not necessarily portable) implementations providing better performance (often using assembly language or "intrinsics"). `libpqcrypto` includes software for the following 77 cryptographic systems (50 signature systems and 27 encryption systems) from 19 of the 22 PQCRYPTO submissions:

- BIG QUAKE: `crypto_kem_bigquake{1,3,5}`
- Classic McEliece: `crypto_kem_mceliece{6960119,8192128}`
- CRYSTALS-DILITHIUM: `crypto_sign_dilithium{2,3,4}`
- CRYSTALS-KYBER: `crypto_kem_kyber{512,768,1024}`
- DAGS: `crypto_kem_dags{3,5}`
- FrodoKEM: `crypto_kem_frodokem{640,976}`
- Gui: `crypto_sign_gui{184,312,448}`
- KINDI: `crypto_kem_kindi{256342,256522,512222,512241,512321}`
- LUOV: `crypto_sign_luov{863256,890351,8117404,4849242,6468330,8086399}`
- MQDSS: `crypto_sign_mqdss{48,64}`
- NewHope: `crypto_kem_newhope{512,1024}cca`
- NTRU-HRSS-KEM: `crypto_kem_ntruhrss701`
- NTRU Prime: `crypto_kem_{ntrulpr,sntrup}4591761`
- Picnic: `crypto_sign_picnicl{1,3,5}{fs,ur}`
- qTESLA: `crypto_sign_qtesla{128,192,256}`
- Rainbow: `crypto_sign_rainbow{1a,1b,1c,3b,3c,4a,5c,6a,6b}`
- Ramstake: `crypto_kem_ramstakers{216091,756839}`
- SABER: `crypto_kem_{firesaber,lightsaber,saber}`
- SPHINCS+: `crypto_sign_sphincs{f,s}{128,192,256}{haraka,sha256,shake256}`

`libpqcrypto` collects this software into an integrated library, with

- a unified compilation framework,
- an automatic test framework,
- automatic selection of the fastest implementation of each system,
- a unified C interface following the NaCl/TweetNaCl/SUPERCOP/libsodium API,
- a unified Python interface,
- command-line signature/verification/encryption/decryption tools, and
- command-line benchmarking tools.

`libpqcrypto` also integrates some symmetric-crypto software from SUPERCOP, including the AES-256-CTR stream cipher (an OpenSSL wrapper and a separate implementation from Romain Dolbeau), the Salsa20-256 and ChaCha20-256 stream ciphers (implementations from Daniel J. Bernstein, Romain Dolbeau, Martin Goll, Shay Gueron, Ted Krovetz, Tanja Lange, Andrew Moon, Samuel Neves, and Peter Schwabe), the Poly1305 MAC (implementations from Daniel J. Bernstein, Billy Brumley, Andrew Moon, and Peter Schwabe), the SHA-512 hash function (an OpenSSL wrapper, a separate implementation from Daniel J. Bernstein, and a separate implementation from Thomas Pornin via `sphlib`), portions of the Keccak Code Package (from Guido Bertoni, Joan Daemen, Michaël Peeters, Gilles Van Assche, and Ronny Van Keer), and the SHAKE256 hash function (a KCP wrapper and implementations from David Leon Gil). 

# liboqs

liboqs is part of the Open Quantum Safe (OQS) project, which aims to develop and integrate into applications quantum-safe cryptography to facilitate deployment and testing in real world contexts. In particular, OQS provides prototype integrations of liboqs into protocols like TLS, X.509, and S/MIME, through our OpenSSL 3 Provider and we provide a variety of other post-quantum-enabled demos.

### Supported Algorithms

#### Key encapsulation mechanisms

- **BIKE**: BIKE-L1, BIKE-L3, BIKE-L5
- **Classic McEliece**: Classic-McEliece-348864†, Classic-McEliece-348864f†, Classic-McEliece-460896†, Classic-McEliece-460896f†, Classic-McEliece-6688128†, Classic-McEliece-6688128f†, Classic-McEliece-6960119†, Classic-McEliece-6960119f†, Classic-McEliece-8192128†, Classic-McEliece-8192128f†
- **FrodoKEM**: FrodoKEM-640-AES, FrodoKEM-640-SHAKE, FrodoKEM-976-AES, FrodoKEM-976-SHAKE, FrodoKEM-1344-AES, FrodoKEM-1344-SHAKE
- **HQC**: HQC-128, HQC-192, HQC-256
- **Kyber**: Kyber512, Kyber768, Kyber1024
- **ML-KEM**: ML-KEM-512-ipd (alias: ML-KEM-512), ML-KEM-768-ipd (alias: ML-KEM-768), ML-KEM-1024-ipd (alias: ML-KEM-1024)
- **NTRU-Prime**: sntrup761

#### Signature schemes

- **CRYSTALS-Dilithium**: Dilithium2, Dilithium3, Dilithium5
- **Falcon**: Falcon-512, Falcon-1024
- **ML-DSA**: ML-DSA-44-ipd (alias: ML-DSA-44), ML-DSA-65-ipd (alias: ML-DSA-65), ML-DSA-87-ipd (alias: ML-DSA-87)
- **SPHINCS+-SHA2**: SPHINCS+-SHA2-128f-simple, SPHINCS+-SHA2-128s-simple, SPHINCS+-SHA2-192f-simple, SPHINCS+-SHA2-192s-simple, SPHINCS+-SHA2-256f-simple, SPHINCS+-SHA2-256s-simple
- **SPHINCS+-SHAKE**: SPHINCS+-SHAKE-128f-simple, SPHINCS+-SHAKE-128s-simple, SPHINCS+-SHAKE-192f-simple, SPHINCS+-SHAKE-192s-simple, SPHINCS+-SHAKE-256f-simple, SPHINCS+-SHAKE-256s-simple

Note that for algorithms marked with a dagger (†), liboqs contains at least one implementation that uses a large amount of stack space; this may cause failures when run in threads or in constrained environments. 

# pq-crystals

The "Cryptographic Suite for Algebraic Lattices" (CRYSTALS) encompasses two cryptographic primitives: [Kyber](https://pq-crystals.org/kyber/index.shtml), an IND-CCA2-secure key-encapsulation mechanism (KEM); and [Dilithium](https://pq-crystals.org/dilithium/index.shtml), a strongly EUF-CMA-secure digital signature algorithm. Both algorithms are based on hard problems over module lattices, are designed to withstand attacks by large quantum computers, and have been submitted to the [NIST post-quantum cryptography project](https://csrc.nist.gov/Projects/Post-Quantum-Cryptography).

### Module Lattices

Module lattices can be thought of as lattices that lie between the ones used in the definitions of the [LWE problem](https://dl.acm.org/citation.cfm?id=1568324), and those used for the [Ring-LWE](https://eprint.iacr.org/2012/230) problem. If the ring underlying the module has a sufficiently high degree (like 256), then these lattices inherit all the efficiency of the ones used in the Ring-LWE problem, and additionally have the following advantages, when used in our cryptographic algorithms:

- The only operations required for Kyber and Dilithium for *all* security levels are variants of Keccak, additions/multiplications in Zq for a fixed q, and the NTT (number theoretic transform) for the ring Zq[X]/(X256+1).
  This means that increasing/decreasing the security level involves virtually no re-implementation of the schemes in software or hardware. Changing a few parameters is all that one needs to convert an optimized implementation for one security level into an optimized implementation for a different one.
- The lattices used in Kyber and Dilithium have less algebraic structure than those used for Ring-LWE and are closer to the unstructured lattices used in LWE. It is therefore conceivable that if algebraic attacks against Ring-LWE appear (there are none that we are aware of at this point), then they may be less effective against schemes like Kyber and Dilithium.

### News

- **2019-05-21:** New paper on [Kyber on Cortex-M4](https://eprint.iacr.org/2019/489)
- **2019-03-30:** CRYSTALS round-2 versions are submitted and online.
- **2017-12-30:** CRYSTALS website is online

### Credits

**The design and implementation of Kyber and Dilithium have been supported by**

- the European Commission through the ICT program under contract [ICT-645622 (PQCRYPTO)](https://pqcrypto.eu.org/);
- the European Commission through the ICT program under contract [ICT-644729 (SAFEcrypto)](https://www.safecrypto.eu/);
- the Swiss National Science Foundation through the 2014 transfer ERC Starting Grant CRETP2-166734 (FELICITY);
- the Netherlands Organization for Scientific Research (NWO) through Veni grant 639.021.645 (Cryptanalysis of Lattice-based Cryptography);
- the European Commission through the ERC Starting Grant [ERC-2013-StG-335086 (LATTAC)](http://perso.ens-lyon.fr/damien.stehle/LATTAC.html);
- the European Commission through the ERC Consolidator Grant ERC-2013-CoG-615073 (ERCC);
- the European Commission through the ERC Starting Grant ERC-2018-StG-805031 (EPOQUE);
- the DFG through the Cluster of Excellence 2092 ([CASA](https://casa.rub.de/)).

# 铜锁/Tongsuo

## **项目简介:**

铜锁（Tongsuo）是一个提供现代密码学算法和安全通信协议的开源基础密码库，为存储、网络、密钥管理、隐私计算、区块链等诸多业务场景提供底层的密码学基础能力，实现数据在传输、使用、存储等过程中的私密性、完整性和可认证性，为数据生命周期中的隐私和安全提供保护能力。铜锁诞生于蚂蚁集团并广泛的应用在蚂蚁集团内部以及外部的多种业务当中，提供了TLS、数据存储、国密合规等关键的密码学相关能力，确保了各项业务平稳、安全、合规的运行。铜锁同时还在前沿密码学领域进行了支持，包括隐私计算场景下所需的多种半同态加密算法、零知识证明、轻量级密码算法和协议以及后量子密码学算法等。

铜锁做为国内稀缺的密码学开源项目，填补了相关领域产品的空白，是我国建设国产密码学开源大生态、发展前沿密码学技术的关键一环。同时基于支付宝海量的用户场景，其性能和稳定性也达到了互联网生产级别。

## **功能特性:**

### 技术合规能力

- 符合GM/T 0028《密码模块安全技术要求》的"软件密码模块安全一级"资质
- 符合 GM/T 0005-2021《随机性检测规范》

### 零知识证明（ZKP）

- Bulletproofs Range
- Bulletproofs R1CS

### 密码学算法

- 中国商用密码算法：SM2、SM3、SM4、祖冲之等
- 国际主流算法：ECDSA、RSA、AES、SHA等
- 同态加密算法：EC-ElGamal、Paillier、Twisted-ElGamal等
- 后量子密码学：Kyber、Dilithium等

### 安全通信协议

- 支持GB/T 38636-2020 TLCP标准，即双证书国密通信协议
- 支持RFC 8998，即TLS 1.3 +国密单证书
- 支持QUIC API
- 支持Delegated Credentials功能，基于draft-ietf-tls-subcerts-10
- 支持TLS证书压缩
- 支持紧凑TLS协议*