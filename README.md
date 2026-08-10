# Sequoia-PySDK

Python SDK leaf for the **Sequoia** project (NVIDIA Jetson + STM32) in the
SiliconCentric `project-managers` fleet.

This leaf provides `sequoia-sdk`, a Pythonic gRPC client for the `HalService`
endpoint exposed by `Sequoia-Client`. The SDK distribution package is
**`sequoia-sdk`** (import name `sequoia_sdk`); a `acadia_sdk` deprecation shim
re-exports the public surface for callers still on the old name.

The SDK source, tooling, docs, examples, and test suite live under
[`sequoia-sdk/`](sequoia-sdk/). See [`sequoia-sdk/README.md`](sequoia-sdk/README.md)
for the full API, quickstart, and `make` targets (`setup`, `gen`, `check`,
`build`).

---
Part of the `Sequoia` project in the `project-managers` fleet. See
`docs/project-managers.md` for the full 9-project / 8-leaf hierarchy and
shared conventions.