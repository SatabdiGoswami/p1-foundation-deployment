# P1 Evidence Log

Status: local evidence recorded below. Classroom namespace/session and BP deployment were unavailable, so local checks are
not represented as classroom results. Operators and predictors were not recorded. Unless stated otherwise, observations
were captured in terminal output; separate header/body files were not preserved.

| Time (UTC) | Milestone | Operator / predictor | Observation | Evidence |
|---|---|---|---|---|
| 2026-11-11 06:26:26 | 2, local packaging | Not recorded | Local image build recorded successful. Image ID `474c4137be468ebaf94dbbf978d8dce52394250b5287b49dc933ef17c802c17a`; container ID `72eb45c8e4c3a90ff5bd9b9f6a044818735c9530f0a886a2a9e4852c8fd90309`. Health returned `200 Healthy`. `/api/boards/missing` returned `404 NOT_FOUND`, release `foundation-observe-a`, environment `workshop-blue`, request ID `5480d1ab-ac47-48ac-bb56-95663e3ad13f`. | Response headers/body retained in this log. |
| 2026-11-21 | 1, baseline | Not recorded | No separate milestone-1 baseline record captured; W1.10 historical baseline was referenced by the project instructions. | Not captured. |
| 2026-11-21 | 2, local packaging | Not recorded | `P1-work/app` matches supplied `code/app` except `wwwroot/client.json`: supplied `80 ms / 0 retries`, configured `450 ms / 0 retries`. Written W1.10 justification was not recorded. | File comparison and local build evidence. |
| 2026-11-21 | 3, local configuration | Not recorded | Local Argo source commits: `46a8a33` (foundation) and `b58a081` (Loki/Grafana). No peer review or review decision was recorded. No classroom configuration commit was created. | Local Git repository; not a classroom review. |
| 2026-11-21 | 4, local Argo deployment | Not recorded | Argo Application `p1-foundation-local` synced to `b58a081ba2d39243e1ef7d0b92be307794ad3f44` and reported Healthy. Foundation Pod was Ready; Service had a ready endpoint. Containerd image config ID matched the local image ID above. Session `p1-local`; environment `workshop-blue`. | `argocd --core app get`; `kubectl get pods,services,endpoints`; image inspection. |
| 2026-11-21 09:26:00 | 4, local health | Not recorded | `/healthz` returned `200 Healthy`; request ID `5230bcdc-34b1-4016-8176-8dd06acc2668`; release `foundation-observe-a`; environment `workshop-blue`. | Service port-forward response and matching stdout record. |
| 2026-11-21 09:26:15 | 4, local reference API | Not recorded | `/api/boards/reference` returned `200`, 3x3 board, six initial moves; request ID `667c54b7-b915-4d93-ae38-d3fbfb23da54`. | Service port-forward response and matching stdout record. |
| 2026-11-21 09:26:28 | 4, local page | Not recorded | `/` returned `200`; request ID `ddb9bf6f-8b3a-41d5-a52a-02941fcaea95`. | Service port-forward response. |
| 2026-11-21 09:36:11.7588243 | 4, local Loki correlation | Not recorded | Loki query for `{job="academy-w110", session="p1-local"} | json | request_id="p1-local-ref-verify-20261121"` returned one `/api/boards/reference` record with status `200`, release `foundation-observe-a`, and environment `workshop-blue`. | Local Loki query result. |
| Not performed | 5, controlled failure and recovery | Not recorded | The required Service-selector mismatch, empty-endpoint observation, corrective revision, and fresh verification were not performed. | No evidence. |
| Not performed | 6, peer reproduction | Not recorded | A peer did not reproduce the handover in a fresh folder. | No evidence. |
| Not recorded | 7, individual demonstration and reflection | Not recorded | Individual demonstrations and learner reflections were not provided. | No evidence. |

Individual reflection: Not provided. Next step: complete the required controlled failure/recovery, peer reproduction, and
individual demonstration when the classroom environment is available.