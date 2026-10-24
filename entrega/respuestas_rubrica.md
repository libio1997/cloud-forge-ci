# Respuestas — Rúbrica §16

## 1. ¿Por qué una prueba puede aprobar y SAST fallar?

Las pruebas ejercitan rutas concretas (suma, entero, rechazo de expresiones). SAST analiza el código estáticamente: una función con `eval` que ninguna prueba llama sigue siendo un hallazgo (p. ej. Bandit B307). Cobertura de tests ≠ ausencia de patrones inseguros.

## 2. ¿Qué implica `package` omitido?

En GitHub Actions, `package` declara `needs: checks`. Si cualquier job de la matriz falla, `checks` no se considera exitoso y `package` no se ejecuta (estado *skipped*). El código no se empaqueta: la puerta de calidad bloqueó el artefacto.

## 3. ¿Qué diferencia un secreto borrado de uno revocado?

- **Borrar** el archivo del árbol actual evita nuevas detecciones en el tip, pero el valor puede seguir en el historial de Git.
- **Revocar** invalida el secreto en el proveedor (API keys, tokens). Ante una credencial real: rotar/revocar, remediar historial y auditar uso. En este lab el token es ficticio; borrar el archivo basta pedagógicamente.

## 4. ¿Qué cobertura falta al escanear solo dependencias directas?

Faltan transitivas (dependencias de dependencias), lockfiles completos, imágenes de contenedor, binarios embebidos y herramientas solo en `requirements-dev.txt` (aquí excluidas a propósito). Un manifiesto vacío o mínimo no prueba cobertura de todo el árbol de paquetes.

## 5. ¿Por qué HIGH/CRITICAL no expresa por sí solo explotabilidad?

La severidad resume impacto teórico y disponibilidad de parche según la base CVE. No indica si el código vulnerable es alcanzable, si hay mitigaciones de red/configuración, ni el contexto de amenaza. Hace falta análisis de explotabilidad y priorización.

## 6. ¿Qué revisar antes de aceptar código generado por IA?

Lint y pruebas, SAST (p. ej. `eval`, inyección), secretos en el diff, dependencias y versiones en manifiestos, que las “correcciones” no oculten fallos (`# noqa`, `# nosec`, cambiar asserts), y que no se desactiven puertas del pipeline.
