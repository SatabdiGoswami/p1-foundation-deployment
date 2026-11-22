# Project 1 Handover

## Status

Local packaging, Kubernetes deployment, Argo CD sync, app checks, and Loki correlation were verified on 2026-11-21.
The prepared classroom deployment, peer review, controlled failure exercise, peer reproduction, and individual
demonstration were not completed. Team name and operators were not recorded. Local results below are not classroom or
BP deployment evidence.

## Source and Changes

* Supplied source: `../code/app`, release `foundation-observe-a`.
* Source comparison: all supplied app files match except `wwwroot/client.json`, which P1 configures separately.
* Client setting: changed from `80 ms / 0 retries` to `450 ms / 0 retries`. A written W1.10 justification was not
	recorded.
* Source commit or aggregate checksum: not recorded.
* Team-owned files: `Containerfile`, `runtime.env`, `app/wwwroot/client.json`, `configuration/app/resources.yaml`, and
	`local-classroom/` local-practice manifests and documentation.

## Prerequisites and Versions

* .NET SDK used locally: `10.0.303`; `app/global.json` requests `10.0.100` and allows feature roll-forward. The P1
	classroom preparation specifies `10.0.401`.
* Podman VM: Hyper-V, 4 CPUs, 6 GiB RAM. Podman version was not captured.
* Local Kubernetes: Kind `0.33.0`, Kubernetes node `v1.37.0`, kubectl client `v1.36.1`.
* Local GitOps tools: Argo CD CLI/server `v3.6.2`, Helm `v3.22.1`.
* Classroom namespace, session variables, and kubeconfig context: unavailable in this workspace; classroom steps were
	not run.

## Build and Image

The supplied image build is recorded as successful. Reproduction commands from the P1 guide:

```bash
dotnet publish app/Foundation.csproj -c Release -o publish --nologo
podman build --pull=never -f Containerfile -t localhost/p1-local:foundation-a .
podman image inspect localhost/p1-local:foundation-a --format '{{.Id}}'
```

* Local image label: `localhost/p1-local:foundation-a`.
* Local image config ID: `474c4137be468ebaf94dbbf978d8dce52394250b5287b49dc933ef17c802c17a`.
* Original container ID in the prior local evidence: `72eb45c8e4c3a90ff5bd9b9f6a044818735c9530f0a886a2a9e4852c8fd90309`.
* The Kind node's imported image config ID was verified to match the local image ID. A facilitator classroom import was
	not performed.

## Configuration and Revisions

* Public environment: `LAB_ENV=workshop-blue`.
* Browser client: `deadlineMs=450`, `retries=0`; written justification from W1.10 was not recorded.
* Local Argo source commit: `b58a081ba2d39243e1ef7d0b92be307794ad3f44`.
* Local Argo Application: `p1-foundation-local`; synced to `b58a081` and Healthy on 2026-11-21.
* Peer review: not recorded. This was the local GitOps repo, not a classroom-reviewed configuration commit.
* GitHub submission commit: `19f4b503c30d07875e2f63234ea00a86e537a9e0`; this is the project submission commit, not the Argo
	deployment revision.

## Verification

| Check | Expected | Local observation |
|---|---|---|
| Page `/` | HTTP 200 | HTTP 200 on 2026-11-21; request ID `87e7ed2d-d6ed-4184-bb7c-d7f82cee68d6`. |
| Health `/healthz` | HTTP 200, `Healthy` | HTTP 200; request ID `p1-local-health-verify-20261121`; release `foundation-observe-a`, environment `workshop-blue`. |
| Reference API | HTTP 200; 3x3 board; six initial moves | Verified through the Kubernetes Service on 2026-11-21; request ID `p1-local-ref-verify-20261121`. |
| Missing board | HTTP 404, `NOT_FOUND` | Prior local response on 2026-11-11; request ID `5480d1ab-ac47-48ac-bb56-95663e3ad13f`. |
| Loki correlation | Matching request record | Loki returned the reference request above with status 200, release `foundation-observe-a`, environment `workshop-blue`, and session `p1-local`. |
| Classroom Grafana/Loki | Matching classroom request | Not run. The Loki result above is from the local Grafana/Loki stack. |

## Failure, Recovery, and Handover

* Required Service-selector failure exercise and recovery: not performed.
* Separate blue-to-green change with config-revision increment: not performed.
* Peer reproduction: not performed.
* Individual demonstration and reflection: not recorded.
* Classroom recovery revision: none exists because classroom deployment was not run. The local Argo app can be inspected
	with `argocd --core app get p1-foundation-local`; the local GitOps commit is listed above.

## Completion Assessment

This repository contains verified local packaging and a local Kubernetes/Argo CD deployment with app and Loki checks.
It is **not a complete P1 delivery yet**: the project brief also requires classroom review and reconciliation, the
controlled failure/recovery exercise, peer reproduction, and individual demonstrations. BP Yalla scaffolding, pull
request, and deployment remain pending because the approved walkthrough was unavailable.
