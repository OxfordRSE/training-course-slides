---
class: lead
highlighter: shiki
lineNumbers: true
transition: slide-left
title: "High-Performance Computing (HPC)"
---

---
layout: two-cols
---

# Fun Fact
The MareNostrum supercomputer in Barcelona is housed in a neo-Gothic chapel.  
It was featured in Dan Brown’s *Origin* (2017).

::right::
<div class="h-full w-full flex items-center justify-center">
  <img src="./img/marenostrum.jpg" class="object-cover h-full w-full"  alt="Photo of MareNostrum supercomputer in the neo-gothic chapel Torre Girona"/>
</div>

---

# Computing Challenges in Research

Research often requires more computing power than personal computers can provide.  
Parallel computing and high-memory systems can help meet these needs.

---

# Key Computing Challenges

- Tasks involving repeated, independent calculations
- Handling and analyzing large datasets
- Simulations and calculations increasing in complexity and size

---

# High-Performance Computing Solutions

- **Parallel Computing:** Run independent tasks simultaneously
- **High-memory systems:** Handle and analyze larger datasets
- **Distributed Computing:** Distribute calculations across multiple computers

---

# Connecting to Remote HPC Systems

- Use **Secure SHell (SSH)** via Command-Line Interface (CLI)
- Example:
  ```bash
  ssh math0842@arc-login.arc.ox.ac.uk
  ```

* Graphical SSH clients: PuTTY, MobaXterm
* Use SSH keys for security (private/public key pair)

---

# Storage Options in HPC Systems

HPC systems provide multiple storage areas with different purposes:

| Storage     | Path                         | Use                    | Notes                  |
|-------------|------------------------------|------------------------|------------------------|
| **Home**    | `/home/username`             | Personal files         | 15GB quota             |
| **Data**    | `/data/projectname/username` | Shared project storage | 5TB quota              |
| **Scratch** | `$SCRATCH`                   | Temporary job files    | Deleted after job exit |
| **Tmpdir**  | `$TMPDIR`                    | Local node storage     | Deleted on exit        |

---

# Roles of Nodes in an HPC Cluster

* **Login node:** Access point for SSH sessions
* **Compute node:** Runs computational workloads
* **Transfer node:** For large data transfers to/from cluster

---

# Modules

HPC clusters use **modules** to manage software and dependencies.

```bash
remote$ module avail
remote$ module list
remote$ module load python
```

Advantages:

* Manage multiple versions
* Avoid software conflicts
* Simplify complex environments

---

# Scheduler

Schedulers allocate resources and manage jobs.
Example: **SLURM** (used on ARCHER2 and ARC)

Common partitions:

| Partition   | Max Runtime |
|-------------|-------------|
| short       | 12 hrs      |
| medium      | 48 hrs      |
| long        | no limit    |
| devel       | 10 min      |
| interactive | 24 hrs      |

Example job script:

```bash
#!/bin/bash
#SBATCH --nodes=2
#SBATCH --ntasks-per-node=4
#SBATCH --time=00:10:00
#SBATCH --partition=devel

module load mpitest
mpirun mpihello
```

Submit and check jobs:

```bash
$ sbatch example-job.sh
$ squeue -u $USER
```

---

# Considering HPC

* Shared resources = higher cost efficiency
* Learn job scheduling and module systems
* Distributed-memory programs are more complex
* Balance your own time against compute runtime

---

# ARC at Oxford

* University of Oxford HPC facility
* Clusters: **arc** and **htc**
    * CPU and GPU nodes (on *htc*)
* Scheduler: **SLURM**
* Login:

  ```bash
  ssh -Y username@arc-login.arc.ox.ac.uk
  ```

---

---
layout: iframe-right

url: https://arc-user-guide.readthedocs.io/en/latest/
---

Docs: <https://arc-user-guide.readthedocs.io/en/latest/>

---

---
layout: fact
---
A fun fact on this slide

---

