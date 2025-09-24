# NetworkasCode_CVPs
# Catalyst Center Network as Code (NaC) – Multi-Vertical Automation

High-level Network as Code (NaC) framework for automating Cisco Catalyst Center (CatC) workflows using Ansible across multiple vertical solution packs.

## Repository Structure
```
NetworkasCode_CVPs/
├── nac_common/          # Reusable core (global + site) configuration building blocks
├── nac_healthcare_sda/  # Healthcare SDA vertical use cases & inputs
├── nac_financial_sda/   # Financial SDA vertical use cases & inputs
└── nac_ites_sda/        # IT-Enabled Services SDA vertical use cases & inputs
```

## Verticals Overview
| Folder | Focus | Key Artifacts |
|--------|-------|---------------|
| nac_common | Baseline/global config inputs (images, credentials, roles, IP pools), shared cleanup, host inventory patterns | `catc_configs/`, `catc_delete_configs/`, reference samples |
| nac_healthcare_sda | End-to-end SDA campus build & operations (day‑0/1/2), host onboarding, fabric provisioning | `usecase_maps/`, healthcare topology, staged automation flows |
| nac_financial_sda | Image lifecycle (download/tag/distribute/activate), fabric device (re)provisioning, static hosts, notifications | Upgrade sequencing, multi‑site patterns |
| nac_ites_sda | (Similar pattern) SDA fabric rollout & operational tasks for ITES vertical | Standardized YAML inputs & playbook orchestration |

Each vertical README provides:  
- Topology diagram  
- Compatibility matrix (CatC, Ansible collection, Python SDK)  
- Project index (inputs, playbooks, cleanup)  
- Use case orchestration maps (ordered automation steps)

// ...existing code...
## Verticals Overview

| Folder | Primary Purpose | Representative Use Cases | Key Inputs / Artifacts |
|--------|-----------------|--------------------------|------------------------|
| `nac_common` | Shared global + site building blocks consumed by all verticals | Global hierarchy, IP pools, servers, credentials, roles/users, image tagging, cleanup orchestration | `catc_configs/`, `catc_delete_configs/`, sample inventories, role/user/image YAML |
| `nac_healthcare_sda` | Healthcare SDA campus build with patient‑care workflow emphasis | Day0/1 fabric build, site provisioning, host onboarding, fabric VNs/zones, gateway deployment | `usecase_maps/`, healthcare topology diagram, fabric + host YAML bundles |
| `nac_financial_sda` | Financial sector focus with operational stability & lifecycle | Image lifecycle (download→golden→activate), device (re)provision, static host onboarding, notifications | Upgrade sequencing maps, image policy YAML, provisioning inputs |
| `nac_ites_sda` | IT / Enterprise Services generalized SDA rollout | Multi‑site fabric enablement, baseline config reuse, expansion & cleanup flows | Standardized SDA site YAML, orchestration maps, cleanup sets |

### When to Use Which
- Start in `nac_common` to align credentials, roles, image tags, global pools.
- Pick a vertical (`healthcare`, `financial`, `ites`) matching your domain for tailored topology, sequencing, and examples.
- Reuse and extend patterns: copy a vertical skeleton and swap its input YAML for a new domain.

### Composition Model
Global (from `nac_common`) + Vertical-Specific (from chosen folder) → Orchestrated via `usecase_maps` → Optional teardown via vertical or common cleanup sets.
//



## Core Concepts
- Declarative YAML input files under `catc_configs/`
- Mapped execution flows under `usecase_maps/`
- Cleanup automation under `catc_delete_configs/`
- Driven by Ansible Collection: `cisco.dnac`
- Extended tasks using `dnacentersdk` where needed
- Modular: compose site + global configs per vertical

## Quick Start
```bash
git clone https://github.com/DNACENSolutions/NetworkasCode_CVPs.git
cd NetworkasCode_CVPs
# (Optional) inspect nac_common for reusable patterns
cd nac_healthcare_sda/NaC_1_0_Healthcare_SDA   # or another vertical
./setup.sh    # sets Python venv, installs collection + SDK
python3 scripts/run_playbooks.py   # guided execution (validate / execute)
```

## Typical Workflow
1. Review vertical README (select your domain)  
2. Adjust YAML inputs (credentials, sites, pools, images, roles)  
3. Validate via runner script (syntax + dependency readiness)  
4. Execute orchestration (parallel + sequential tasks as defined)  
5. (Optional) Run cleanup mappings for teardown / rollback  

## Reuse From nac_common
Leverage `nac_common` to:
- Standardize golden image tagging
- Share global IP pools / servers
- Centralize credentials & role definitions
- Apply consistent cleanup logic

## Extending
To add a new vertical:
1. Copy a vertical skeleton
2. Define topology + compatibility
3. Author YAML under `catc_configs/`
4. Map ordered flows in `usecase_maps/`
5. (Optional) Add cleanup set
6. Document in new README

## References
- Cisco Catalyst Center Ansible Collection: cisco.dnac  
- Python SDK: dnacentersdk  

## Contributing
Issues / PRs welcome. See individual vertical READMEs for deep details.

## License
See LICENSE (or vertical-specific notice if present).

---
For detailed operational sequences: open the README inside