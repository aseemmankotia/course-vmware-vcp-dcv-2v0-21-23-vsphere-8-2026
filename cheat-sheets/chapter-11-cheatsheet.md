## Ch.11 Cheat Sheet — Security, Roles, vLCM, esxtop

### Roles & Permissions
| Item | Rule |
|---|---|
| System roles | Administrator, Read-Only, No Access — cannot edit/delete |
| Sample roles | Templates (e.g., VM Power User) — clone, don't edit directly |
| Custom roles | Clone sample or build from scratch to match least-privilege need |
| Propagation | 'Propagate to children' checked by default; controls downward inheritance |
| Precedence | Permission defined **directly on an object** always overrides one inherited from a parent |
| Multiple groups conflict | At same object level, if user is in two groups with conflicting roles, deny/No Access typically wins — but explicit local user assignment beats group inheritance |

### Certificate Management
| Mode | Behavior |
|---|---|
| VMCA (default) | VMCA auto-issues/renews all machine & solution-user certs |
| VMCA as subordinate CA | Enterprise root signs VMCA's cert; VMCA still auto-issues, compliant chain |
| Custom mode | All certs replaced manually per service — no auto-renewal |
| Thumbprint mode | Legacy/deprecated — avoid in new deployments |

### vLCM (vSphere 8)
| Concept | Detail |
|---|---|
| Desired image | ESXi base image + vendor add-on + firmware/driver add-on + components |
| Cluster mode | Image-managed OR baseline-managed — never both |
| Hardware compatibility | Validated against HCL/Hardware Support Manager before remediation |
| Baselines | Legacy, per-host patch/extension attach-and-remediate model |

### esxtop Key Counters
| Counter | Meaning | Exam Threshold/Note |
|---|---|---|
| %RDY | CPU ready time per vCPU | >5-10% sustained per vCPU = contention |
| %CSTP | Co-stop (SMP VM waiting for all vCPUs scheduled together) | High = reduce vCPU count |
| DAVG | Device (physical array) latency | High = storage array bottleneck |
| KAVG | VMkernel queue latency | High w/ low DAVG = queue depth exceeded in ESXi |
| GAVG | Guest-observed latency | GAVG = DAVG + KAVG |

### Troubleshooting Escalation
| Log | Purpose |
|---|---|
| vpxd.log | vCenter Server service |
| vpxa.log | Host agent ↔ vCenter communication |
| hostd.log | ESXi host management agent |
| vmkernel.log | Kernel, storage, network events |
| `vm-support` | Basic config/log bundle |
| `vm-support -p -d <sec> -i <sec>` | Adds live esxtop performance snapshot to bundle |
