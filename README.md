# AES-GCM-SIV
AES-GCM-SIV Hardware Implementation (RFC 8452)

This repository contains the hardware design files and supporting material used in the paper:

First High-Throughput RFC 8452 AES-GCM-SIV Hardware Implementation with Performance Comparison to AES-GCM
Bilal Maqbool, Hassaan Ahmed, Ali Ashraf, Muhammad Imran

The work presents a high-throughput, RFC 8452–compliant hardware implementation of AES-GCM-SIV, along with a fair performance and resource comparison against a high-performance AES-GCM baseline.

Description

AES-GCM-SIV is a nonce-misuse-resistant authenticated encryption scheme standardized in RFC 8452. Unlike AES-GCM, it remains secure even when nonces are reused.

This repository includes the actual RTL and evaluation artifacts used in the paper, covering both FPGA and ASIC implementations.
