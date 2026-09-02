# Referencia maestra de casos, capacidades y contenido

**Yaocalli Consultoría y Estrategia**
Documento interno de trabajo · Versión 1.0 · 1 de septiembre de 2026

---

## Qué es esto y cómo se usa

Este archivo consolida todo el material fuente disponible sobre el trabajo realizado, ordenado en la forma en que el sitio lo va a necesitar. No es un documento para publicar: es la materia prima desde la que se redactan las fichas de servicio, las fichas de caso, las notas metodológicas y la página de quiénes somos.

Cada afirmación aquí proviene de los tres documentos fuente. Lo que no está respaldado por ellos aparece marcado como **pendiente** o **por verificar**, y no debe llegar al sitio sin confirmación.

**Fuentes consolidadas:**

| Fuente | Contenido | Uso principal |
|---|---|---|
| `portafolio_inteligencia_politica.md` | Seis áreas de trabajo con proyectos, metodología y tecnología | Casos, fichas de servicio, inventario técnico |
| `Indice_Municipal_de_Prioridad_para_la_Asistencia_Social_2026` | Documento metodológico completo del IMPAS, DIF Mineral de la Reforma | Caso, notas de priorización y focalización |
| `Diseno_Metodologico_CCA_Presupuesto_2027_consolidado` | Diseño metodológico del diagnóstico participativo, Mineral de la Reforma | Caso, notas de muestreo y participación |

**Regla de oro para redactar desde aquí:** ninguna cifra pasa al sitio sin su fuente y su fecha. Es el pilar de método auditable del manual de identidad, y aplica también a las cifras propias.

---

## 1. Perfil y posicionamiento

**Cómo se describe el perfil en el portafolio:** liderazgo en ciencia de datos y desarrollo de software de alta dirección, especializado en traducir datos masivos de opinión pública, demografía, territorio e infraestructura en herramientas dinámicas para la toma de decisiones estratégicas.

**Competencias declaradas:** backend, procesamiento de lenguaje natural, modelos de aprendizaje automático para análisis de sentimientos, mapeo geoespacial avanzado y automatización de procesos a gran escala.

**Traducción al posicionamiento del sitio** (definido en el documento 01): *la casa donde el dato se vuelve decisión*. La mayoría de las casas encuestadoras entregan un número; aquí se entrega el número, el instrumento que lo produjo, la ficha técnica que lo respalda y el sistema con el que se puede volver a levantar el año siguiente.

---

## 2. Casos de estudio

Formato uniforme para pasar directo a la ficha de caso del sitio: institución, año, escala, problema, qué se hizo, resultado, servicios aplicados y estado de confidencialidad.

---

### Caso A · Auditoría territorial de transporte y movilidad a escala estatal

**Institución:** pendiente de confirmar si es publicable con nombre
**Escala:** 84 municipios · 80 encuestadores en campo · 30 auditores de gabinete
**Servicios aplicados:** encuestas y opinión pública · cartografía y análisis territorial · software y automatización

**El problema.** Diseñar e instrumentar una auditoría territorial masiva de infraestructura y percepción del transporte público y privado a nivel estatal, con cobertura completa del estado y control de calidad verificable.

**Qué se hizo.**

- Backend en Django sobre infraestructura contenerizada con Docker y Docker Compose, integrado con base de datos relacional y geoespacial en PostgreSQL con PostGIS.
- Aplicación móvil offline-first en React Native, Express y SQLite para encuestadores en campo: inicio de sesión único, almacenamiento local de catálogos y sincronización masiva asíncrona al recuperar conexión.
- Seguimiento coordinado de más de 80 encuestadores simultáneos en territorio y equipo de gabinete de 30 auditores para control de calidad, limpieza de datos y eliminación de duplicados.
- Monitoreo georreferenciado por municipio del avance del levantamiento en los 84 municipios del estado.
- Importación de trazas completas de rutas en formato GPX recolectadas con rastreadores GPS.
- Generación de *buffers* geográficos con la Red Nacional de Caminos para calcular cobertura espacial y cruzarla con datos demográficos del INEGI a nivel microlocal.
- Matrices de correlación estadística sobre las encuestas de percepción para medir eficiencia y satisfacción del usuario.

**Por qué es el caso más fuerte del portafolio.** Es el único que demuestra las tres capacidades al mismo tiempo: campo a gran escala, geoespacial fino y software propio. Ningún competidor identificado en el benchmark ofrece esa combinación.

**Uso en el sitio:** caso destacado de la página de inicio y prueba principal de la ficha de encuestas. Alimenta la nota de enero sobre control de calidad en levantamientos grandes.

---

### Caso B · Índice Municipal de Prioridad para la Asistencia Social (IMPAS)

**Institución:** Sistema Municipal para el Desarrollo Integral de la Familia de Mineral de la Reforma, Hidalgo
**Periodo:** ejercicio fiscal 2026, anexo técnico
**Servicios aplicados:** índices y priorización · software y automatización · tableros y visualización

**El problema.** El organismo debía ordenar con criterios verificables la asignación de los apoyos de asistencia social. El problema tenía dos caras: una sustantiva, cómo identificar quién necesita más; y una operativa, cómo hacerlo de forma homogénea entre casos y entre personas aplicadoras, y dejar rastro de la decisión.

**Qué se hizo.** Un instrumento de valoración, focalización y prelación que traduce la condición social de una persona solicitante y de su hogar a una escala continua de 0 a 100 puntos, integrada por seis dimensiones ponderadas:

| Dimensión | Puntos |
|---|---|
| Condición económica del hogar | 25 |
| Inseguridad alimentaria | 20 |
| Condición de vulnerabilidad prioritaria | 15 |
| Red de apoyo y apoyos sociales | 15 |
| Condiciones de salud y funcionalidad | 15 |
| Condiciones de vivienda | 10 |

El puntaje clasifica cada solicitud en cuatro niveles de prioridad —muy alta, alta, media y baja— que orientan la incorporación al padrón, la periodicidad sugerida de atención y, en su caso, la canalización a otras instancias.

**Los seis componentes del sistema:**

| Componente | Qué resuelve |
|---|---|
| Instrumento de valoración | Cuestionario único de seis bloques ponderados más bloque administrativo y bloque de revisión social. Captura homogénea y comparable |
| Escala de 100 puntos | Suma ponderada con topes por dimensión y conversión de escalas de severidad. Prelación objetiva |
| Ajuste cualitativo colegiado | Margen documentado de −5 a +5 puntos posterior al puntaje base. Sensibilidad sin discrecionalidad abierta |
| Banderas automáticas | Alertas de expediente, duplicidad, caso sensible, evidencia insuficiente y concentración territorial |
| Plataforma de soporte | Expediente digital, motor de reglas versionado, dictamen, padrón, entregas y reportes |
| Sistema de indicadores | Métricas de proceso, focalización, producto, resultado, equidad y auditoría |

**La decisión de diseño que más vale contar.** El Índice **no es un mecanismo de decisión automática**. Es un modelo de decisión pública asistida por evidencia: calcula un puntaje base con reglas explícitas y versionadas, genera banderas de revisión, ordena la prelación y conserva un margen acotado de ajuste colegiado que solo procede con evidencia documentada y acta. No sustituye la valoración social profesional: la ordena, la hace comparable y le proporciona un registro trazable.

**Fundamentación documental.** Revisión en cuatro escalas territoriales, con cada referente desembocando en dimensiones y reactivos concretos del instrumento, y una matriz de trazabilidad que permite remitir cualquier pregunta aplicada en ventanilla a un fundamento documental identificable y a una regla de cálculo verificable.

- **Internacional:** medición experiencial de inseguridad alimentaria de la FAO; enfoque de análisis de seguridad alimentaria del Programa Mundial de Alimentos; Clasificación Internacional del Funcionamiento de la OMS y herramientas del Grupo de Washington sobre estadísticas de la discapacidad; escalas de dependencia funcional de Barthel, Katz y Lawton y Brody; literatura del Banco Mundial sobre registros sociales; evidencia crítica sobre comprobación sustitutiva de medios; experiencia comparada de Chile, Colombia, Brasil y Perú.
- **Nacional:** medición multidimensional de la pobreza a cargo del INEGI; Cuestionario Único de Información Socioeconómica y Sistema de Focalización de Desarrollo; índices de marginación de CONAPO y de rezago social de CONEVAL; herramientas de focalización del SNDIF; Encuesta Nacional de Salud y Nutrición Continua.
- **Estatal:** marco de asistencia social de Hidalgo y sus instrumentos de planeación y operación.
- **Municipal:** perfil sociodemográfico y de carencias de Mineral de la Reforma.

**Uso en el sitio:** caso principal de la ficha de índices y priorización. Alimenta las notas de diciembre sobre criterios de priorización y sobre la diferencia entre marginación, rezago y pobreza.

---

### Caso C · Diagnóstico participativo para el anteproyecto de presupuesto 2027

**Institución:** Secretaría de Bienestar para la Comunidad, Dirección de Desarrollo Social, Inclusión y Aprendizaje, Presidencia Municipal de Mineral de la Reforma, Hidalgo
**Objeto:** Centros Comunitarios de Aprendizaje y su oferta formativa
**Servicios aplicados:** encuestas y opinión pública · índices y priorización · tableros y visualización

**El problema.** Sustentar con evidencia el anteproyecto de presupuesto 2027 de la red de Centros Comunitarios de Aprendizaje, en un municipio que pasó de 127 404 habitantes en 2010 a 202 749 en 2020 —un crecimiento de 59.1 % en una década, tres veces superior al de la capital estatal— con una demanda de equipamiento comunitario que no se genera de forma gradual sino en bloques simultáneos por la instalación de fraccionamientos de interés social.

**Contexto sociodemográfico documentado:**

- 202 749 habitantes en 2020; 52.5 % mujeres y 47.5 % hombres; segundo municipio más poblado de Hidalgo, con 6.6 % de la población estatal.
- La mitad de la población tiene 30 años o menos; 145 587 personas (71.8 %) son mayores de 18 años; 17 477 personas (8.6 %) tienen 60 años o más.
- Estimaciones CONEVAL 2020: 17.5 % en pobreza moderada, 1.21 % en pobreza extrema, 36.6 % vulnerable por carencias sociales y 6.41 % vulnerable por ingresos. Aproximadamente 55.3 % presentaba al menos una carencia social.

**Qué se hizo.** Tres instrumentos dirigidos a los tres actores que concurren en el espacio comunitario —personas usuarias, instructoras y administradoras— sobre un marco común de seis dimensiones analíticas, con escalas homologadas y clave común de vinculación Centro Comunitario × taller para permitir cruce sistemático y triangulación.

| Dimensión | Contenido |
|---|---|
| D1 | Condiciones físicas y mantenimiento |
| D2 | Equipamiento, materiales e inventario |
| D3 | Oferta formativa, demanda y cobertura |
| D4 | Gestión, atención y seguridad del espacio |
| D5 | Resultados percibidos y valor público |
| D6 | Priorización y disposición presupuestal |

**Diseño muestral, con los números exactos:**

- Marco construido desde el concentrado de matrícula del ciclo anterior: **1 733 inscripciones en 183 grupos y 16 sedes**, con 1 490 mujeres (86.0 %) y 243 hombres (14.0 %).
- Muestra estratificada por Centro con afijación mixta —mínimo garantizado por sede más asignación proporcional— y corrección por población finita.
- **Escenario A:** n = 380, error máximo de ±4.4 puntos porcentuales a nivel municipal con 95 % de confianza.
- **Escenario B, recomendado:** n = 600, ±3.2 puntos porcentuales a nivel municipal y de ±8.6 a ±16.3 puntos por sede, equivalentes a ±0.17 a ±0.33 puntos en las escalas ordinales de 1 a 5. Precisión suficiente para elaborar fichas técnicas por Centro.
- **Diseño censal** para instructoras y administradoras, justificado formalmente porque el tamaño requerido para muestra probabilística con error de 5 % —124 de 183 asignaciones— prácticamente agota la población.
- Tamaño operativo con supuesto conservador de 15 % de no respuesta: n(op) = 314.6 ÷ 0.85 = 370.1 ≈ 371.

**Estrategia de análisis en cinco capas encadenadas:**

0. Depuración, ponderación y tratamiento de datos faltantes.
1. Validación psicométrica: consistencia interna, adecuación muestral y análisis factorial.
2. Índices dimensionales en escala 0–100 y reducción de dimensionalidad por componentes principales, la misma técnica que CONEVAL emplea para construir el Índice de Rezago Social.
3. Asociación y contraste entre instrumentos, con modelos de respuesta ordinal y aprendizaje supervisado para identificar factores que restringen la participación.
4. Integración en un **Índice de Prioridad Presupuestal** que traduce la evidencia en un ordenamiento auditable de necesidades y en escenarios de asignación por sede y por rubro.

**Cuatro decisiones metodológicas declaradas por anticipado:** vector derivado con corrección por tamaño de bloque para la preferencia presupuestal; estimación del factor de duplicidad desde padrón único, reportando sobre base de inscripciones mientras no exista; análisis de cobertura territorial a nivel de sede según colonias de influencia declaradas; y escala de cuatro puntos sin punto medio en D4, que exige denominador específico en la normalización y correlaciones policóricas en la validación factorial.

**Controles de calidad que conviene contar en el sitio:**

- Capacitación certificada de seis horas para todo el personal aplicador, que cubre marco conceptual, lectura literal de cada reactivo, preguntas condicionadas, protocolo de consentimiento informado y criterios de no inducción de respuesta, y concluye con ejercicio de aplicación supervisada.
- Identificador operativo no nominativo registrado en bitácora para detectar si una persona ya respondió en otro grupo o sede.
- Umbral de consistencia interna de α ≥ 0.70 por escala, con revisión de reactivos cuya eliminación eleve α en más de 0.03; ω de McDonald como verificación complementaria en escalas de cuatro puntos.
- Prueba cognitiva previa con 12 personas usuarias, 4 instructoras y 2 administradoras, con protocolo de pensamiento en voz alta y criterio de comprensión unívoca en al menos 11 de 12 casos por reactivo.
- Reposición de no respuesta dentro del mismo grupo o familia temática y sede, nunca entre sedes, porque alteraría la afijación y por tanto los ponderadores.
- Redundancia informativa controlada: cada dimensión se mide desde al menos dos de los tres instrumentos. Cuando las tres poblaciones convergen, la evidencia es robusta; cuando divergen, la divergencia es en sí misma un hallazgo que orienta la verificación en campo.

**Uso en el sitio:** caso de la ficha de encuestas y de la de índices. Alimenta las notas de octubre sobre tamaño de muestra, de noviembre sobre margen de error y de enero sobre presupuesto participativo.

---

### Caso D · Roots ID, análisis de redes de complejidad en trámites gubernamentales

**Institución:** nivel estatal y municipal, incluidas universidades, dependencias y enlaces
**Escala:** más de 600 usuarios activos diarios · más de 900 trámites digitalizados · construido en menos de dos meses
**Servicios aplicados:** software y automatización · tableros y visualización

**El problema.** Optimizar los trámites y servicios gubernamentales mediante un mapeo analítico del flujo de la administración pública.

**Qué se hizo.**

- Sistema de administración gubernamental desarrollado en menos de dos meses que conectó a más de 600 usuarios activos diarios a nivel estatal y municipal.
- Carga y digitalización de más de 900 trámites administrativos con sus requisitos normativos.
- **Modelo de redes de complejidad:** diseño de un modelo de nodos y relaciones para estudiar el árbol de requisitos y la complejidad burocrática de los trámites.
- A través del análisis de grafos se identificaron cuellos de botella normativos y duplicidades, priorizando qué trámites intervenir dentro de la Estrategia Anual de Simplificación Administrativa y Digitalización.
- Visualización y reporte ejecutivo en paneles interactivos de Power BI y Looker Studio.

**Uso en el sitio:** caso de la ficha de software y automatización. Es la mejor demostración de velocidad de entrega. Alimenta la nota de reserva sobre modelar trámites como red.

---

### Caso E · Hablemos de Hidalgo, plataforma de participación ciudadana

**Institución:** foros de consulta del Plan Estatal de Desarrollo
**Escala:** eventos híbridos con más de 400 asistentes presenciales y más de 150 participantes virtuales
**Servicios aplicados:** software y automatización · encuestas y opinión pública

**Qué se hizo.**

- CMS especializado en Django para organización de eventos interactivos, foros virtuales y blog.
- Integración con transmisión en vivo mediante Facebook Live API y herramientas de moderación y retroalimentación para captación directa de comentarios ciudadanos.
- Soporte masivo para eventos híbridos con análisis de reacciones.

**Uso en el sitio:** caso secundario de la ficha de software. Refuerza el argumento de participación ciudadana junto con el caso C.

---

### Caso F · Laboratorio Nacional de Indicadores Sociolaborales

**Institución:** Organización Internacional del Trabajo y Secretaría del Trabajo y Previsión Social
**Escala:** más de 200 scripts de R orquestados · múltiples dependencias federales
**Servicios aplicados:** software y automatización · tableros y visualización

**El problema.** Normalizar y sistematizar datos de políticas públicas de empleo provenientes de múltiples dependencias gubernamentales federales.

**Qué se hizo.**

- Orquestación de pipelines ETL con Apache NiFi.
- Ejecución sistematizada de más de 200 scripts de análisis desarrollados en R y provistos por distintas dependencias federales, que procesan la información sociolaboral cruda, la normalizan y la cargan en base centralizada en PostgreSQL.
- Portal interactivo en Laravel para la visualización del Sistema Nacional de Indicadores, con mapas interactivos, análisis temporal y gráficos dinámicos para uso ejecutivo.

**Por qué importa para el sitio.** Es el único caso con un organismo internacional. Para el perfil del enlace administrativo que verifica proveedores, este es el caso que más peso tiene.

---

### Caso G · Sistema de evaluación y scoring de vulnerabilidad para programas sociales

**Institución:** programas sociales estatales y municipales
**Servicios aplicados:** índices y priorización

**Qué se hizo.**

- Algoritmo basado en metodologías de orden social y estado del arte para generar un índice ponderado de vulnerabilidad.
- Evaluación multidimensional de perfiles para programas con enfoque social y de género: madres trabajadoras, grupos en situación vulnerable y emprendimientos comunitarios.
- Sistema de apoyo a la decisión que complementa de manera metodológica y auditable el criterio de los especialistas en campo.
- Herramientas estadísticas avanzadas y análisis de discurso cualitativo con procesamiento de lenguaje natural para optimizar el diseño de los instrumentos de recolección.

**Nota:** conceptualmente cercano al caso B. Conviene decidir si se presentan como dos casos o como uno solo con dos aplicaciones, para no diluir el argumento.

---

### Caso H · Modelo de priorización de infraestructura urbana

**Servicios aplicados:** cartografía y análisis territorial · índices y priorización

**El problema.** Crear un sistema objetivo de decisión para la intervención vial y de servicios urbanos, balanceando necesidades técnicas y rentabilidad social y territorial.

**Qué se hizo.**

- Modelo matemático ponderado que integra capas de fuentes secundarias oficiales del INEGI y CONEVAL: índices de marginación urbana, censos de población y vivienda y datos demográficos locales.
- Variables dinámicas sobre el estado físico de la red vial mediante rastreo de baches, y cercanía a servicios clave como transporte público y escuelas, integrando la Red Nacional de Caminos.
- Cálculo automatizado de un puntaje de prioridad de atención **por calle y por colonia**.

**Por qué es útil en el sitio.** Es el caso más fácil de explicar a un público no técnico y el que mejor demuestra la resolución fina frente a los competidores nacionales, que solo dan la fotografía municipal.

---

### Caso I · Plataforma de escucha digital y análisis de opinión pública

**Servicios aplicados:** escucha digital y análisis de actores

**Qué se hizo.**

- Crawlers y scraping ético de redes sociales, portales de noticias, prensa digital y reseñas públicas de dependencias gubernamentales.
- Procesamiento de lenguaje natural: detección automática de sentimientos y emociones, modelado de temas latentes con LDA para identificar narrativas emergentes, análisis de complejidad de lectura y legibilidad.
- Análisis vectorial: transformación de texto libre en vectores densos y cálculo de distancias de coseno para medir similitud y convergencia de discursos.
- Modelado predictivo y clasificación con redes neuronales, máquinas de soporte vectorial, árboles de decisión y análisis de regresión para mapear tendencias de percepción.
- Visualización en cuadros de mando interactivos en Looker Studio, Power BI y Django.

---

## 3. Banco de cifras para el sitio

Todas verificadas contra los documentos fuente. Antes de publicarlas hay que confirmar que siguen siendo correctas y que son divulgables.

| Cifra | Concepto | Caso | Dónde usarla |
|---|---|---|---|
| 84 | Municipios cubiertos en un levantamiento estatal | A | Inicio, ficha de encuestas |
| 80 | Encuestadores simultáneos en campo | A | Inicio, ficha de encuestas |
| 30 | Auditores de gabinete para control de calidad | A | Ficha de encuestas, nota de enero |
| 600 | Usuarios activos diarios en Roots ID | D | Inicio, ficha de software |
| 900 | Trámites administrativos digitalizados | D | Inicio, ficha de software |
| < 2 meses | Tiempo de construcción de Roots ID | D | Ficha de software |
| 200 | Scripts de R orquestados para el laboratorio nacional | F | Ficha de software, quiénes somos |
| 400 + 150 | Asistentes presenciales y virtuales en evento híbrido | E | Ficha de software |
| 1 733 / 183 / 16 | Inscripciones, grupos y sedes del marco muestral | C | Nota de octubre sobre muestra |
| ±3.2 pp | Error a nivel municipal del escenario recomendado | C | Nota de noviembre sobre margen de error |
| 0 a 100 | Escala continua del IMPAS | B | Ficha de índices |
| 6 | Dimensiones ponderadas del IMPAS | B | Ficha de índices |
| −5 a +5 | Margen de ajuste cualitativo colegiado | B | Ficha de índices, nota de diciembre |

---

## 4. Mapeo de casos a servicios

Cada ficha de servicio del sitio necesita al menos dos casos. Este es el reparto según el material disponible.

| Servicio | Casos disponibles | Suficiencia |
|---|---|---|
| Encuestas y opinión pública | A, C, E | Suficiente |
| Cartografía y análisis territorial | A, H | Suficiente |
| Escucha digital y análisis de actores | I | **Insuficiente:** falta un segundo caso o hay que desagregar el I |
| Índices y priorización | B, G, H | Suficiente y es el servicio mejor respaldado |
| Tableros y visualización | B, C, D, F | Suficiente |
| Software y automatización | A, D, E, F | Suficiente, es el diferencial competitivo |

**Conclusión operativa:** cinco de seis fichas tienen respaldo sobrado. La de escucha digital es la única que se sostiene sobre un solo proyecto descrito de forma genérica. Hay que decidir si se desagrega en aplicaciones concretas, se documenta un caso nuevo, o se publica en la versión 1 con menos peso.

---

## 5. Inventario técnico

Para la página de quiénes somos y para las secciones de método de cada ficha.

**Ciencia de datos y lenguaje natural:** procesamiento de lenguaje natural, análisis de sentimientos, modelado de tópicos con LDA, embeddings vectoriales con similitud de coseno, regresiones, máquinas de soporte vectorial, redes neuronales, árboles de decisión.

**Inteligencia geoespacial:** PostGIS, GPX, mapas de calor, análisis de buffers con redes viales nacionales, capas de INEGI y CONEVAL.

**Ingeniería de datos y ETL:** Apache NiFi, Python con Pandas, NumPy y Scikit-learn, scripting en R, PostgreSQL, SQLite, integración con Firebase.

**Desarrollo web y GovTech:** Python con Django, Tailwind CSS, Astro, React, React Native, PHP con Laravel y WordPress, Docker y Docker Compose.

**Visualización e inteligencia de negocio:** Looker Studio, Power BI, Tableau.

**Métodos estadísticos documentados en los proyectos:** muestreo estratificado con afijación mixta, corrección por población finita, análisis de componentes principales, alfa de Cronbach y omega de McDonald, correlaciones policóricas, modelos de respuesta ordinal, aprendizaje supervisado, matrices de correlación.

---

## 6. Marco normativo y ética de datos

Material para la página de protección de datos, que el documento 02 identificó como argumento competitivo y no como trámite.

**Legislación citada en los documentos fuente:**

- **Ley General de Protección de Datos Personales en Posesión de Sujetos Obligados**, publicada el 20 de marzo de 2025. Obliga a tratamiento adecuado, relevante y estrictamente necesario; aviso de privacidad; y derechos de acceso, rectificación, cancelación y oposición. La respuesta operativa documentada es consentimiento previo a la captura de datos sensibles, control de roles, minimización y reportes anonimizados.
- **Ley General de Transparencia y Acceso a la Información Pública**, publicada el 20 de marzo de 2025. La respuesta operativa es memoria pública con resultados agregados y sin datos identificables.
- **Normas oficiales mexicanas** NOM-014-SSA3-2013, NOM-043-SSA2-2012 y NOM-251-SSA1-2009 en materia de asistencia social.

**Prácticas de campo documentadas que pueden publicarse:** protocolo de consentimiento informado dentro de la capacitación obligatoria, identificador operativo no nominativo, criterios de no inducción de respuesta, verbalizaciones textuales anonimizadas para el informe narrativo, y reportes agregados sin datos identificables.

---

## 7. Material listo para convertirse en contenido

Cruce entre lo que ya está escrito en los documentos fuente y las doce notas del calendario editorial del documento 03. La columna de esfuerzo indica cuánto trabajo real queda.

| Nota del calendario | Material fuente disponible | Esfuerzo |
|---|---|---|
| Tamaño de muestra explicado sin fórmulas | Sección de fundamento estadístico del caso C, con los dos escenarios y la corrección por no respuesta | Edición |
| Qué se puede saber sin levantar una encuesta | Capas INEGI, CONEVAL, CONAPO y Red Nacional de Caminos de los casos A y H | Edición |
| Margen de error, confianza y efecto de diseño | Ficha técnica y potencia estadística del caso C | Edición |
| Reelección de alcaldes en 2027 | **Sin material fuente.** Requiere investigación nueva | Redacción completa |
| A quién apoyar primero cuando el presupuesto no alcanza | Caso B completo: dimensiones, ponderaciones, niveles de prioridad | Edición |
| Marginación, rezago social y pobreza no son lo mismo | Marco conceptual del caso B y datos CONEVAL del caso C | Edición |
| Ochenta encuestadores en campo | Caso A más los controles de calidad del caso C | Edición y ampliación |
| Presupuesto participativo: qué dice la evidencia | Estado del arte del caso C, con experiencia internacional y nacional revisada | Edición |
| Cartografía electoral: la sección importa, el municipio no | Casos A y H, con adaptación al contexto electoral | Redacción parcial |
| Qué encuestas necesita una campaña municipal | **Sin material fuente.** Requiere redacción nueva | Redacción completa |
| Cómo leer una encuesta de prensa sin dejarse engañar | Ficha técnica del caso C como base de los criterios | Edición y ampliación |
| Del dato al tablero: qué ve un alcalde cada lunes | Casos B, D y F, con sus sistemas de indicadores | Edición |

**Dato relevante para la planeación:** diez de las doce notas tienen material fuente y solo requieren trabajo de edición. Las dos que exigen redacción desde cero son las del pilar de ventana electoral. Eso reduce la carga estimada del documento 03 de forma considerable en los primeros meses.

---

## 8. Voz de la marca

Frases tomadas literalmente de los documentos fuente. Sirven de referencia de registro al redactar el sitio y algunas pueden citarse como muestra de escritura propia.

> «Los números aleatorios empleados en la selección sistemática de grupos y en la selección de personas dentro de grupo se generan con semilla documentada y se archivan antes del levantamiento. Este requisito convierte la aleatoriedad en un hecho auditable y no en una declaración.»

> «El valor del diagnóstico participativo no radica en obtener más presupuesto, sino en asignar mejor el presupuesto disponible.»

> «El Índice no sustituye la valoración social profesional: la ordena, la hace comparable entre casos y le proporciona un registro trazable.»

> «Esa redundancia no es un defecto de diseño, es su principal fuente de validez. Cuando las tres poblaciones convergen en el diagnóstico de una sede, la evidencia es robusta y la asignación es defendible; cuando divergen, la divergencia misma es un hallazgo que orienta la verificación en campo.»

> «El riesgo del ejercicio participativo no es la falta de entusiasmo inicial, sino la desinstitucionalización: procesos que producen consultas sin producir asignaciones, o que producen asignaciones sin producir trazabilidad verificable.»

> «La revisión documental no se presenta como ejercicio ilustrativo. Cada referente desemboca en dimensiones y reactivos concretos del instrumento en operación.»

**Rasgos del registro, para replicarlo:** frases declarativas, sin adjetivos de venta; la limitación se enuncia en la misma oración que la capacidad; se nombra la técnica concreta en lugar de la categoría; y toda afirmación metodológica va acompañada del criterio que la vuelve verificable.

---

## 9. Pendientes antes de redactar el sitio

Ordenados por cuánto bloquean.

**Bloquean la producción de páginas completas:**

1. **Confidencialidad caso por caso.** De los nueve casos, hay que decidir cuáles llevan nombre de la institución, cuáles van anonimizados por tipo de institución y cuáles no se publican. Los casos B, C, E y F tienen institución identificada en los documentos fuente; el A y el D no.
2. **Autorización para publicar cifras de cliente.** Las cifras del banco de la sección 3 provienen de proyectos con instituciones. Publicarlas requiere confirmar que son divulgables.
3. **Segundo caso de escucha digital**, o decisión de desagregar el caso I en aplicaciones concretas.

**Bloquean páginas específicas:**

4. **Equipo.** Los documentos fuente hablan en primera persona del plural pero no identifican integrantes. Falta saber cuántas personas y con qué perfiles para decidir si quiénes somos lleva fichas individuales.
5. **Datos de la firma:** razón social, domicilio fiscal, correo del dominio propio y número de WhatsApp.
6. **Material visual:** si existen capturas de tablero, mapas o fotografía de campo publicables, o si la versión 1 se resuelve con visualizaciones producidas para el sitio.

**Verificación antes de publicar:**

7. **Vigencia de las cifras.** Varias provienen de proyectos con fecha. Hay que confirmar cuáles siguen siendo el dato más reciente.
8. **Estado de los proyectos.** Si alguno terminó, se amplió o cambió de alcance desde que se escribieron los documentos fuente.

---

## 10. Cómo se conecta con el resto de la serie

| Documento | Qué toma de aquí |
|---|---|
| 00 Benchmark | Las capacidades de la sección 5 sostienen el argumento de que nadie vende el sistema |
| 01 Manual de identidad | Las frases de la sección 8 son la base del tono de voz |
| 02 Arquitectura | Los casos de la sección 2 llenan las fichas de caso; el banco de cifras llena el inicio |
| 03 Plan de contenidos | La sección 7 dice qué notas están casi escritas y cuáles no |
| 04 Posicionamiento | El inventario técnico alimenta el campo de materias conocidas de los datos estructurados |
