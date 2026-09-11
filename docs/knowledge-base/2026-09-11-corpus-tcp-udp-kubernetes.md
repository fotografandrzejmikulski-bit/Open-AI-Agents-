# Corpus Audit — TCP/UDP + Kubernetes Architecture

Date: 2026-09-11
Source type: 2 uploaded visual references
Decision: integrate into existing portfolio; no new numbered project

## 1. Source inventory

### A. TCP vs UDP
The visual compares:
- TCP: connection-oriented 3-way handshake, reliable delivery with acknowledgements/retransmission, ordered delivery, flow control, byte-stream semantics;
- UDP: connectionless datagrams, best-effort delivery, no transport-level retransmission/ACK, unordered delivery, lower protocol overhead and discrete message boundaries.

It also maps representative uses: TCP for HTTP/HTTPS, file transfer, email, SSH, database connections and APIs; UDP for latency-sensitive or datagram-oriented cases such as DNS, streaming, gaming, VoIP and IoT. These examples are treated as conceptual guidance, not universal protocol rules.

### B. Kubernetes Architecture
The visual decomposes Kubernetes into:
- Control Plane: API Server, Scheduler, Controller Manager, etcd;
- Worker Nodes: kubelet, kube-proxy, container runtime;
- Pods: smallest deployable unit, one or more containers, shared network namespace and storage volumes;
- Services/networking: ClusterIP, NodePort, LoadBalancer, Ingress;
- Deployments/scaling: Deployment → ReplicaSet → Pods, rolling updates/rollback, HPA;
- ConfigMaps/Secrets: configuration vs sensitive data injection into workloads.

## 2. Architectural synthesis

The two references add a lower-level runtime/network substrate beneath the existing DevSecOps and agent architectures:

AGENT / API / SERVICE
→ APPLICATION PROTOCOL
→ TCP/UDP TRANSPORT
→ NETWORK POLICY / TLS / SEGMENTATION
→ KUBERNETES SERVICE / INGRESS
→ POD
→ CONTAINER RUNTIME
→ NODE
→ CONTROL PLANE
→ OBSERVABILITY / VERIFICATION

This makes networking and orchestration explicit parts of the execution environment rather than invisible infrastructure.

## 3. Agent-runtime implications

For P100/P117/P119, transport must be represented as a capability with explicit semantics:

- connection vs datagram;
- ordering guarantees;
- delivery/retry responsibility;
- flow/congestion behavior;
- message boundaries;
- latency sensitivity;
- encryption/authentication layer;
- timeout and failure semantics.

An agent must not infer delivery guarantees merely from the presence of a network connection. Application-level reliability may be required above UDP, while TCP's reliability does not imply application-level correctness.

## 4. Kubernetes as controlled execution substrate

Kubernetes adds a declarative control-plane model to the portfolio's controlled-execution doctrine:

DESIRED STATE
→ CONTROL PLANE
→ SCHEDULING / RECONCILIATION
→ WORKLOAD
→ OBSERVATION
→ ACTUAL STATE
→ DRIFT DETECTION
→ RECONCILIATION

This maps naturally to agent verification, but with an important boundary: Kubernetes reconciliation is infrastructure orchestration, not authorization. A desired state accepted by the control plane must still originate from an authorized change process.

## 5. Provenance and rollback

Deployment provenance should bind:
- source commit/tree identity;
- build artifact digest;
- container image digest;
- deployment manifest/config version;
- target cluster/namespace/workload;
- rollout strategy;
- health/readiness evidence;
- resulting runtime state;
- rollback decision and reason.

Tags and mutable image references should not be treated as immutable provenance identifiers when a digest is available.

## 6. Kubernetes security implications

The visual's ConfigMap/Secret distinction reinforces:
- configuration ≠ secret;
- encoded secret material ≠ automatically encrypted-at-rest secret material;
- environment injection ≠ authorization;
- pod isolation ≠ complete Zero Trust.

Kubernetes RBAC, network policy, workload identity, admission controls, secret handling, image provenance and runtime security should therefore remain separate policy dimensions.

## 7. TCP/UDP security and agent networking

Transport selection must not be treated as a security boundary by itself. Security properties are layered above and around transport through TLS, authentication, authorization, network segmentation and application policy.

The existing invariant remains:

NETWORK REACHABILITY ≠ AUTHORIZATION

and is extended to:

TRANSPORT RELIABILITY ≠ APPLICATION CORRECTNESS

## 8. Project mapping

| Theme | Primary project(s) | Action |
|---|---|---|
| TCP/UDP transport semantics | P100, P117, P119 | add transport capability metadata and failure semantics |
| Kubernetes control plane | P100, P117 | controlled deployment/reconciliation model |
| Kubernetes networking | P100, P119 | service/ingress/network-policy layer |
| Pods/container runtime | P117, P119 | execution isolation and runtime observation |
| HPA/scaling | P100, P117 | policy-controlled autoscaling and capacity signals |
| ConfigMap/Secrets | P100, P119 | configuration/secret separation and policy checks |
| rollout/rollback | P100, P117 | digest-bound deployment provenance and postcondition verification |

## 9. New-project decision

No new numbered project is warranted. Kubernetes and transport networking are infrastructure substrates for existing agent/DevSecOps/runtime projects, not an independent product boundary in this corpus.

## 10. Evidence boundaries

- diagram ≠ complete Kubernetes security architecture;
- conceptual TCP/UDP comparison ≠ application-specific performance benchmark;
- container isolation ≠ full security isolation;
- Kubernetes reconciliation ≠ authorization;
- Secret object encoding ≠ proof of secure secret storage;
- service reachability ≠ permission;
- successful rollout ≠ verified business correctness.

## 11. Backlog

1. Add transport metadata to provider/tool capability schemas.
2. Add Kubernetes deployment as an explicit controlled-execution adapter.
3. Record image/artifact digests in deployment provenance.
4. Add readiness/health/runtime readback to promotion gates.
5. Add network-policy and workload-identity checks to Zero Trust policy evaluation.
6. Model desired-state vs observed-state drift for agent-managed infrastructure.
