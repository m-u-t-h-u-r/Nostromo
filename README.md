# Nostromo
**The MUTHUR Application Library & Deployment Catalog**

Nostromo acts as the primary decoupled, external data repository that powers the **[MUTHUR](https://github.com/m-u-t-h-u-r/muthur)** platform. While MUTHUR handles the intelligence, RAG routing, and user interface, Nostromo serves as the strictly-governed "Infrastructure as Data" library containing 2,600+ self-hosted applications and their deployment manifests.

By separating the application library from the core application logic, MUTHUR achieves offline capability, instant local loading (via shallow git clones), and allows the open-source community to contribute to the dataset without altering the core AI engine.

## Repository Architecture
Nostromo is a Semantic Linked Data Catalog. Every level of the directory tree contains an `_index.json` (JSON-LD) file detailing its ontological purpose.

This library is organized into five primary domains:

```text
Nostromo/
├── library/                        # 1. The Core JSON-LD Datastore
│   ├── _index.json                 # Root catalog metadata
│   └── {category}/
│       └── {subcategory}/
│           └── {leaf_node}/        # Mapped using the `about` property with a `DefinedTerm`
│               ├── _index.json     
│               └── {app_name}.json # The standard Schema.org Application metadata
│
├── install/                        # 2. Deployment Manifests
│   ├── _index.json
│   ├── bare_metal/                 # Bash scripts, Ansible Playbooks
│   ├── container/                  # docker-compose.yml, Portainer templates
│   └── vm/                         # Cloud-init templates, OVA references
│
├── assets/                         # 3. Offline Media Cache
│   ├── _index.json
│   ├── icons/                      # Local application icons
│   └── screenshots/                # Application GUIs and UI previews
│
├── schemas/                        # 4. Governance Data Schemas
│   ├── _index.json
│   └── muthur_app_v2.schema.json   # Strict JSON Schema for CI/CD validation
│
└── translations/                   # 5. Internationalization Strings
    ├── _index.json
    └── en_US.json                  # Locale mappings for app descriptions
```

## Contributing & Governance
*(Note: Full contribution guidelines are currently paused while the MUTHUR Category Taxonomy is finalized.)*

All applications added to Nostromo must abide by the MUTHUR Schema governance. 
- Deployment manifests (`docker-compose.yml`, shell scripts) **are never** embedded in the JSON structure. They must be submitted to the `install/` directory.
- The `library/.../{app_name}.json` file acts merely as a pointer to those exact deployment scripts using relative paths.
- Taxonomy categories and IDs must use strict lowercase underscore routing (e.g., `infrastructure_management/`).
- The third-tier `leaf_node` categorization is semantically mapped within the JSON-LD using the Schema.org `about` property with a `DefinedTerm`, ensuring granular taxonomy context is preserved for LLMs.

## Air-Gapped / Offline Usage
Nostromo is designed for high-availability offline homelabs. It is available as a standalone, persistent Docker container via GHCR (`ghcr.io/m-u-t-h-u-r/nostromo-local`). This proxy container serves the library and assets locally, allowing MUTHUR to deploy applications natively via SSH without requiring a connection to GitHub.
