# EvidencePack Download Links

## Primary (recommended)

| Pack | URL | SHA256 | Size |
|------|-----|--------|------|
| **Full** | [Download](https://ttgos-evidence.s3.us-east-2.amazonaws.com/artifacts/stweb-core84/v1/stweb_core84_evidencepack_full_v1.tar.gz) | `f8db5338eae4f5ea23968a00513bdf0a1910fd65081d90aa16559889ff33beb4` | 72.3 KB |
| **Light** | [Download](https://ttgos-evidence.s3.us-east-2.amazonaws.com/artifacts/stweb-core84/v1/stweb_core84_evidencepack_light_v1.zip) | `0fe3dba3fcbe1f1c2f7e1d310c0935ef727bc2e570967405865b333ebe9502c1` | 3.1 KB |

## Secondary (individual bundles for inspection)

| Artifact | URL | SHA256 | Size |
|----------|-----|--------|------|
| Core-84 Guard | [Download](https://ttgos-evidence.s3.us-east-2.amazonaws.com/artifacts/stweb-core84/v1/core84_guard.tar.gz) | `3e3208efe6fb2613542399be9015da8ff4e0a74e333ae575337358dae5874883` | 9.0 KB |
| Core-84 Baseline | [Download](https://ttgos-evidence.s3.us-east-2.amazonaws.com/artifacts/stweb-core84/v1/core84_baseline.tar.gz) | `fcc356a175814333bd12980066ddb4cec9db0857c7fd97c44e9ab2446b284200` | 5.9 KB |
| Full235 Guard | [Download](https://ttgos-evidence.s3.us-east-2.amazonaws.com/artifacts/stweb-core84/v1/full235_guard.tar.gz) | `c1f4def7fdbe129d49ada3681bca7a81cf67a70d7e6488fcb007b574bc227af1` | 23.7 KB |
| Full235 Baseline | [Download](https://ttgos-evidence.s3.us-east-2.amazonaws.com/artifacts/stweb-core84/v1/full235_baseline.tar.gz) | `3736b543fa43db41e7f52ff97c1e8c2cbab2226f1e6eb106c78b19499b0f095a` | 22.8 KB |

## Verification

```bash
# Download and verify Full pack
curl -O https://ttgos-evidence.s3.us-east-2.amazonaws.com/artifacts/stweb-core84/v1/stweb_core84_evidencepack_full_v1.tar.gz
shasum -a 256 stweb_core84_evidencepack_full_v1.tar.gz
# Expected: f8db5338eae4f5ea23968a00513bdf0a1910fd65081d90aa16559889ff33beb4
```
