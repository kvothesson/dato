# dato

Datos públicos de Argentina, procesables. Estadísticas del INDEC, resultados electorales, datos catastrales y jurisprudencia — todo desde fuentes primarias oficiales.

## Instalación

```bash
claude --plugin-dir /ruta/a/dato
```

## Comandos

### `/dato indec inflacion`

Últimos datos de inflación mensual (IPC) del INDEC.

```
## IPC (Inflación mensual) — INDEC

**Último dato disponible:** 3,7% (marzo 2025)
**Mes anterior:** 2,4% (febrero 2025)
**Variación:** +1,3 pp

**Últimos 6 meses:**
| Período       | Variación mensual |
|---------------|-------------------|
| Marzo 2025    | 3,7%              |
| Febrero 2025  | 2,4%              |
| Enero 2025    | 2,3%              |
| Diciembre 2024| 2,7%              |
| Noviembre 2024| 2,4%              |
| Octubre 2024  | 2,9%              |

Fuente: INDEC — API Series de Tiempo Argentina
URL: https://apis.datos.gob.ar/series/api/series/?ids=101.1_I2N_2016_M_22&limit=12
Fecha de consulta: [en tiempo real al ejecutar el comando]
```

---

### `/dato elecciones 2023 nacional`

Resultados de las elecciones generales 2023.

```
## Elecciones Generales — Presidente 2023

**Participación:** 76,3% (26.756.000 votos válidos)

| Candidato / Frente              | Votos      | %     |
|---------------------------------|------------|-------|
| Javier Milei (LLA)              | 14.476.762 | 55,7% |
| Sergio Massa (UxP)              | 11.512.960 | 44,3% |

Segunda vuelta — 19 de noviembre de 2023

Fuente: Ministerio del Interior — https://resultados.gob.ar
Fecha del dato: noviembre 2023
```

---

### `/dato catastro caba`

Datasets catastrales disponibles para Ciudad de Buenos Aires.

```
## Catastro — Ciudad Autónoma de Buenos Aires

**Datasets disponibles:**

| Dataset                    | Formato        | Última actualización | URL |
|----------------------------|----------------|----------------------|-----|
| Parcelas urbanas           | GeoJSON/SHP    | 2024                 | https://data.buenosaires.gob.ar/dataset/catastro |
| Permisos de obra           | CSV            | Mensual              | https://data.buenosaires.gob.ar/dataset/permisos-obra-construccion |
| Avalúos fiscales           | CSV            | Anual                | https://data.buenosaires.gob.ar/dataset/avaluos-fiscales |

**Cómo acceder:**
Todos los datasets son descarga directa desde el portal BA Data.

Fuente: Portal de Datos Abiertos CABA — https://data.buenosaires.gob.ar
Fecha de consulta: mayo 2025
```

---

### `/dato justicia violencia de genero`

Normativa y datos sobre violencia de género en Argentina.

```
## Justicia — Violencia de género

**Normativa vigente:**
- Ley 26.485 (Protección integral para prevenir, sancionar y erradicar la violencia contra las mujeres)
  URL: https://www.infoleg.gob.ar/infolegInternet/anexos/150000-154999/152155/norma.htm
- Ley 27.736 (Programa Acompañar — asistencia económica a víctimas)
  URL: https://www.infoleg.gob.ar

**Datos disponibles:**
- Femicidios y homicidios agravados: https://datos.jus.gob.ar/dataset/registro-sistematizacion-y-seguimiento-de-femicidios-y-homicidios-agravados-por-el-genero
- Causas judiciales activas: https://datos.jus.gob.ar

**Más información:**
- SAIJ: https://www.saij.gob.ar (buscar "violencia de género")
- InfoLeg: https://www.infoleg.gob.ar

Fuente: datos.jus.gob.ar | Fecha: mayo 2025
```

---

## Fuentes

- [API Series de Tiempo Argentina — INDEC/Datos.gob.ar](https://apis.datos.gob.ar/series/api/)
- [Portal Nacional de Datos Abiertos](https://datos.gob.ar)
- [Resultados Electorales — Ministerio del Interior](https://resultados.gob.ar)
- [BA Data — Ciudad de Buenos Aires](https://data.buenosaires.gob.ar)
- [Datos Justicia Argentina](https://datos.jus.gob.ar)
- [SAIJ — Jurisprudencia y Normativa](https://www.saij.gob.ar)
