[![CI](https://github.com/infrasonar/toolkit/workflows/CI/badge.svg)](https://github.com/infrasonar/toolkit/actions)
[![Release Version](https://img.shields.io/github/release/infrasonar/toolkit)](https://github.com/infrasonar/toolkit/releases)


## Installation

Using pip:

```shell
pip install infrasonar
```

Or, clone this project and use the setup

```shell
python setup.py install
```

## Upsert assets

Create a _yaml_ file, for example: `assets.yaml`

```yaml
labels:
  windows: 3257

configs:
  tcp:
    checkCertificatePorts: [443, 995, 993, 465, 3389, 989, 990, 636, 5986]

assets:
- name: foo.local
  kind: Windows
  labels: ["windows"]
  collectors:
  - key: lastseen
  - key: ping
  - key: tcp
    config: tcp
  - key: wmi
```

Next, use the following command to upsert the assets: _(-v for verbose output)_

```bash
infrasonar -v upsert-assets assets.yaml
```
