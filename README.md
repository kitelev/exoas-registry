# exoas-registry — Exocortex AssetSpace registry

**The catalogue of mountable AssetSpaces for [Exocortex](https://github.com/kitelev/exocortex).** This repository is itself an **AssetSpace** — a git-backed package of vault assets you mount into an Exocortex vault. It holds one `exo__AssetSpace` **descriptor** per known repository, recording where the AssetSpace lives, the namespace it mounts under, and what it **depends on** — the dependency DAG the engine resolves when you apply a Profile.

> **Where this fits.** In the [Exo-as-SDK topology](https://github.com/kitelev/exocortex/blob/main/docs/explanation/assetspace-sdk-topology.md), `exo` is the platform, an AssetSpace is a library/jar, and a Profile is a manifest. The registry is the **package index** that ties them together: a Profile lists leaf AssetSpaces, and the engine walks each descriptor's `dependsOn` here to compute the full effective mount set.

---

## What's in here

A single namespace folder, `registry/`, with one descriptor asset per AssetSpace. Each descriptor is an instance of `exo__AssetSpace` (defined in [`exoas-exo`](https://github.com/kitelev/exoas-exo)).

### Descriptor shape

```yaml
---
exo__Instance_class:
  - "[[exo__AssetSpace]]"
exo__Asset_label: "kitelev/exoas-public"
exo__AssetSpace_source: "https://github.com/kitelev/exoas-public"
exo__AssetSpace_namespace: "public"
exo__AssetSpace_dependsOn:
  - "[[exoas-exo]]"
  - "[[exoas-exocmd]]"
---
```

| Property | Purpose |
| --- | --- |
| `exo__AssetSpace_source` | The git URL the engine clones to mount the AssetSpace. |
| `exo__AssetSpace_namespace` | The namespace it mounts under (`assetspaces/<owner>/<repo>/`). |
| `exo__AssetSpace_dependsOn` | Other AssetSpaces this one needs — the edges of the dependency DAG. |

### What's catalogued

Descriptors cover the whole audience-layered topology: the floor (`exoas-exo`, `exoas-exocmd`, `exoas-w3c-aggregated`), the public library (`exoas-public`), shared collaboration layers (`exoas-shared-*`), personal leaves (`exoas-my`, `exoas-tbank`, `exoas-exodev`, …), the registry and profiles themselves, plus peer-tester spaces (`kalashnikova/…`, `mudriy/…`, `levina/…`) and the `exofs-kitelev-files` FileSpace. The set grows as new AssetSpaces are published.

> Every descriptor is a live asset on disk in `registry/`. This README is reference prose; the authoritative catalogue is the assets themselves.

---

## Using this AssetSpace

The registry is consumed by the engine to resolve Profiles. As a tester you rarely mount it alone — you **apply a Profile** ([`exoas-profiles`](https://github.com/kitelev/exoas-profiles)), and the engine reads the registry to expand that Profile's `includes` into a full mount set via `dependsOn`.

- **CLI:** `npx @kitelev/exocortex-cli assetspace-add --vault ~/vault --url https://github.com/kitelev/exoas-registry`, then apply a profile.
- **Plugin:** **Exocortex: Apply profile** resolves dependencies through the registry automatically.

Once mounted, descriptors appear under `assetspaces/kitelev/exoas-registry/registry/`.

## Conventions (for contributors)

- **UID-canon.** Every descriptor is a UUID-named file (`<exo__Asset_uid>.md`); the repo slug lives in `exo__Asset_label` (e.g. `kitelev/exoas-public`).
- **Add a descriptor when you publish an AssetSpace.** A new mountable repo needs a descriptor here (with `source`, `namespace`, and any `dependsOn`) before a Profile can include it.
- **Keep the DAG acyclic.** `dependsOn` edges must not form a cycle — the engine walks them transitively.
- **CI.** Pushes run the shared [AssetSpace SHACL gate](https://github.com/kitelev/exoas-ci) (`validate schema --shapes-mode`).

## See also

- [exoas-profiles](https://github.com/kitelev/exoas-profiles) — the `exo__Profile` manifests that select AssetSpaces from this registry.
- [exoas-exo](https://github.com/kitelev/exoas-exo) — defines the `exo__AssetSpace` class these descriptors instantiate.
- [Exocortex engine repo](https://github.com/kitelev/exocortex) · [Exo-as-SDK topology](https://github.com/kitelev/exocortex/blob/main/docs/explanation/assetspace-sdk-topology.md).

## License

MIT — see the [engine repo](https://github.com/kitelev/exocortex/blob/main/LICENSE).
