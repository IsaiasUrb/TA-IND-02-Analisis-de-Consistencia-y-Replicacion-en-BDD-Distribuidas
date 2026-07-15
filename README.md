# Aplicaciones Distribuidas (ISR-701) — Trabajos Autónomos

Repositorio con los trabajos autónomos individuales de la asignatura **Aplicaciones Distribuidas (ISR-701)**, Unidad 3 — Bases de Datos Distribuidas.

**Estudiante:** Isaías Abraham Urbina Romero
**Universidad Técnica Estatal de Quevedo** — Facultad de Ciencias de la Computación — Carrera de Ingeniería de Software

Este repositorio contiene dos entregables independientes:

| Tarea | Descripción | Carpeta |
|---|---|---|
| TA-IND-02 | Informe técnico: análisis crítico de consistencia y replicación en BDD, aplicado al PFC SCLI | [`/ta-ind-02`](#ta-ind-02--análisis-de-consistencia-y-replicación-en-bdd-distribuidas) |
| Banco Austro | Aplicación distribuida con enrutamiento por nodos (Cuenca / Quito) | [`/banco-austro`](#banco-austro--base-de-datos-distribuida) |

---

## TA-IND-02 — Análisis de Consistencia y Replicación en BDD Distribuidas

### Descripción

Informe técnico individual, elaborado en LaTeX, que analiza el modelo de consistencia y la estrategia de replicación implementados en **SCLI (Sistema de Control de Laboratorios Informáticos)**, el Proyecto Fin de Curso del equipo **FUVV**.

El informe caracteriza el modelo realmente implementado en el código del PFC (patrón *base de datos por servicio* sobre CockroachDB, control de concurrencia optimista, transacciones locales atómicas, llamadas REST síncronas entre microservicios), lo contrasta con dos alternativas (sagas asíncronas y despliegue multinodo real de CockroachDB) y responde, apoyado en los marcos CAP y PACELC, si dicho modelo es el óptimo para el dominio del sistema.

### Estructura del documento

1. Portada
2. Resumen
3. Introducción
4. Marco teórico (espectro de consistencia, CAP/PACELC, estrategias de replicación)
5. Análisis del modelo de consistencia del PFC (arquitectura, topología, consistencia intra e inter-servicio)
6. Evaluación de alternativas y trade-offs (tabla comparativa)
7. Discusión crítica: ¿es el modelo óptimo?
8. Conclusiones
9. Declaración de uso de IA generativa
10. Referencias (formato IEEE)

### Contenido de la carpeta

```
ta-ind-02/
├── TA-IND-02_Urbina_FUVV.tex     # Fuente LaTeX del informe
├── TA-IND-02_Urbina_FUVV.pdf     # Informe compilado
└── README.md                      # (este archivo, si se documenta por separado)
```

### Cómo compilar

El documento compila sin errores con `pdflatex` (requiere los paquetes `booktabs`, `tikz`, `hyperref`, `geometry`, `fancyhdr`):

```bash
pdflatex TA-IND-02_Urbina_FUVV.tex
pdflatex TA-IND-02_Urbina_FUVV.tex   # segunda pasada para referencias cruzadas y tabla de contenidos
```

### Referencias principales

- D. J. Abadi, "Consistency Tradeoffs in Modern Distributed Database System Design," *Computer*, 2012. doi: 10.1109/MC.2012.33
- J. C. Corbett et al., "Spanner: Google's Globally Distributed Database," *ACM TOCS*, 2013. doi: 10.1145/2491245
- G. DeCandia et al., "Dynamo: Amazon's Highly Available Key-value Store," SOSP '07, 2007. doi: 10.1145/1294261.1294281
- S. Gilbert y N. Lynch, "Brewer's Conjecture and the Feasibility of Consistent, Available, Partition-Tolerant Web Services," *ACM SIGACT News*, 2002. doi: 10.1145/564585.564601
- M. van Steen y A. S. Tanenbaum, *Distributed Systems*, 3.ª ed., 2017.
- P. Viotti y M. Vukolić, "Consistency in Non-Transactional Distributed Storage Systems," *ACM Computing Surveys*, 2016. doi: 10.1145/2926965

---

## Banco Austro — Base de Datos Distribuida

### Descripción

Este proyecto implementa una aplicación distribuida para el Banco del Austro utilizando **Spring Boot**, **PostgreSQL** y **Docker**.

La aplicación simula una base de datos distribuida mediante dos nodos independientes:

- **Cuenca**
- **Quito**

El sistema enruta automáticamente las consultas hacia la base de datos correspondiente utilizando el prefijo del número de cuenta:

- **22** → Cuenca
- **17** → Quito

Además, permite realizar consultas distribuidas que combinan la información almacenada en ambos nodos.

### Tecnologías utilizadas

- Java 21
- Spring Boot 3.5.4
- Maven
- PostgreSQL 16
- Docker Compose
- IntelliJ IDEA

### Estructura del proyecto

```
banco-austro/
│
├── src/
├── sql-cuenca/
├── sql-quito/
├── docker-compose.yml
├── pom.xml
└── README.md
```

### Cómo ejecutar el proyecto

**1. Iniciar los contenedores**

```bash
docker compose up -d
```

**2. Ejecutar la aplicación**

Abrir el proyecto en IntelliJ IDEA y ejecutar:

```
BancoAustroApplication
```

### Endpoints disponibles

**Consultar saldo**

```
GET /api/banco/saldo/{numero}
```

Ejemplos:

```
GET /api/banco/saldo/2201000001
GET /api/banco/saldo/1701000001
```

**Listar clientes**

```
GET /api/banco/clientes
```

### Bases de datos

| Nodo | Puerto |
|------|--------|
| Cuenca | 5442 |
| Quito | 5433 |

---

## Autor

**Isaías Urbina**
Universidad Técnica Estatal de Quevedo
Aplicaciones Distribuidas (ISR-701)
