# IS 2.d.02 (a) - Auditoría de Superficie de Exposición Post-Incidente (OSINT pasivo)
- Entidad objetivo: Clínica de San Rafael de Cádiz

- Equipo/Grupo: Grupo 2

- Integrantes: [Pablo González Silva], [Carlos Alcina Romero] y [Luis Carlos Romero Navarro]

- Fecha(s) de investigación: [2026-01-26 a 2026-02-01]

- Versión: 1.0

- Límite de entrega (a): máximo 6 folios (12 caras) en PDF (si aplica)

## 1. Resumen ejecutivo
Durante el periodo 2026-01-26 a 2026-02-01 se realizó una auditoría OSINT pasiva sobre la huella pública asociada al Hospital San Rafael (Cádiz) y su presencia digital vinculada (web corporativa, perfiles y fuentes de terceros ya recolectadas). El objetivo fue identificar información disponible antes del incidente supuesto que facilitase el reconocimiento: estructura de dominios/subdominios, exposición de canales de correo y administración, tecnologías empleadas, publicación de personal/roles y referencias públicas relevantes. Se consultaron fuentes de DNS pasivo/CT logs (p. ej., SecurityTrails/crt.sh), registros públicos (p. ej., RIPE), y contenidos accesibles públicamente (p. ej., web corporativa/directorios). Los hallazgos muestran una combinación de exposición organizativa (roles y nombres) y exposición técnica (subdominios y stack) que reduce el coste de preparación de ataques de phishing/suplantación y ayuda a perfilar infraestructura y proveedores.

**Objetivo.** Determinar qué información pública existía (antes del incidente supuesto) que podría haber facilitado la fase de reconocimiento de un atacante: identidades digitales, contactos, dominios/subdominios, huella documental (metadatos), menciones públicas y exposiciones derivadas.

**Hallazgos clave (3-7 bullets).**
- Se observan múltiples subdominios orientados a correo y administración (p. ej., autodiscover, webmail/cpanel/whm, ftp, webdisk, test), identificables por fuentes pasivas; esto facilita el mapeo de superficie y la preparación de campañas de suplantación.
- La configuración DNS/MX publica rutas de correo (p. ej., servidor principal y backup), lo que permite a un atacante adaptar señuelos (phishing/BEC) a los canales reales de la organización.
- El sitio web parece basarse en WordPress y plugins conocidos (p. ej., Elementor/WPML), y se identifica la existencia de panel de administración; conocer el stack reduce el esfuerzo de búsqueda de vulnerabilidades y de ingeniería social técnica.
- Existe un directorio público con nombres y cargos/especialidades de personal (incluyendo roles de dirección), complementable con perfiles profesionales públicos; esto habilita spear phishing altamente dirigido.
- Se hallaron referencias a exposición en brechas de terceros (p. ej., verifications.io) y a información corporativa/registral pública; esto puede alimentar intentos de reutilización de credenciales y pretextos creíbles.

**Riesgo global (una frase).**
- Medio por la combinación de exposición de identidades/roles y huella técnica (subdominios, correo y tecnologías), que incrementa la probabilidad y efectividad de ataques de ingeniería social y abuso de servicios expuestos.

**Recomendaciones prioritarias (3-5 bullets).**
- Reducir la exposición de subdominios sensibles: despublicar los no necesarios (p. ej., entornos “test”) y restringir el acceso a paneles de administración/correo (WAF, allowlist/VPN, 2FA).
- Minimizar datos personales publicados: revisar el “cuadro médico” y contenidos para limitar detalles no imprescindibles (especialmente roles de dirección) y evitar publicación directa de correos/telefonía cuando no aporte valor.
- Gestionar el riesgo del CMS: inventario de plugins, actualización y hardening de WordPress (2FA, control de accesos, desactivar superficies no usadas, monitorización de vulnerabilidades).
- Implantar monitorización continua de exposición: alertas de CT logs/DNS pasivo, seguimiento de menciones y revisión periódica de brechas que afecten a dominios corporativos.

## 2. Alcance, supuestos y reglas de compromiso
**Alcance.** Investigación OSINT estrictamente pasiva sobre la entidad objetivo (Clínica/Hospital San Rafael de Cádiz) y su huella pública asociada: presencia web, información corporativa pública, huella de dominios/subdominios observada por terceros, y perfiles profesionales/páginas públicas relacionadas. Se excluye deliberadamente la investigación individual en profundidad (apartado b) y cualquier verificación técnica activa.

**Ventana temporal y supuestos.**
- Ventana de consulta: 2026-01-26 a 2026-02-01.
- Los datos reflejan lo que terceros y fuentes públicas mostraban en la fecha de consulta; pueden existir cambios posteriores (alta/baja de subdominios, cambios de proveedor, modificaciones de contenido).
- La presencia de un subdominio o certificado en fuentes pasivas no implica necesariamente que el servicio estuviera accesible en el momento de la investigación.

**Fuentes consultadas (OSINT pasivo, 5-10).**
- Web corporativa/directorios públicos (p. ej., cuadro médico y páginas informativas): evidencia en `evidencias/Trabajadores-Web.txt` y `evidencias/Tabla-Trabajadores-Web.md`.
- DNS pasivo / histórico de subdominios (p. ej., SecurityTrails): evidencia en `evidencias/2026-01-26_securitytrails_subdominios.txt`.
- Certificate Transparency / CT logs (p. ej., crt.sh): evidencia en `evidencias/2026-01-26_crt.sh_subdominios.csv`.
- Registros de red/propiedad IP (p. ej., RIPE): evidencia en `evidencias/2026-01-26_whois_duenoip.txt`.
- Consultas DNS públicas exportadas (p. ej., A/NS/MX/SOA): evidencia en `evidencias/2026-01-26_whois_dns.txt`.
- Información tecnológica publicada por terceros/proveedor (p. ej., stack WordPress y referencias públicas): evidencia en `evidencias/tecnologiasWeb.md`.
- Bases de datos/noticias de brechas de terceros (consulta pasiva): evidencia en `evidencias/brechasDeSeguridad.md`.
- Fuentes judiciales y hemeroteca/registro público (consulta y lectura): evidencia en `evidencias/demandasHospital.md`.
- Perfiles profesionales públicos (p. ej., LinkedIn) únicamente para confirmar rol/posición pública: evidencias en `evidencias/IreneMoyaGarcia.md` y `evidencias/SergioMunozPinero.md`.
- Datos corporativos públicos (identificación y contacto publicados): evidencia en `evidencias/resumen-ejecutivoPascualSA.md`.

**Regla crítica (no actividad).**
- No se han realizado escaneos, enumeración directa de servicios, fingerprinting activo, pruebas de login, ni interacción con formularios.
- No se han lanzado peticiones deliberadas a paneles, webmail, cPanel/WHM u otros endpoints con el objetivo de comprobar disponibilidad o extraer banners.
- En caso de usar herramientas que podrían emplearse activamente, se han usado solo como consulta de datos ya recolectados por terceros (DNS pasivo/CT logs), sin generar tráfico hacia la infraestructura objetivo.

**Minimización y privacidad.**
- Se evita incluir datos personales innecesarios (p. ej., fecha de nacimiento, teléfonos personales, imágenes de perfil) cuando no aportan al análisis de riesgo.
- Cuando es suficiente para justificar el hallazgo, se prioriza describir roles/funciones sobre identificar a personas concretas.
- Si aparece información de contacto o identificadores personales, se recomienda enmascarado parcial o reducción al mínimo (p. ej., mostrar solo dominio o patrón, no direcciones completas).

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
  - Impacto potencial en ingeniería social.
  - Reutilización de credenciales/patrones.
  - Exposición de infraestructura por huella documental/histórica.
<!-- AYUDA (BORRAR): Indicad 2-4 criterios máximo y cómo los aplicasteis. -->

- Ventana temporal:
  - Consulta realizada en: [YYYY-MM-DD]
  - Evidencias archivadas en: `evidencias/` (todas deben quedar enlazadas en el informe).
<!-- AYUDA (BORRAR): Si usasteis Wayback, indicad el rango de años consultado. -->

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
  - [Query/dork 1]
  - [Query/dork 2]
  - [Query/dork 3]

- Evidencias:
  - Guardar capturas o PDFs en `evidencias/` con nombres: `YYYY-MM-DD_fuente_tema.ext`
  - Registrar URL (y, cuando sea útil, captura) y fecha de acceso en cada hallazgo.
  - Toda evidencia mencionada en el informe debe estar enlazada (URL y/o ruta relativa a `evidencias/`).
<!-- AYUDA (BORRAR): Si una URL cambia o desaparece, la captura/PDF en `evidencias/` es la prueba de trazabilidad. -->

### 3.4 Procesamiento y organización
<!-- AYUDA (BORRAR): Cómo ordenasteis datos: deduplicación, clasificación por categorías y relevancia, y control de calidad. -->

- Normalización:
  - Deduplicación de correos/teléfonos/dominios.
  - Agrupación por categoría (contacto, identidad, infra, documentos).

- Criterios de calidad:
  - Fiabilidad de la fuente (primaria vs. terciaria).
  - Fecha y vigencia (actual vs. histórico).
  - Corroboración cruzada (>= 2 fuentes cuando sea posible).
<!-- AYUDA (BORRAR): Indicad qué hallazgos NO pudisteis corroborar y por qué. -->

### 3.5 Análisis e interpretación
<!-- AYUDA (BORRAR): Transformad datos en “inteligencia”: vectores habilitados, probabilidad/impacto, y mitigación recomendada. -->

- Correlaciones (ejemplos):
  - Patrones de email + nombres de empleados + roles (posible spear phishing).
  - Documentos públicos -> metadatos -> nombres de usuario/software.
  - Dominios/subdominios históricos -> superficies olvidadas.
<!-- AYUDA (BORRAR): Añadid 2-5 correlaciones reales. Mejor pocas y buenas. -->

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
<!-- AYUDA (BORRAR): Perfiles corporativos, posibles empleados/roles (solo info pública), y “pivots” para ingeniería social. -->

- A-01
- A-02

### 5.2 Datos de contacto (emails, teléfonos, estructuras)
<!-- AYUDA (BORRAR): Patrones de correo (si se infieren), teléfonos publicados, extensiones, formularios de contacto y riesgos asociados. -->

- A-03
- A-04

### 5.3 Dominios, subdominios y huella DNS (pasivo)
<!-- AYUDA (BORRAR): Dominios oficiales/variantes y subdominios observados en fuentes pasivas/históricas. Evitad enumeración activa. -->

- A-05
- A-06

### 5.4 Huella documental y metadatos (documentos públicos)
<!-- AYUDA (BORRAR): Documentos públicos y metadatos relevantes (autor, software, rutas, fechas). Adjuntad evidencia. -->

- A-07
- A-08

### 5.5 Brechas y filtraciones (consulta pasiva)
<!-- AYUDA (BORRAR): Aparición del dominio/correos en brechas conocidas. No incluyáis contraseñas. Priorizad mitigaciones (2FA, rotación, etc.). -->

- A-09

## 6. Resumen de riesgos
<!-- AYUDA (BORRAR): Tabla para priorizar: qué arreglar primero (P1), después (P2) y al final (P3). -->

| ID   | Hallazgo (resumen) | Riesgo | Prioridad | Acción recomendada |
|------|--------------------|--------|-----------|--------------------|
| A-01 | [..]               | Alto   | P1        | [..]               |
| A-02 | [..]               | Medio  | P2        | [..]               |
| A-03 | [..]               | Bajo   | P3        | [..]               |

## 7. Conclusiones
<!-- AYUDA (BORRAR): 3-6 bullets: qué superficie pública existía y qué vector pudo facilitar. Sin repetir texto, aportad síntesis. -->

- [Conclusión 1: qué explica la exposición encontrada y por qué importa]
- [Conclusión 2]
- [Conclusión 3]

## 8. Recomendaciones
<!-- AYUDA (BORRAR): Convertid hallazgos en acciones concretas. Si podéis, asignad responsable sugerido (IT/Seguridad/RRHH/Comunicacion). -->

**Quick wins (0-30 días)**
<!-- AYUDA (BORRAR): Cambios rápidos: retirar/editar documentos, sanear metadatos, ajustar contenidos públicos, concienciación inmediata. -->
- [..]
- [..]

**Medio plazo (1-3 meses)**
<!-- AYUDA (BORRAR): Cambios estructurales: políticas de publicación, revisión periódica, procesos, formación, controles de identidad. -->
- [..]

**Mejora continua**
<!-- AYUDA (BORRAR): Medidas recurrentes: monitorización de menciones, revisiones trimestrales de exposición, playbook OSINT. -->
- [..]

## 9. Anexos
<!-- AYUDA (BORRAR): Trazabilidad. Esta sección facilita la corrección: fuentes, consultas y evidencias enlazadas. -->

### 9.1 Registro de fuentes
<!-- AYUDA (BORRAR): Fuentes base consultadas (URL + fecha). No hace falta duplicar cada evidencia si ya está en hallazgos, pero sí lo principal. -->

| Fuente   | URL  | Fecha acceso | Nota |
|----------|------|--------------|------|
| [Fuente] | [..] | [YYYY-MM-DD] | [..] |

### 9.2 Consultas (dorks) empleadas
<!-- AYUDA (BORRAR): Dejad 5-15 consultas representativas. Deben ser pasivas y reproducibles. -->

(Registrar aquí las consultas utilizadas. Evitar incluir acciones activas o instrucciones de acceso.)

- `site:[dominio] filetype:pdf [palabra clave]`
- `site:[dominio] "@[dominio]"`
- `"Clínica San Rafael" "Cádiz" [palabra clave]`

### 9.3 Evidencias (índice)
<!-- AYUDA (BORRAR): Índice con enlaces relativos a ficheros dentro de `evidencias/`. Debe permitir abrir cada evidencia sin buscar. -->

<!-- AYUDA (BORRAR): Ejemplo de enlace: `[2026-01-27 - Google - PDF organigrama](../evidencias/2026-01-27_google_organigrama.pdf)` -->

- `evidencias/`:
  - `YYYY-MM-DD_fuente_tema.ext` - [descripción]
