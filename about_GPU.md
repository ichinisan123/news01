## 【超わかりやすい！】ワンピースの海軍本部組織で例える、GPUの仕組み - YouTube

The video, titled "【超わかりやすい！】ワンピースの海軍本部組織で例える、GPUの仕組み," explains the structure and data flow of a GPU, primarily focusing on **AMD's RDNA 4 architecture** (using the RX 9070XT as an example), by comparing its organization to a military or naval command structure.

The core purpose of the video is to enhance understanding of how data is processed smoothly within the hardware, allowing the system to fully utilize its potential for high-speed processing.

### I. GPU Definition and Core Philosophy

The video begins by defining the GPU (Graphics Processing Unit) in contrast to the CPU:

*   **Origin and Purpose:** The GPU was invented in 1993 by Jensen Huang (Co-founder of NVIDIA) as an independent chip designed to **accelerate complex, time-consuming processing** that would otherwise burden the CPU.
*   **Specialization (Parallel Execution):** While CPUs are designed to handle any type of processing, the GPU is a specialized chip dedicated to **parallel execution**. Although marketed for graphics processing (hence the 'G' in GPU), it is fundamentally a dedicated chip that pulls out the parallel computation aspects from the CPU.
*   **The Difference Analogized:** A CPU might have about 10 "geniuses," while a GPU contains 10,000 "mediocre soldiers" (Stream Processors or SPs). The CPU *can* do what the GPU does, but it takes significantly longer. The key to the GPU's speed is **organization and coordination** among the many parallel workers, managed by various ranks of commanders.

### II. GPU Architecture: The Military Hierarchy

The video breaks down the GPU's internal structure using military ranks, starting from the lowest unit (the soldier) and moving up the chain of command.

| Military Rank/Analogy | AMD Unit (RDNA 4 Focus) | Function/Notes |
| :--- | :--- | :--- |
| **Soldiers (Kaihei)** | **Stream Processor (SP)** | The basic unit of calculation, capable of one job. Known as CUDA Cores (NVIDIA) or Execution Units (Intel EU). |
| **Squad/Platoon** | **SIMD 32 Unit (Vector Unit)** | 32 SPs (32 threads) aggregated together. Handles vector calculations (multi-dimensional arrays). Two SIMD 32 units (64 people/threads) are managed together. |
| **Specialists** | **Scalar Unit** | Performs calculations common to all threads (like address processing) once, so results can be shared efficiently across all Vector Units. |
| **Company/Major** | **Compute Unit (CU)** | A combined unit containing two Vector Units, a Scalar Unit, a Wave Scheduler (the commander), and additional specialized units (TLU, Matrix Accelerator). |
| **Colonel/Lieutenant Colonel** | **Work Group Processor (WGP)** | Combines two CUs into one execution unit. This commander decides how to allocate local shared memory and tasks to the CUs. |
| **General/Marshal** | **Shader Engine** | Holds the authority of a general; RDNA 4 (Navi 48) has four Shader Engines. These commanders give operational direction to the WGPs. |
| **Fleet Admiral (Gensui)** | **Command Processor** | Receives commands (job instruction sheets) from the CPU/driver (via the PCI bus) and creates a plan for which Shader Engine handles which job. |

### III. Data Flow: Commands from the Top Down

Data processing starts when a game or application sends commands (job instructions) via the CPU and driver to the GPU's **Command Processor** (Fleet Admiral).

1.  The Command Processor reads the instructions and distributes the workload among the **Shader Engines** (Generals).
2.  Shader Engines assign jobs and sequences to the **WGPs** (Colonels), who act as the actual implementation unit.
3.  The WGP manages its two CUs, determining if they should run simultaneously and how caches are used.
4.  Inside the CU, the **Wave Scheduler** (the lowest commander) determines how to process threads and which units (Vector Units, Matrix Accelerators, etc.) will perform the work. The collective instruction given to these units is called a **Wave** (or Warp in NVIDIA terminology).
5.  Tasks are divided and processed in parallel. The speed is heavily dependent on the competence of these internal schedulers.

### IV. Specialized Units (RDNA 4 Enhancements)

The RDNA 4 architecture features several expanded and specialized components within the CU:

*   **Matrix Accelerator / AI Accelerator:** This is a crucial specialist unit that executes **WMMA** (Wave Matrix Multiply Accumulate) instructions. It is highly proficient at **matrix calculation**.
    *   **Function:** Matrix calculations are essential for graphics, physical simulations, and AI. The Matrix Accelerator processes large matrices quickly by dividing them into smaller blocks.
    *   **Advancements:** RDNA 4 improves upon RDNA 3 by being designed to handle **sparse matrices** (matrices containing zeros) more efficiently, preventing wasted computation on multiplying by zero.
    *   **Nomenclature:** This unit is the same as NVIDIA’s Tensor Core and Intel’s XMX unit, though companies often use the term "AI Accelerator" for marketing purposes.
*   **TLU (Transcendental Logic Unit):** Handles complex functions like cosine and logarithms ("transcendental" means "transcendent").
*   **Ray Accelerator:** A separate detachment assigned mainly to graphics work, specifically the intersection calculations needed for ray tracing (BVH traversal). This is equivalent to NVIDIA's RT Core.

### V. Caveats on Comparison

The video emphasizes that comparing specifications like the number of CUs, SPs, or Streaming Multiprocessors (SMs) across different manufacturers (AMD vs. NVIDIA) or even across different generations of the same architecture (RDNA 3 vs. RDNA 4) is **meaningless for performance comparison**.

*   **Design Changes:** Because architectures evolve and expand (e.g., RDNA 4 added the Matrix Accelerator and TLU alongside the original 64 threads), a CU from one generation performs fundamentally different work than a CU from the next generation.
*   **Marketing (Romance):** These numbers are often included in spec sheets because they offer a sense of scale and "romance," but should not be taken literally for performance comparisons.
*   **Design Philosophy:** The differences between AMD and NVIDIA are rooted in design philosophy and sales strategy, rather than pure superiority. NVIDIA tends to target professionals more heavily, while AMD targets consumers, though this gap is narrowing.

Understanding these internal mechanisms allows users to better assess performance benchmarks, avoid making purchasing decisions based only on price or reputation, and develop their own criteria for selecting hardware.

***

The complexity of the GPU organization, with specialized units and layered command structures, is similar to a **highly coordinated, multi-layered military operation**. Just as a small military unit relies on specialized roles (infantry, logistics, intelligence) and clear communication between ranks (squad leaders, colonels, generals) to successfully complete a mission, the GPU relies on the specialized CU units and the schedulers to ensure millions of threads are processed efficiently and in parallel.
