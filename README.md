# Cloud Forge — Laboratorio 2 | Pipeline seguro

Proyecto didáctico del **Módulo 3 · Sesión 2**: CI con Ruff, pytest, Bandit y Trivy. Cinco controles independientes bloquean el empaquetado si fallan.

## Estructura

```
app/calculadora.py          # sumar + interpretar_entero
tests/test_calculadora.py   # 3 pruebas
ci/check.sh                 # lint | tests | sast | secrets | sca
security/trivy-secret.yaml  # regla CFDEMO_*
.github/workflows/secure-ci.yml
entrega/                    # matriz, reportes y reflexión
```

## Requisitos

- Python 3.11+ (en CI: 3.11)
- GitHub Actions (recomendado) o, en local: venv + Trivy (binario o Docker)

## Uso local

```bash
python -m venv .venv
source .venv/bin/activate   # Windows: .venv\Scripts\Activate.ps1
python -m pip install -r requirements-dev.txt

# Controles (mismo script que Actions)
bash ci/check.sh lint
bash ci/check.sh tests
bash ci/check.sh sast
bash ci/check.sh secrets   # requiere Trivy
bash ci/check.sh sca       # requiere Trivy + DB
```

Instalar Trivy (alternativa a Docker):

```bash
curl -sfL https://raw.githubusercontent.com/aquasecurity/trivy/main/contrib/install.sh \
  | sh -s -- -b ~/.local/bin
export PATH="$HOME/.local/bin:$PATH"
```

## GitHub Actions

Al publicar en `main`, el workflow **Secure CI** ejecuta la matriz `lint, tests, sast, secrets, sca` (`fail-fast: false`). Solo si los cinco pasan, el job `package` genera `dist/cloud-forge.zip`.

## Entrega

Ver `entrega/`:

- `matriz_experimentos.csv` — evidencia de los 5 fallos y correcciones
- `respuestas_rubrica.md` — reflexión (rúbrica §16)
- `reportes/` — salidas locales de línea base, fallos y verificación final
- `hashes_commits.md` — SHA de cada commit del laboratorio

## Seguridad

No hay credenciales reales. El token `CFDEMO_…` es sintético y no otorga acceso a ningún servicio. `requirements-dev.txt` se excluye del SCA solo en este ejercicio didáctico.
