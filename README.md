# Sequoia-PySDK

## Project Summary

Sequoia-PySDK is the Python client leaf for the Sequoia project. Its packaged
distribution is `sequoia-sdk`, imported as `sequoia_sdk`, and it provides a
Pythonic gRPC client for the HalService endpoint exposed by Sequoia-Client. The
SDK source, type declarations, examples, changelog, package metadata, and test
suite live below `sequoia-sdk/`. The repository also preserves an
`acadia_sdk` deprecation shim so callers using the earlier import name can
migrate without an immediate API break.

The documented SDK surface includes connection setup, discovery, one-shot and
long-running test execution, event/monitor handling, typed result round trips,
and a fake server used by tests. Examples demonstrate long-running workflows
and running all self-tests. The package README and Makefile are the source for
generation, setup, checking, and build commands; this root README provides the
repository-level inventory and points to that detailed guide. Test names give
good evidence for client behavior, but they do not verify interoperability with
a real Sequoia-Client, network failure behavior on a board, TLS deployment, or
the compatibility shim in every downstream application. Those remain manual
checks and are explicitly marked below.

The SDK is intentionally a leaf rather than a second implementation of HAL
logic: it serializes caller intent into the client's service contract and
returns typed responses and events. This means validation must use matching
generated contracts and server versions; packaging metadata, generated-code
freshness, and deprecation behavior should be checked during release
preparation.

## Feature Inventory

| # | Name / Description | Implemented? | Test Coverage? | Manual Test |
|---:|---|---|---|---|
| 1 | `sequoia-sdk` package and `sequoia_sdk` import | Implemented | Package checks present | [ ] Manual verification required |
| 2 | Typed gRPC client connection | Implemented | Covered by `test_connect.py` | [ ] Manual verification required |
| 3 | Module discovery | Implemented | Covered by `test_discovery.py` | [ ] Manual verification required |
| 4 | One-shot test invocation | Implemented | Covered by `test_oneshot.py` | [ ] Manual verification required |
| 5 | Long-running test control | Implemented | Covered by `test_long_running.py` | [ ] Manual verification required |
| 6 | Events and monitoring | Implemented | Covered by `test_event.py`, `test_monitor.py` | [ ] Manual verification required |
| 7 | Typed result round trips | Implemented | Covered by `test_types_roundtrip.py` | [ ] Manual verification required |
| 8 | Fake server/test harness | Implemented | `tests/fakes/fake_server.py` and fixtures | [ ] Manual verification required |
| 9 | Deprecation compatibility shim | Implemented | Covered by `test_deprecation_shim.py` | [ ] Manual verification required |
| 10 | User examples for long-running/all-tests flows | Implemented | Example execution not automated | [ ] Manual verification required |
| 11 | Real Sequoia-Client interoperability | Unknown | Fake-server tests only | [ ] Manual verification required |
| 12 | Published package/release workflow | Partial | Build/check commands documented | [ ] Manual verification required |

## Validation

From `sequoia-sdk/`, follow its README and Makefile for setup, generated
protos, checks, and build. The focused tests are under `sequoia-sdk/tests/`;
the examples are under `sequoia-sdk/examples/`.