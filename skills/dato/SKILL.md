---
description: Datos publicos de Argentina procesables — estadísticas INDEC, resultados electorales, datos catastrales y jurisprudencia. Usar cuando el usuario pide datos oficiales, estadísticas o quiere analizar información pública argentina.
---

## Fecha actual

Antes de cualquier WebSearch que incluya año o mes, confirmá la fecha del sistema (`Bash: date` o contexto `currentDate`). Nunca asumas ni hardcodees el año — usá siempre el que reporta el sistema.

---

## Comandos

### `/dato indec [indicador]`

Mapear el indicador a un ID de serie de tiempo. IDs principales:

| Indicador              | ID de serie                     |
|------------------------|----------------------------------|
| IPC (inflación mensual)| `101.1_I2N_2016_M_22`           |
| Desempleo              | `148.3_INIVELNAL_DICI_M_26`     |
| Canasta básica total   | `145.3_CBTOTAL_0_M_26`          |
| Salario privado formal | `148.3_IPPRIVFOR_DICI_M_15`     |
| Tipo de cambio oficial | `168.1_T_CAMBIOR_0_M_33`        |
| PBI variación trim.    | `143.3_NO_PR_2004_A_33`         |

Hacer WebFetch a:
`https://apis.datos.gob.ar/series/api/series/?ids={ID}&limit=12&format=json`

Si el indicador no está en la tabla, hacer WebSearch:
`"apis.datos.gob.ar series [indicador] id argentina"`

Luego intentar WebFetch con el ID encontrado.

Fallback si la API falla: WebSearch a `site:indec.gob.ar [indicador]` y presentar el dato más reciente disponible.

Formato:
```
## [Indicador] — INDEC

**Último dato disponible:** [valor] ([fecha])
**Mes anterior:** [valor] ([fecha])
**Variación:** [+/-X%]

**Últimos 6 meses:**
| Período  | Valor |
|----------|-------|
| [mes]    | [val] |
| ...      | ...   |

Fuente: INDEC — API Series de Tiempo Argentina
URL: https://apis.datos.gob.ar/series/api/series/?ids={ID}&limit=12
Fecha de consulta: [hoy]
```

---

### `/dato elecciones [año] [distrito]`

Hace WebFetch a:
`https://datos.gob.ar/dataset/interior-resultados-elecciones-nacionales`

Si el dataset tiene descarga directa, indica la URL. Si no, hace WebSearch:
`"resultados elecciones [año] [distrito] argentina datos.gob.ar OR resultados.gob.ar"`

Para resultados recientes (2023 en adelante): WebFetch a `https://resultados.gob.ar`

Presentar:
- Total de votos válidos / participación
- Resultado por partido/candidato (top 5)
- Comparación con elección anterior si el usuario la pide

Formato:
```
## Elecciones [año] — [Distrito/Nacional]

**Participación:** X% (X.XXX.XXX votos válidos)

| Partido / Candidato | Votos     | %     |
|---------------------|-----------|-------|
| [nombre]            | X.XXX.XXX | XX.X% |
| [nombre]            | X.XXX.XXX | XX.X% |

Fuente: [origen del dato — Ministerio del Interior / resultados.gob.ar]
URL: [url]
Fecha del dato: [fecha oficial]
```

---

### `/dato catastro [provincia]`

Hace WebSearch con:
`"catastro datos abiertos [provincia] argentina api descarga"`

Luego intenta WebFetch al portal de datos de esa provincia.

Portales conocidos:
- CABA: `https://data.buenosaires.gob.ar/dataset?q=catastro`
- Buenos Aires: `https://catalogo.datos.gba.gob.ar/dataset?q=catastro`
- Córdoba: `https://datos.gob.ar/dataset?q=catastro+cordoba`
- General: `https://datos.gob.ar/dataset?q=catastro+[provincia]`

Presentar:
- Qué datasets están disponibles
- URL de descarga directa si existe
- Formato del dato (shapefile, CSV, GeoJSON)
- Última actualización

Formato:
```
## Catastro — [Provincia]

**Datasets disponibles:**

| Dataset              | Formato     | Última actualización | URL |
|----------------------|-------------|----------------------|-----|
| [nombre]             | [formato]   | [fecha]              | [url] |

**Cómo usar el dato:**
[instrucciones breves si aplica]

Fuente: [portal de datos de la provincia]
Fecha de consulta: [hoy]
```

Si no hay datos disponibles online, indicar el organismo provincial al que hay que contactar.

---

### `/dato justicia [tema]`

Hace WebFetch a:
`https://datos.jus.gob.ar/dataset?q=[tema]`

Si no hay resultados, WebSearch:
`"site:saij.gob.ar [tema]"` para jurisprudencia y normativa.

También intenta:
`"[tema] jurisprudencia argentina [año] fallo"`

Presentar:
- Normativa vigente sobre el tema (leyes, decretos)
- Jurisprudencia relevante si aplica
- Dónde encontrar más información

Formato:
```
## Justicia — [Tema]

**Normativa vigente:**
- [Ley/Decreto número]: [descripción breve] — [URL infoleg]

**Jurisprudencia destacada:**
- [Fallo]: [descripción] — [URL]

**Más información:**
- SAIJ: https://www.saij.gob.ar
- InfoLeg: https://www.infoleg.gob.ar

Fuente: [origen] | Fecha: [hoy]
```

---

## Tono

- Datos presentados en tablas cuando hay múltiples valores
- Siempre mostrar fuente y URL directa
- Si el dato puede estar desactualizado, aclararlo
- Si la API falla, decirlo y ofrecer la fuente alternativa
- No interpretar políticamente los datos, solo presentarlos
