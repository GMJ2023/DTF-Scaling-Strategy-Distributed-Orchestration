## 🧩 DTF Scaling Strategy – Distributed Orchestration

**Goal:**  
Scale the Data Transformation Framework (DTF) from a single-VM setup to a distributed, fully parallel architecture that supports hundreds of agencies while preserving transparency and control.

---

### **Current Model**
- Single VM running PowerShell, Node.js and Zoho Catalyst functions  
- Serially processes all agency files and uploads via a single browser session  
- Becoming reliable, but constrained by sequential execution  

---

### **Proposed Model: *Distributed Orchestration***

**Key Components:**

- **Multiple VMs** – Identical DTF environments, each with its own MDA browser session  
- **Orchestrator Service** – Monitors load and routes files dynamically to available VMs  
- **VM Identification** – Each VM reports under a unique name (e.g. `DTF-01`, `DTF-02`, or custom alias) embedded in log and alert messages for full traceability  
- **Load Logic** – Round-robin or least-busy allocation based on active job count  

---

### **Flow Overview**
1. Inbound files arrive in the shared *Dispatch Zone*  
2. The **Orchestrator** assigns each file to an available VM’s *Timesheet* folder  
3. The selected VM processes the file using standard DTF routines  
4. Each VM’s **dedicated browser** performs MDA uploads in parallel  
5. Status updates, alerts and error messages include the VM identifier (e.g. `DTF-03 – Browser Session Timeout`)  
6. Results and logs are consolidated back into shared storage  

---

### **Benefits**
✅ True parallel transformation and upload throughput  
✅ Complete visibility — all alerts traceable to specific VMs  
✅ Simple scaling via identical VM images  
✅ Low engineering overhead; zero disruption to proven DTF logic  
✅ Provides a natural bridge toward a cloud queue–driven model in Catalyst  

---

### **Diagram1:** *Distributed Transformation Architecture*

The Dispatch Zone feeds files to multiple DTF VMs via a central Orchestrator, enabling balanced, scalable processing across identical environments.

![Distribution Illustration](G:\My Drive\.Zoho\Typora Markup\Distribution Illustration.jpg)

This diagram illustrates how the **Dispatch Zone** distributes incoming files evenly to multiple **DTF virtual machines** through a central **Orchestrator**. Each VM runs an identical instance of the DTF environment, processing files independently while maintaining synchronised configuration and logging. This layout enables near-linear scalability — simply add more VMs to increase throughput without altering the core workflow.