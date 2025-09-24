# NetworkasCode_CVPs
# Catalyst Center Network as Code (NaC) – Multi-Vertical Automation

High-level Network as Code (NaC) framework for automating Cisco Catalyst Center (CatC) workflows using Ansible across multiple vertical solution packs.

## Repository Structure
```
NetworkasCode_CVPs/
├── nac_common/          # Reusable core (global + site) configuration building blocks
├── nac_healthcare_sda/  # Healthcare SDA vertical use cases & inputs
├── nac_financial_sda/   # Financial SDA vertical use cases & inputs
├── nac_ites_sda/        # IT/ES (Enterprise Services) SDA vertical (structure similar)
├── scripts/             # (If present) shared helper scripts
├── setup.sh             # Environment bootstrap (Python SDK + Ansible collection)
└── requirements.txt     # Python dependencies
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

## Technology Coverage (Examples)
- SDA Fabric sites, zones, VNs, transit, edge onboarding
- LAN Automation (PnP to fabric readiness)
- Image lifecycle (download → golden → distribute → activate)
- Host onboarding (static)
- Device provisioning & reprovisioning
- Events & notifications (email destinations)
- Roles, users, credentials
- Inventory & compliance (where applicable)

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