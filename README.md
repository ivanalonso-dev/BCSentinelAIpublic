# BCSentinel — investigate_wallet_v7: resumen técnico público
### Versión apta para repositorio público — 28 de octubre de 2026

---

**Qué es este documento y qué no es.** Esto es un resumen de arquitectura de alto nivel, pensado para un repositorio **público** de GitHub, como prueba verificable de que el sistema existe y de cómo está construido conceptualmente. **No incluye el código fuente real, ni las fórmulas exactas, ni los pesos, ni los umbrales de decisión** — esos valores son secreto industrial de BCSentinel (ver `GEN-007-Strategic-value-definition.md`) y viven únicamente en la versión privada de este documento (`investigate_wallet_v7_FREEZE_DOC.md`) y en el código fuente, ambos en el repositorio privado. Si en algún momento este resumen y el documento privado entran en contradicción, el documento privado es la fuente de verdad — este es solo el escaparate.

**Qué es BCSentinel, en una frase.** Un sistema de detección y alerta temprana de formación de entidades cripto (protocolos, DAOs, lanzamientos de token) a partir de patrones de comportamiento on-chain, antes de que esa formación sea pública. **BCSentinel detecta y alerta — no es una recomendación de inversión ni asesoramiento financiero, no indica dónde invertir ni si se debe invertir.**

---

## 1. Qué responde `investigate_wallet_v7.py`

Dada una dirección de wallet en una red compatible con EVM, el sistema evalúa si hay evidencia de que esa wallet esté actuando como fundadora u operadora de una formación institucional emergente, y en qué fase de esa formación se encuentra. El sistema nunca asigna un nombre de entidad de forma automática — eso siempre requiere confirmación humana explícita.

## 2. Arquitectura, a nivel conceptual

El análisis combina varias fuentes de evidencia on-chain (selectores de función invocados, contratos desplegados, estructura de multisig/gobernanza, actividad reciente) en una abstracción de cuatro niveles:

```
Nivel 1: Wallet individual
Nivel 2: Firma de comportamiento (bloques de patrón de actividad)
Nivel 3: Candidato de Formación (agrupación de wallets relacionadas, con nivel de confianza)
Nivel 4: Entidad nombrada (solo tras confirmación humana)
```

Sobre esa base, un motor de puntuación propietario (no publicado) combina tres ejes de evidencia — estructural, institucional y de potencial futuro — en una puntuación compuesta única, que alimenta una clasificación de nivel de escalación (desde "sin cambios" hasta "revisión inmediata"). Los valores exactos de ponderación y los umbrales de cada nivel son secreto industrial y no se publican aquí.

El sistema organiza el análisis en capas de enriquecimiento independientes (memoria de señales persistente, detección de patrones de silencio/pivote, clasificación de arquetipo, estimación de tiempo restante hasta visibilidad pública, motor de narrativa automática, entre otras), diseñadas para degradar con elegancia: si una capa no está disponible, el sistema sigue funcionando con las capas restantes, sin fallar.

## 3. Qué NO hace (límites de alcance, públicos por diseño)

- No ejecuta consultas arbitrarias contra fuentes on-chain de forma oculta — cada consulta usada proviene de una definición fija y auditada internamente.
- Cobertura limitada a un número reducido de redes EVM soportadas explícitamente.
- No fusiona automáticamente la identidad de una misma entidad a través de distintas redes más allá de un registro simple de presencia.
- Nunca asigna de forma automática un resultado de "confirmado" o "descartado" — ambos requieren revisión humana.
- No identifica la identidad real de la persona u organización detrás de una wallet — entrega evidencia on-chain para que un analista humano investigue esa identidad.

## 4. Honestidad sobre limitaciones conocidas

El sistema documenta internamente sus propios puntos débiles conocidos en vez de ocultarlos — entre ellos: el enlace entre wallets de un mismo "Candidato de Formación" se basa en solapamiento de patrones, no en una verificación de relación real por sí solo (requiere verificación adicional antes de confirmarse como núcleo institucional); hay un eje de "confianza en el dato temporal" que puede entrar en tensión con la puntuación de relevancia institucional, y el sistema expone ambos por separado en vez de ocultarlos detrás de un único número; y el análisis multi-red no deduplica automáticamente una misma entidad activa en varias redes. Ninguna de estas limitaciones es nueva ni oculta — están documentadas en el propio código desde que se descubrieron.

## 5. Validación empírica

Un backtest retrospectivo sobre un dataset histórico interno de 186 casos etiquetados mostró que el sistema clasifica correctamente como formación real el 49% de los casos (92/186), con una metodología transparente de exclusión de casos ambiguos (ningún caso se clasifica inventando datos que no existen). Esta cifra describe comportamiento retrospectivo sobre datos ya conocidos, no una tasa de precisión validada estadísticamente contra resultados futuros ni una tasa de éxito comercial confirmada por clientes.

---

*Este documento es la versión pública y deliberadamente incompleta de la documentación técnica de `investigate_wallet_v7.py`. La versión completa, con fórmulas, pesos, umbrales y código fuente, es información confidencial de BCSentinel y no se publica.*
