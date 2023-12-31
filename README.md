# Synapse IOC Parser
This Synapse Rapid Power-up adds support for using the `iocparser.com` service for quick ingestion of IOCs into Synapse from raw text and URLs.

**This extension is in WIP stage**

## Usage
There are 2 commands available: 
### `ex.iocparser.url`
For a given inbound `inet:url` fetches and parses IOCs from the page, creating a `media:news` node as well as the following other nodes:
- `inet:fqdn`
- `inet:ipv6`
- `inet:ipv4`
- `inet:email`
- `file:base`
- `inet:url`
- `hash:md5`
- `hash:sha1`
- `hash:sha256`
- `inet:asn`
- `it:sec:cve`
- `inet:mac`

Optionally takes a `--yield` argument to yield the generated nodes instead of the inbound `inet:url`. 

#### Example:
`[inet:url=https://pylos.co/2022/11/23/detailing-daily-domain-hunting/] | ex.iocparser.url --yield`

---
### `ex.iocparser.text`
Scrapes text provided as a command line argument, creates an `it:exec:query` node and scrapes the same types of IOCs as `ex.iocparser.url`

##### Example:
`ex.iocparser.text "example.com 1.1.1.1"`

---
## Installation
The easiest way to use this Power-Up is to load the JSON package into the Cortex by running: 

`pkg.load --raw "https://raw.githubusercontent.com/EXC3L-ONE/synapse-iocparser/main/synapse_iocparser.json"`

Alternatively, you can also clone this repo, and load the package via `python -m synapse.tools.genpkg` (see reference in Synapse docs [here](https://synapse.docs.vertex.link/en/latest/synapse/userguides/syn_tools_genpkg.html#building-the-example-package))
