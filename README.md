# Network as Code (NaC) for Catalyst Center - Cisco Validated Multi-Vertical Automation 

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
| Folder | Focus | Representative Use Cases |
|--------|-------|--------------------------|
| nac_common | Baseline global + site building blocks consumable by all verticals | Global hierarchy, IP pools, servers, credentials, roles/users, devices provision, fabric deployment,  cleanup orchestration |
| nac_healthcare_sda | Healthcare End-to-end SDA deployment and operation focus with scaled virtual networks, scaled anycast gateway and scaled remote clinic sites | Day0/1 fabric build, day1 remote site expansion, bulk host onboarding, bulk fabric VN and gateway deployment |
| nac_financial_sda | Financial sector focus with operational stability & lifecycle | Image lifecycle (download→golden→distribute→activate), Upgrade sequencing, multi‑site patterns,device (re)provision, static host onboarding, notifications|
| nac_ites_sda | IT-Enabled Services SDA rollout and opertaion tasks | Multi‑site fabric enablement, baseline config reuse, expansion & cleanup workflows|

Each vertical README provides:  
- Topology diagram  
- Compatibility matrix (CatC, Ansible collection, Python SDK)  
- Project index (inputs, playbooks, cleanup)  
- Use case orchestration maps (ordered automation steps)

### When to Use Which
- Start in `nac_common` to align credentials, roles, image tags, global pools.
- Pick a vertical (`healthcare`, `financial`, `ites`) matching your domain for tailored topology, scale, sequencing, and deployment details.
- Reuse and extend patterns: copy a vertical skeleton and swap its input YAML for a new domain.


## Core Concepts
- Declarative YAML input files under `catc_configs/`
- Mapped execution flows under `usecase_maps/`
- Cleanup automation under `catc_delete_configs/`
- Driven by Ansible Collection: `cisco.dnac`
- Modular: compose site + global configs per vertical

## Quick Start
```bash
git clone https://github.com/DNACENSolutions/NetworkasCode_CVPs.git
cd NetworkasCode_CVPs
# (Optional) inspect nac_common for reusable patterns
cd nac_healthcare_sda/NaC_1_0_Healthcare_SDA   # or another vertical
source ./setup.sh    # sets Python venv, installs collection + SDK
python3 scripts/run_playbooks.py   # guided execution (validate / execute)
```

## Typical Workflow
1. Review vertical README (select your domain)  
2. Adjust YAML inputs (credentials, sites, pools, images, roles,devices, fabrics)  
3. Validate via runner script (syntax + dependency readiness)  
4. Execute orchestration ( tasks as defined in usecase maps)  
5. (Optional) Run cleanup mappings for teardown / rollback  

## Reuse From nac_common
Leverage `nac_common` to:
- Centralize credentials & role definitions
- Share global IP pools / servers / network hierarchy
- Standardize fabric creation, device onboard and host onboard
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