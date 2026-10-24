# Cloud Forge — Laboratorio 2 | Pipeline seguro

CI con Ruff, pytest, Bandit y Trivy. Autor: **libio**.

## Resultado de las pruebas

Archivo: [`entrega/matriz_experimentos.csv`](entrega/matriz_experimentos.csv)

| Experimento | Resultado | Regla / aviso | Package | Commit fallo | Commit fix |
|-------------|-----------|---------------|---------|--------------|------------|
| Línea base | success | — | habilitado | `b3d5cb1` | `b3d5cb1` |
| 1 · Lint | fallido | F401 os unused | omitido | `9b21334` | `3b6e497` |
| 2 · Tests | fallido | assert -1 == 5 | omitido | `0a6ddbf` | `a33c6b3` |
| 3 · SAST | fallido | B307 eval | omitido | `93ea973` | `b97d84a` |
| 4 · Secrets | fallido | cloud-forge-demo HIGH | omitido | `f012008` | `4a175ed` |
| 5 · SCA | fallido | CVE-2018-18074 | omitido | `1652df4` | `a847100` |
| Verificación final | success | — | habilitado | `a847100` | `a847100` |

## Controles locales

```bash
python -m pip install -r requirements-dev.txt
bash ci/check.sh lint
bash ci/check.sh tests
bash ci/check.sh sast
bash ci/check.sh secrets
bash ci/check.sh sca
```
