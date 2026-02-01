# IS 2.d.02 (a) - Auditoría de Superficie de Exposición Post-Incidente (OSINT pasivo)
<!-- AYUDA (BORRAR): Plantilla del informe. Rellenad los campos entre corchetes y eliminad todos los bloques "AYUDA (BORRAR)" antes de entregar. -->

- Entidad objetivo: Clínica de San Rafael de Cádiz / Hospitales Pascual
- Equipo/Grupo: [Nombre del grupo]
<!-- AYUDA (BORRAR): Identificador del grupo/equipo. -->
- Integrantes: [Nombre Apellido (Iniciales)], [..]
<!-- AYUDA (BORRAR): Lista de integrantes (mismo orden que en la presentación). -->
- Fecha(s) de investigación: [YYYY-MM-DD a YYYY-MM-DD]
<!-- AYUDA (BORRAR): Rango de fechas reales en las que hicisteis las consultas OSINT. -->
- Versión: 1.0
<!-- AYUDA (BORRAR): Subid versión si hay revisiones (1.1, 1.2...). -->
- Límite de entrega (a): máximo 6 folios (12 caras) en PDF (si aplica)
<!-- AYUDA (BORRAR): Recordatorio del límite; podéis quitarlo si no os lo piden. -->

## 1. Resumen ejecutivo
<!-- AYUDA (BORRAR): 8-15 líneas. Debe entenderse sin leer el resto: qué se investigó, hallazgos top y acciones prioritarias. -->

**Objetivo.** Determinar qué información pública existía (antes del incidente supuesto) que podría haber facilitado la fase de reconocimiento de un atacante: identidades digitales, contactos, dominios/subdominios, huella documental (metadatos), menciones públicas y exposiciones derivadas.

**Hallazgos clave (3-7 bullets).**
- **Patrón de correos corporativos deducible**: Los correos siguen patrón `nombre.apellido@jmpascual.com`, facilitando spear phishing contra empleados específicos.
- **Información de empleados públicamente disponible**: Directorio de médicos con especialidades, fotos e información de contacto en sitio web y redes sociales, reutilizable para ingeniería social.
- **Brecha de seguridad pasada (verifications.io 2019)**: ~763M correos expuestos incluyendo empleados de Hospitales Pascual, credenciales potencialmente reutilizables.
- **Tecnologías web identificadas**: WordPress con plugins conocidos (Elementor, WPML, Simple Job Board) expone panel admin de login en ruta predecible (`/wp-login.php`).
- **Dominio corporativo y subdominios históricos**: Identificados múltiples subdominios a través de DNS pasivo, algunos potencialmente obsoletos sin protección.

**Riesgo global (una frase).**
- **Alto** por exposición significativa de identidades digitales, patrones de contacto y antecedentes de brecha que facilitan ataques dirigidos de phishing e ingeniería social.

**Recomendaciones prioritarias (3-5 bullets).**
- Auditoría urgente de exposición WordPress: aplicar parches, deshabilitar enumeración de usuarios, validar plugins desactualizados (P1).
- Limpieza de información personal en canales públicos (LinkedIn, sitio web): reducir datos de contacto directo de empleados (P1).
- Implementar Autenticación Multifactor (MFA) en cuentas corporativas y sistemas críticos (P1).
- Revisar y rotar credenciales potencialmente comprometidas en brecha verifications.io 2019 (P2).
- Establecer política de publicación de información corporativa y revisión trimestral de OSINT (P2).

## 2. Alcance, supuestos y reglas de compromiso
<!-- AYUDA (BORRAR): Dejad claro QUÉ se ha hecho y QUÉ no (para demostrar OSINT pasivo). Indicad supuestos y límites. -->

**Alcance.** Solo OSINT pasivo sobre la entidad (y su huella pública asociada). No se incluye investigación individual (apartado b).

**Fuentes permitidas (ejemplos).** Motores de búsqueda, hemeroteca, registros públicos, perfiles públicos en RRSS, repositorios públicos, documentos públicos, Wayback/archivos, bases de datos de brechas (consulta pasiva).
<!-- AYUDA (BORRAR): Listad las fuentes reales que usasteis (5-10), no un listado infinito. -->

**Regla crítica.** Prohibida cualquier acción activa: escaneos, enumeración directa de servicios, pruebas de login, interacción con formularios, generación de tráfico hacia los sistemas objetivo.
<!-- AYUDA (BORRAR): Si una herramienta pudiera considerarse “activa”, explicad cómo la usasteis de forma pasiva (solo consultas a datos ya recopilados por terceros). -->

**Minimización y privacidad.**
<!-- AYUDA (BORRAR): Explicad cómo reducís datos personales (enmascarado parcial, iniciales, no incluir PII innecesaria). -->
- Evitar incluir datos personales innecesarios.
- Si aparecen datos personales de terceros (p. ej., correos de empleados), aplicar reducción: mostrar solo lo imprescindible o enmascarar parcialmente cuando no aporte valor al riesgo.

## 3. Metodología (ciclo OSINT)
<!-- AYUDA (BORRAR): Explicad el proceso seguido de forma reproducible (ciclo OSINT) y cómo volvisteis a fases anteriores si fue necesario. -->

Esta sección describe el proceso seguido según el ciclo OSINT: planificación, fuentes, adquisición, procesamiento, análisis y difusión.

### 3.1 Planificación y dirección
<!-- AYUDA (BORRAR): Objetivos, preguntas guía y criterios de priorización. Esto demuestra teoría + método. -->

- Preguntas guía (ejemplos):
  - ¿Qué dominios y marcas usa la entidad?
  - ¿Existen patrones de email/usuarios visibles públicamente?
  - ¿Existen documentos públicos con metadatos reveladores?
  - ¿Hay menciones de tecnologías, proveedores, sedes, organigrama o personal?
  - ¿La entidad aparece asociada a brechas pasadas o leaks públicos?
<!-- AYUDA (BORRAR): Ajustad estas preguntas a lo que realmente investigasteis. -->

- Criterios de priorización:
  - **Facilidad de ingeniería social**: Información de contacto directo o patrones deducibles de credenciales.
  - **Reutilización de credenciales**: Exposiciones en brechas conocidas o fuentes públicas.
  - **Exposición de infraestructura**: Tecnologías identificables, versiones, rutas de acceso predecibles.
  - **Impacto potencial en confidencialidad/integridad**: Información sobre roles críticos o sistemas backend.


- Ventana temporal:
  - Consulta realizada en: 31/01/2026
  - Evidencias archivadas en: `evidencias/` (todas enlazadas en el informe).


### 3.2 Identificación de fuentes
<!-- AYUDA (BORRAR): Fuentes por categoría. Mejor pocas y justificadas. Indicad cómo se mantiene el enfoque pasivo. -->

Tabla de fuentes (añadir/quitar según aplique):
<!-- AYUDA (BORRAR): En “Notas (pasivo)” indicad qué aporta la fuente y por qué no implica interacción con los sistemas objetivo. -->

| Categoría   | Fuente/Herramienta                  | Qué se busca                | Notas (pasivo)              |
|-------------|-------------------------------------|-----------------------------|-----------------------------|
| Buscadores  | Google / Bing / DuckDuckGo          | menciones, PDFs, indexación | dorks sin acceder a paneles |
| Archivo web | Wayback Machine                     | versiones antiguas          | solo lectura                |
| Dominios    | WHOIS/RDAP (consulta)               | datos de registro           | solo consulta pública       |
| DNS pasivo  | dnsdumpster, securitytrails, etc.   | subdominios/histórico       | sin enumeración activa      |
| Brechas     | HIBP / DeHashed (si se usa)         | apariciones en brechas      | no intentar logins          |
| RRSS        | LinkedIn/X/Facebook (público)       | perfiles, roles, nicks      | solo contenido público      |
| Metadatos   | exiftool/FOCA (sobre docs públicos) | autores, rutas, software    | sobre ficheros públicos     |

### 3.3 Adquisición (recopilación)
<!-- AYUDA (BORRAR): Consultas representativas (no todas). Añadid palabras clave, variantes del nombre, ubicaciones, etc. -->

- Consultas realizadas (resumen):
  - `site:jmpascual.com` (directorio general)
  - `site:josemanuelpascualpascual.com` (variante de dominio)
  - `site:hospitalespascual.com` (posibles subdominios)
  - `"jmpascual.com" filetype:pdf` (documentos internos)
  - `"Jose Manuel Pascual" "Cádiz" médicos especialidad` (empleados públicos)
  - `"verifications.io" brecha 2019 correos` (brechas conocidas)
  - `securitytrails subdominios hospitalespascual.com` (DNS histórico)

- Evidencias:
  - Guardar capturas o PDFs en `evidencias/` con nombres: `YYYY-MM-DD_fuente_tema.ext`
  - Registrar URL (y, cuando sea útil, captura) y fecha de acceso en cada hallazgo.
  - Toda evidencia mencionada en el informe debe estar enlazada (URL y/o ruta relativa a `evidencias/`).
<!-- AYUDA (BORRAR): Si una URL cambia o desaparece, la captura/PDF en `evidencias/` es la prueba de trazabilidad. -->

### 3.4 Procesamiento y organización
<!-- AYUDA (BORRAR): Cómo ordenasteis datos: deduplicación, clasificación por categorías y relevancia, y control de calidad. -->

- Normalización:
  - Deduplicación de correos corporativos: descartados duplicados y formatos alternativos.
  - Agrupación por categoría: empleados, tecnología, dominios, brechas, documentos.
  - Verificación de fechas y vigencia: señaladas exposiciones históricas vs. actuales.

- Criterios de calidad:
  - **Fiabilidad**: WHOIS (primaria), registros públicos (primaria), RRSS verificadas (secundaria), brechas conocidas (primaria si verificada).
  - **Fecha y vigencia**: Expuesto actualmente en web/RRSS (crítico), histórico en DNS (medio), en brecha 2019+ (alto).
  - **Corroboración cruzada**: Información triangulada (p. ej., empleado en sitio web + LinkedIn + patrón correo = riesgo alto).

### 3.5 Análisis e interpretación
<!-- AYUDA (BORRAR): Transformad datos en “inteligencia”: vectores habilitados, probabilidad/impacto, y mitigación recomendada. -->

- Correlaciones identificadas:
  - **Patrón correo + empleados públicos**: Correos en patrón `nombre.apellido@jmpascual.com` + perfiles LinkedIn + web hospital = spear phishing altamente probable.
  - **Brecha verifications.io 2019 + reutilización**: ~763M correos expuestos incluyendo empleados → credenciales potencialmente en diccionarios de ataque.
  - **WordPress + plugins conocidos**: Versión identificable (logo) + plugins públicos (Elementor, WPML) + panel `/wp-login.php` visible → vector de ataque (fuerza bruta, vulnerabilidades plugin).
  - **Subdominios históricos sin protección**: DNS pasivo revela servicios antiguos → posible información confidencial o backdoors no actualizados.
  - **Exposición de roles/especialidades + datos médicos**: Directorio público médicos + especialidades + teléfono = ingeniera social dirigida a acceso a historiales.

- Valoración de riesgo: usar una escala simple.
  - Alto: facilita acceso/engaño de alta probabilidad o alto impacto.
  - Medio: aporta información útil, pero requiere pasos adicionales.
  - Bajo: información marginal o muy genérica.
<!-- AYUDA (BORRAR): Justificad el riesgo con una frase (“Alto porque permite suplantación del canal X”, etc.). -->

### 3.6 Difusión
<!-- AYUDA (BORRAR): Explicad a quién va dirigido el informe y cómo se usará (priorizar mitigaciones y concienciación). -->

- Este informe resume hallazgos, evidencia y recomendaciones accionables.
- Presentación clara para audiencias técnicas y no técnicas.

## 4. Herramientas utilizadas
<!-- AYUDA (BORRAR): Incluid solo herramientas realmente usadas y una evidencia por cada una (URL o fichero en `evidencias/`). -->

| Herramienta   | Tipo                          | Uso concreto | Salida/evidencia               |
|---------------|-------------------------------|--------------|--------------------------------|
| [Herramienta] | [Buscador/DNS/Metadatos/etc.] | [Para qué]   | [archivo en evidencias/ o URL] |

## 5. Resultados (hallazgos)
<!-- AYUDA (BORRAR): Parte principal. Cada hallazgo debe ser verificable y tener evidencia enlazada (URL y/o `evidencias/...`). -->

Formato recomendado por hallazgo:
<!-- AYUDA (BORRAR): Copiad esta tabla por cada hallazgo importante (o adaptadla si preferís una tabla global). -->

| Campo           | Contenido                                                                  |
|-----------------|----------------------------------------------------------------------------|
| ID              | A-01                                                                       |
| Categoría       | Contacto / Identidad / Dominio-DNS / Documentos-Metadatos / RRSS / Brechas |
| Descripción     | [Qué se encontró, claro y verificable]                                     |
| Evidencia       | [URL] + `evidencias/...`                                                   |
| Fecha evidencia | [YYYY-MM-DD]                                                               |
| Impacto         | [Qué permite a un atacante]                                                |
| Riesgo          | Alto / Medio / Bajo                                                        |
| Recomendación   | [Mitigación concreta]                                                      |

### 5.1 Identidades digitales (nicks, perfiles, cuentas)

**A-01: Directorio de profesionales en web**
- **Descripción**: Perfiles públicos de médicos con especialidades, fotos e información.
- **Evidencia**: Sitio web y LinkedIn
- **Riesgo**: Alto (facilita spear phishing dirigido)

**A-02: Perfiles de empleados en RRSS**
- **Descripción**: Información de roles y especialidades en LinkedIn, Facebook, Twitter.
- **Evidencia**: Redes sociales corporativas
- **Riesgo**: Medio (facilitación de ingeniería social)

### 5.2 Datos de contacto (emails, teléfonos, estructuras)

**A-03: Patrón de correos corporativos**
- **Descripción**: Correos en formato `nombre.apellido@jmpascual.com` deducible a partir de datos públicos.
- **Evidencia**: [correosynicknames.md](../evidencias/correosynicknames.md)
- **Riesgo**: Alto (CRÍTICO para spear phishing sin enumeración)

**A-04: Teléfonos corporativos públicos**
- **Descripción**: Números: 956017200, 956017444, 956017377 expuestos en sitio web y directorios.
- **Evidencia**: [resumen-ejecutivoPascualSA.md](../evidencias/resumen-ejecutivoPascualSA.md)
- **Riesgo**: Medio (vishing, social engineering)

### 5.3 Dominios, subdominios y huella DNS (pasivo)

**A-05: Dominios corporativos identificados**
- **Descripción**: `jmpascual.com`, `josemanuelpascualpascual.com`, `hospitalespascual.com`.
- **Evidencia**: WHOIS público, [resumen-ejecutivoPascualSA.md](../evidencias/resumen-ejecutivoPascualSA.md)
- **Riesgo**: Medio (mapa de propiedades digitales)

**A-06: Subdominios históricos**
- **Descripción**: Servicios obsoletos identificados vía DNS pasivo sin parches actualizados.
- **Evidencia**: [2026-01-26_securitytrails_subdominios.txt](../evidencias/2026-01-26_securitytrails_subdominios.txt), [2026-01-26_crt.sh_subdominios.csv](../evidencias/2026-01-26_crt.sh_subdominios.csv)
- **Riesgo**: Alto (posibles backdoors, servicios sin actualizar)

### 5.4 Huella documental y metadatos (documentos públicos)

**A-07: Documentos corporativos sin sanitizar**
- **Descripción**: Memorias y PDFs públicos con posible información sensible (rutas, software, autores).
- **Evidencia**: [Memorias-San-Rafael.pdf](../evidencias/Memorias-San-Rafael.pdf)
- **Riesgo**: Medio (metadatos, información técnica)

**A-08: Stack tecnológico identificable**
- **Descripción**: WordPress + Elementor + WPML + Simple Job Board; panel login en `/wp-login.php`; versiones identificables.
- **Evidencia**: [tecnologiasWeb.md](../evidencias/tecnologiasWeb.md), screenshot WordPress login
- **Riesgo**: Alto (facilita búsqueda de CVE, fuerza bruta, enumeración)

### 5.5 Brechas y filtraciones (consulta pasiva)

**A-09: Brecha verifications.io 2019**
- **Descripción**: ~763 millones de correos expuestos; incluye empleados Hospitales Pascual (email, nombre, teléfono, dirección, fecha nacimiento, empleador, cargo).
- **Evidencia**: [brechasDeSeguridad.md](../evidencias/brechasDeSeguridad.md)
- **Impacto**: CRÍTICO - Credenciales reutilizables, información para suplantación
- **Riesgo**: Alto (CRÍTICO - afecta a múltiples empleados actuales/pasados)

## 6. Resumen de riesgos
<!-- AYUDA (BORRAR): Tabla para priorizar: qué arreglar primero (P1), después (P2) y al final (P3). -->

| ID   | Hallazgo (resumen) | Riesgo | Prioridad | Acción recomendada |
|------|--------------------|--------|-----------|--------------------|
| A-01 | Directorio de profesionales en web | Alto | P1 | Reducir datos de contacto directo en web |
| A-02 | Perfiles de empleados en RRSS | Medio | P2 | Auditar y limitar información pública |
| A-03 | Patrón correos corporativos | Alto | P1 | Implementar MFA obligatorio |
| A-04 | Teléfonos públicos | Medio | P2 | Entrenar en detección de vishing |
| A-05 | Dominios corporativos | Medio | P2 | Auditar DNS records y DNSSEC |
| A-06 | Subdominios históricos | Alto | P1 | Auditar y desactivar servicios obsoletos |
| A-07 | Documentos sin sanitizar | Medio | P2 | Sanitizar metadatos antes de publicar |
| A-08 | Stack WordPress identificable | Alto | P1 | Parches, ocultar versiones, implementar WAF |
| A-09 | Brecha verifications.io 2019 | Alto | P1 | Rotar credenciales y implementar MFA |

## 7. Conclusiones

- **Exposición significativa de identidades digitales**: La combinación de directorio público (web/RRSS) + patrón correo deducible + brecha 2019 crea superficie de ataque muy vulnerable a spear phishing dirigido y social engineering.

- **Stack tecnológico visible facilita explotación**: WordPress público con plugins identificables y panel login predecible permite ataque automatizado (fuerza bruta, exploits públicos). Falta de versión oculta/WAF incrementa probabilidad.

- **Subdominios históricos sin ciclo de vida**: DNS pasivo revela servicios antiguos potencialmente sin actualizar, posibles backdoors o acceso heredado sin protección.

- **Brecha verifications.io afecta directamente**: ~763M registros expuestos incluyendo empleados significa credenciales probablemente en diccionarios atacantes. Reutilización de contraseñas = riesgo alto.

- **Información médica + roles sensibles**: Exposición de especialidades y teléfono permite suplantación de profesionales médicos con alto impacto en confidencialidad de pacientes.

## 8. Recomendaciones

**Quick wins (0-30 días)** — Responsable sugerido: **TI / Seguridad**

- **Parches críticos WordPress** (P1): Actualizar core, todos los plugins; ocultar versiones; activar WAF (ModSecurity o Cloudflare).
- **Implementar MFA** (P1): Obligatorio en cuentas corporativas, especialmente dominios críticos (email, admin, médicos).
- **Limpieza de directorio público** (P1): Reducir información de contacto directo en web; retirar números de teléfono si es posible; usar formulario de contacto opaco.
- **Auditar y desactivar subdominios obsoletos** (P1): Conectar con equipo de infraestructura; retirar servicios sin uso (mail antiguo, FTP, admin panels).
- **Concienciación urgente phishing** (P1): Email a todos empleados sobre patrón phishing + brecha 2019; entrenar en verificación de identidad.

**Medio plazo (1-3 meses)** — Responsable sugerido: **Seguridad / RRHH / Comunicación**

- **Política de ciclo de vida de DNS**: Auditoría trimestral de dominios/subdominios; desactivación automática de servicios fuera de vida útil.
- **Sanitización de documentos**: Herramienta automatizada (exiftool) antes de publicación; auditar documentos históricos.
- **Auditoría de credenciales en brecha**: Cruzar empleados actuales/pasados contra verifications.io y HIBP; rotar obligatoriamente si están en leak.
- **Política de información corporativa pública**: Qué puede publicarse (roles, especialidades, contacto); revisar LinkedIn corporativo, web, directorios.
- **Implementar DNSSEC + DMARC/SPF/DKIM**: Proteger contra spoofing de dominio; monitorizar intentos phishing.

**Mejora continua** — Responsable sugerido: **Seguridad / TI**

- **Monitorización OSINT trimestral**: Revisar exposición de dominio, empleados, tecnología públicamente; reportar hallazgos.
- **Playbook de respuesta**: Procedimiento si empleado reporta phishing; escalada a SOC si es dirigido.
- **Auditoría anual de superficie de ataque**: Repetir este estudio; medir reducción de exposición.

## 9. Anexos
<!-- AYUDA (BORRAR): Trazabilidad. Esta sección facilita la corrección: fuentes, consultas y evidencias enlazadas. -->

### 9.1 Registro de fuentes

| Fuente   | URL / Descripción | Fecha acceso | Nota |
|----------|-------------------|--------------|------|
| WHOIS / Registro | jmpascual.com, josemanuelpascualpascual.com | 2026-01-21 | Consulta pública pasiva |
| SecurityTrails | DNS histórico + subdominios | 2026-01-26 | Datos públicos pasivos (no activos) |
| Google Search | `site:jmpascual.com`, `site:hospitalespascual.com` | 2026-01-20 | Indexación web pública |
| LinkedIn | Hospitales Pascual corporativo | 2026-01-22 | Perfil corporativo público |
| Facebook | San Rafael Cádiz | 2026-01-22 | Página oficial pública |
| Twitter/X | @sanrafaelcadiz | 2026-01-22 | Cuenta oficial pública |
| Have I Been Pwned / Dehashed | verifications.io brecha 2019 | 2026-01-28 | Consulta pasiva sobre leaks |
| Sitio web | hospitalespascual.com | 2026-01-20 | Directorio público de médicos |
| Documentos públicos | Memorias-San-Rafael.pdf | 2026-01-20 | PDF publicado sin sanitizar |

### 9.2 Consultas (dorks) empleadas

(Consultas pasivas ejecutadas via Google / Bing sin acceso a paneles o sistemas objetivo)

- `site:jmpascual.com` - Indexación general dominio
- `site:josemanuelpascualpascual.com` - Variante dominio
- `site:hospitalespascual.com` - Posibles subdominios
- `"jmpascual.com" "@jmpascual.com" email` - Patrones correo
- `site:jmpascual.com filetype:pdf` - Documentos PDF públicos
- `"Jose Manuel Pascual" "Cádiz" médicos especialidad` - Empleados públicos
- `"verifications.io" brecha 2019 correos expuestos` - Investigación brecha
- `linkedin.com/company/jose-manuel-pascual` - Perfil corporativo
- `facebook.com/sanrafaelcadiz` - Redes sociales
- `securitytrails subdominios hospitalespascual` - DNS histórico

### 9.3 Evidencias (índice)

Todas las evidencias están archivadas en `evidencias/` y enumeradas a continuación:

- [tecnologiasWeb.md](../evidencias/tecnologiasWeb.md) - Stack web identificado: WordPress, Elementor, WPML, plugins
- [resumen-ejecutivoPascualSA.md](../evidencias/resumen-ejecutivoPascualSA.md) - Datos corporativos: NIF, domicilio, teléfonos, estructura
- [correosynicknames.md](../evidencias/correosynicknames.md) - Tabla de empleados y patrones correo deducibles
- [brechasDeSeguridad.md](../evidencias/brechasDeSeguridad.md) - Resumen brecha verifications.io 2019
- [JoseManuelPascual.md](../evidencias/JoseManuelPascual.md) - Perfil de empleado clave
- [demandasHospital.md](../evidencias/demandasHospital.md) - Antecedentes legales/litigios
- [2026-01-26_securitytrails_subdominios.txt](../evidencias/2026-01-26_securitytrails_subdominios.txt) - DNS histórico via SecurityTrails
- [2026-01-26_crt.sh_subdominios.csv](../evidencias/2026-01-26_crt.sh_subdominios.csv) - Subdominios via CT logs
- [2026-01-26_whois_dns.txt](../evidencias/2026-01-26_whois_dns.txt) - WHOIS DNS público
- [2026-01-26_whois_duenoip.txt](../evidencias/2026-01-26_whois_duenoip.txt) - WHOIS propietario IP
- [Memorias-San-Rafael.pdf](../evidencias/Memorias-San-Rafael.pdf) - Documento corporativo con posibles metadatos
- Screenshot WordPress login - Panel admin en ruta `/wp-login.php` visible
