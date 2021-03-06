# GitHub Action: gh-action-spdx-sbom-generator

This actions generates sbom file from a package file based on language ecosystem.

## Workflow setup

```yaml
# workflow name
name: Generate sbom file

# on events
on:
  release:
    types:
        - created

# workflow tasks
jobs:
  generate:
    name: Generate sbom file
    runs-on: ubuntu-latest
    steps:
      - name: Checkout the repository
        uses: actions/checkout@v2
      - name: gh-action-spdx-sbom-generator
        uses: niravpatel27/gh-action-spdx-sbom-generator@v1.0.0
        with:
            version: '0.0.9'   
      - name: Check if sbom file generated
        run: |
          if [ ! -f "bom-go-mod.spdx" ]; then
            echo "::error::bom-go-mod.spdx is missing. Must generate using the spdx-sbom-generator cli."
            exit 1
          else
             echo "Success!"            
          fi   
```
