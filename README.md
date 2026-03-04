# Nostromo
**Deployment & Configuration File Library for M.U.T.H.U.R**

Nostromo acts as the central repository for all functional deployment payloads, configuration templates, and orchestration files referenced by the **[MUTHUR](https://github.com/m-u-t-h-u-r/muthur)** Application Taxonomy engine. 

To maintain a clean schema, the MUTHUR JSON taxonomy operates on a referential decoupled architecture—it points to the exact URLs housed in this repository rather than embedding massive YAML payloads directly into the application metadata.

## Repository Structure
This library is organized by deployment methodology and application:

```text
Nostromo/
├── install/
│   ├── bare_metal/
│   │   └── {app_name}/          # Bash scripts, Ansible Playbooks, APT dependencies
│   ├── container/
│   │   └── {app_name}/          # docker-compose.yml, Helm Charts, Portainer templates
│   └── vm/
│       └── {app_name}/          # Cloud-init templates, OVA download references
├── config/                      # Default application configurations
└── scripts/                     # Reusable utility orchestration scripts
```

## Contributing
When MUTHUR detects or interacts with a homelab application, it retrieves the necessary deployment or troubleshooting instructions from this repository via GitHub raw file links. 
When adding a new application to the MUTHUR taxonomy:
1. Create the appropriate `{app_name}` directory under the correct `install/` method inside this repo.
2. Commit your deployment artifacts (e.g., `docker-compose.yml`).
3. Take the raw URL of the committed file and embed it into the MUTHUR application JSON schema (in `G:\Repos\M-U-T-H-U-R\Conversations\JSON_Data\...`).
