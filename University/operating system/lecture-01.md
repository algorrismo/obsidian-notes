# Computer system organization

Computer-System Operation describes how the CPU, memory, and device controllers work together to execute programs. All components communicate through a common system bus that allows data transfer and access to shared memory. The CPU and input/output devices can operate concurrently, ensuring efficient execution of tasks.

# Diagram Explanation (how to explain in exam) 🧩

In the diagram, the **CPU**, **memory**, and different device controllers are connected through a **system bus**. The disk controller connects storage devices, the USB controller connects input devices like keyboard and mouse, and the graphics adapter connects the monitor. All these components communicate through the system bus to share data with memory. The CPU executes instructions while device controllers manage input and output operations. The CPU and I/O devices can work at the same time, which is called concurrent execution, but they share the same memory for data access.

---

# Interrupt-Driven I/O Cycle (Simple Idea) 🧠

An **interrupt** is a signal sent to the CPU to tell:

> “Stop for a moment, something needs attention!”

Example:  
You are studying 📖 → phone rings 📞 → you stop → answer → continue studying.  
Phone call = interrupt.

---

# Step-by-step Diagram Explanation 🔄

Follow the numbers in the diagram:

### Step 1

Device driver requests the CPU to start an Input/Output operation.

### Step 2

CPU sends request to the I/O controller to start the device operation.

### Step 3

When the device finishes its task (input ready / output complete / error), it sends an **interrupt signal** to CPU.

### Step 4

CPU detects the interrupt and pauses current work.

### Step 5

CPU runs the **interrupt handler** (special program) to process the data.

### Step 6

After handling the interrupt, CPU returns to the previous task.

### Step 7

CPU continues normal execution.

---
