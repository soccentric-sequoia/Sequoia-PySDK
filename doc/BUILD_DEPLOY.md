# Sequoia-PySDK Build and Deployment

## Scope

Sequoia-PySDK is the Python SDK for the Sequoia HAL service. The root Makefile
uses `uv` to create a virtual environment, install `sequoia-sdk[dev]` in
editable mode, regenerate protobuf and dataclass bindings, run pytest, ruff,
and strict mypy, and build a wheel plus source distribution.

## 1. Prerequisites

- Python 3.10 or newer, as required by `sequoia-sdk/pyproject.toml`.
- `uv` on `PATH` (override with `UV=/path/to/uv`). Dependency installation and
  generation require network access unless the needed packages are cached.
- The generated bindings are derived from the Sequoia-HAL protobuf contract;
  use a compatible sibling checkout when regenerating.

```sh
make help
make venv                    # create .venv only
make setup                   # create .venv and install editable dev package
```

## 2. Setup

## 3. Build

```sh
make gen                     # regenerate proto and dataclass bindings
make gen-check               # fail when committed generated stubs are stale
make gen-clean               # remove generated output, then regenerate
make build                   # build sdist and wheel
```

Generated protobuf output is under `sequoia-sdk/src/sequoia_sdk/_proto`.

## 4. Test and lint

```sh
make test                    # pytest with coverage
make lint                    # ruff check SDK source
make typecheck               # mypy --strict using the SDK config
make check                   # lint, typecheck, and test
make all                     # alias for check
```

## 5. Artifacts

`make build` writes the wheel and sdist to `sequoia-sdk/dist`. Editable
installation uses the package metadata and development extras in
`sequoia-sdk/pyproject.toml`; the generated `.pyi` package data is included in
the distribution. No Docker, cloud image, or installer target is declared.

## 6. Deploy, install, and run

```sh
make shell                   # open a uv-activated development subshell
```

This leaf is a library and has no service `run` or remote `deploy` target.
Install a built wheel into a consumer environment with that environment's
package manager, then connect it to a reachable HalService endpoint according
to the SDK API. Credentials, endpoint configuration, and a compatible HAL
service are conditional integration requirements.

## 7. Cleanup

```sh
make clean                   # remove SDK build/dist/cache artifacts
make distclean               # clean plus remove .venv and stamps
```

## 8. Verification caveats

Unit tests and generated-stub checks do not prove gRPC interoperability with a
real HAL service, device timing, firmware compatibility, or authentication.
Run a manual client workflow against a compatible Sequoia target after package
installation. No cloud deployment workflow is defined by this repository.