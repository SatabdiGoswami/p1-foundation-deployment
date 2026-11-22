# P1 Local Classroom

This is a local practice environment, not the shared classroom or BP Yalla deployment. It uses Kind on the Podman VM,
Argo CD, an internal Git daemon, and single-instance Loki/Grafana. The Podman VM is allocated 6 GiB RAM and 4 CPUs.

## Current Result

* Argo Application: `p1-foundation-local`, synced and healthy at `b58a081`.
* App image: `localhost/p1-local:foundation-a`.
* App config image ID: `474c4137be468ebaf94dbbf978d8dce52394250b5287b49dc933ef17c802c17a`.
* Local session label: `p1-local`; environment: `workshop-blue`.
* The supplied app and API return through the `foundation` Service; request records are pushed to local Loki.

## Access

The port-forwards are currently running in separate terminals. If they stop, start each in its own terminal:

```powershell
kubectl --context kind-p1-local -n p1-local port-forward service/foundation 18081:8080
kubectl --context kind-p1-local -n p1-local port-forward service/grafana 13000:3000
kubectl --context kind-p1-local -n p1-local port-forward service/loki 13100:3100
```

* App page: http://127.0.0.1:18081
* Health: http://127.0.0.1:18081/healthz
* Reference API: http://127.0.0.1:18081/api/boards/reference
* Grafana: http://127.0.0.1:13000 (anonymous Viewer; datasource `P1 Loki`)
* Loki readiness: http://127.0.0.1:13100/ready

In Grafana Explore, use a query such as:

```text
{job="academy-w110", session="p1-local"} | json | request_id="YOUR_REQUEST_ID"
```

Argo status:

```powershell
& "$env:LOCALAPPDATA\Programs\argocd\argocd.exe" --core app get p1-foundation-local
```

## Local Boundaries

This setup has no classroom namespace assignment, facilitator import, Argo classroom Git server, public ingress, or BP
deployment. Its internal Git daemon has no authentication and must remain cluster-internal; do not expose its Service
outside this local cluster. Grafana is configured for anonymous Viewer access. The Git repository and Loki data use
ephemeral local storage and are for practice, not durable records. Stop port-forwards with Ctrl+C in their terminals.