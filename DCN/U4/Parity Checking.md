
### **What is Parity Checking in the Data Link Layer?**

**Parity checking** is an **error detection technique** used at the Data Link Layer (Layer 2) to identify errors in transmitted data. It ensures that the transmitted data has maintained its integrity during transmission. Parity checking involves adding a **parity bit** to the data being transmitted, which helps detect if the number of bits that have changed during transmission is odd or even.

There are two types of parity checking:
1. **Even Parity**: The parity bit is set so that the total number of 1s in the data, including the parity bit, is even.
2. **Odd Parity**: The parity bit is set so that the total number of 1s in the data, including the parity bit, is odd.

### **How Parity Checking Works:**

1. **Sender Side**:
   - The sender calculates the parity bit for a block of data.
   - For **even parity**, the parity bit is chosen so that the number of 1s in the block (data + parity bit) is even.
   - For **odd parity**, the parity bit is chosen so that the number of 1s in the block (data + parity bit) is odd.
   - The sender then transmits the data along with the parity bit to the receiver.

2. **Receiver Side**:
   - Upon receiving the data and the parity bit, the receiver checks the number of 1s in the received data (including the parity bit).
   - If the parity (even or odd) matches the expected value, the data is assumed to be error-free.
   - If the parity is incorrect (i.e., it does not match the expected even or odd parity), an error is detected, indicating that one or more bits have been altered during transmission.

### **Example of Even Parity Checking**:

Let’s assume we are transmitting a 7-bit data sequence, `1011001`.

#### **Step 1: Calculate Parity (Even Parity)**
- Count the number of `1s` in the data: `1011001` has **4 ones**.
- For even parity, the number of `1s` (including the parity bit) should be **even**. Since the count is already even (4), the parity bit is set to `0` (no change is needed).

So, the transmitted data becomes:  
**Data with parity bit: `10110010`** (7-bit data + 1 parity bit).

#### **Step 2: Transmission**
- The data `10110010` is transmitted.

#### **Step 3: Parity Check at Receiver**
- The receiver checks the number of `1s` in the received data: `10110010` has **4 ones**.
- Since the number of 1s is **even** and we are using even parity, no error is detected.

### **Example of Odd Parity Checking**:

For odd parity, let's take the same 7-bit data, `1011001`.

#### **Step 1: Calculate Parity (Odd Parity)**
- The number of `1s` in `1011001` is **4**.
- For odd parity, the total number of 1s (including the parity bit) must be **odd**. Since 4 is even, the parity bit is set to `1` to make the number of 1s odd.

So, the transmitted data becomes:  
**Data with parity bit: `10110011`** (7-bit data + 1 parity bit).

#### **Step 2: Transmission**
- The data `10110011` is transmitted.

#### **Step 3: Parity Check at Receiver**
- The receiver checks the number of `1s` in the received data: `10110011` has **5 ones**.
- Since the number of 1s is odd and we are using odd parity, no error is detected.

### **Limitations of Parity Checking**:
- **Cannot detect all errors**: Parity checking can only detect an **odd number of bit errors**. If two or any even number of bits are altered during transmission, the parity remains unchanged, and the error goes undetected.
- **No error correction**: Parity checking can only detect errors but **cannot correct** them.

### **Applications of Parity Checking**:
- **Serial communication**: Used in basic serial communication protocols.
- **RAM (memory error detection)**: Parity bits are sometimes used in memory systems to detect single-bit errors.
