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
infrasonar upsert-assets assets.yaml -v
```

The script will create a new asset if an asset with the given name cannot be found, otherwise it will apply the changes to the existing asset. Existing labels and/or collectors will _not_ be removed, but a _kind_ will be overwritten if one is given. The properties _kind_, _labels_ and _collectors_ are all optional.

### Token

A token might be included in the yaml file:
```yaml
token: xxxxxx
```

Or, it will be asked in a prompt when starting the script.

> :point_right: Note that a **container token** with **Agent** flags must be used for the _upsert-assets_ action to work!

## Get assets

Get container assets. _(in the example below, 123 is a container Id)_

```bash
infrasonar get-assets 123 -o yaml
```
