# AES-GCM-SIV Hardware Implementation

## 📋 Overview
High-throughput **Verilog implementation** of the **RFC 8452 AES-GCM-SIV** authenticated encryption algorithm optimized for **FPGA deployment**.

![AES-GCM-SIV Architecture](https://via.placeholder.com/800x400/2d3748/ffffff?text=AES-GCM-SIV+Architecture+Diagram)
*Complete hardware architecture showing parallel AES units and data flow*

## 🚀 FPGA Performance (Xilinx Kintex-7)

### 🔧 **Device**: XC7K160T-FBG676

| Resource | Utilization | Performance Metric | Value |
|----------|-------------|-------------------|-------|
| **LUTs** | 7,950 | **Maximum Frequency** | 330 MHz |
| **FFs** | 8,432 | **Throughput** | 42.2 Gbps |
| **BRAMs** | 97 | **Latency** | 14 cycles |
| **DSPs** | 0 | **Block Size** | 256-bit |

### 📊 **Key Architecture Features**
- **7 parallel AES-256 units** (6 rolled + 1 pipelined)
- **Dedicated PolyVal module** for authentication
- **Two-pass processing** with parallel message handling
- **AXI4-Stream compatible** ready/valid interfaces
- **Nonce-misuse resistant** by design

## 🏗️ Hardware Architecture

### **Core Components**
1. **Key Derivation Unit** (6 rolled AES cores)
   - Generates encryption and authentication keys
   - Processes nonce with counter values

2. **Tag Computation Unit**
   - PolyVal polynomial hash
   - AES encryption for final tag

3. **Encryption Unit**
   - Pipelined AES-CTR mode
   - Uses computed tag as counter

4. **Control State Machine**
   - Manages two-pass algorithm flow
   - Handles data buffering and backpressure

### **Top-Level Interface**
```verilog
module aes_gcm_siv_top (
    input  wire         clk,
    input  wire         rst_n,
    // Data interface
    input  wire [255:0] data_in,
    input  wire         data_valid,
    output wire         data_ready,
    output wire [255:0] data_out,
    output wire         data_out_valid
    // ... control and status signals
);
aes-gcm-siv-fpga/
├── rtl/                    # Verilog source files
│   ├── aes_256_core.v     # AES encryption core
│   ├── polyval_unit.v     # Authentication hash
│   ├── key_derivation.v   # Key generation logic
│   ├── controller_fsm.v   # Main state machine
│   └── aes_gcm_siv_top.v  # Top-level module
├── sim/                   # Testbenches
├── constraints/           # FPGA timing constraints
└── scripts/              # Build scripts
