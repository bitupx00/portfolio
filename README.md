# Brad M Blanco — Portfolio

**IT Analyst · Full-Stack Developer · Systems Builder**
Santiago, Chile · mbitupx@gmail.com · [GitHub](https://github.com/bitupx00) · [X @I_Am_Bitupx](https://x.com/I_Am_Bitupx)

> 🌐 **Sitio web:** [bitupx00.github.io/portfolio](https://bitupx00.github.io/portfolio)
>
> 🇪🇸 Español abajo · 🇬🇧 English below

---

## 🇪🇸 Sobre mí

Desarrollador full-stack y analista IT. Construyo sistemas empresariales reales — plataformas de gestión contable, automatización de procesos gubernamentales (SII Chile), juegos online y herramientas con IA. Me muevo con soltura entre **Rust, TypeScript/React, Python y Electron**, del backend a la infraestructura.

**Lo que me define:** no hago demos — hago productos que operan en producción con empresas reales, con tests, CI y documentación.

### Stack principal

| Área | Tecnologías |
|---|---|
| Sistemas | Rust (tokio, sqlx, axum, Tauri), Python |
| Web | TypeScript 5.9, React 19, Next.js 14–16, Tailwind, Zustand |
| Desktop | Electron 28, Tauri 2 |
| Datos | PostgreSQL 17 (+pgvector), MariaDB, SQLite, Neon, Drizzle |
| Infra | Docker, PM2, Vercel, GitHub Actions, Linux, Sentry |
| IA | RAG, extracción documental, integraciones LLM |
| Juegos | WebRTC P2P, protocolos binarios (Tibia 8.60), TFS 1.5 |

---

## 🇪🇸 Proyectos destacados

### 🔒 HuaboDesk — Plataforma empresarial contable (Confidencial)

Suite integral de gestión empresarial para el mercado chileno: contabilidad, remuneraciones, cumplimiento tributario SII, gestión documental, correo y colaboración en equipo. **14+ módulos en producción operando con empresas reales.**

**Arquitectura de la plataforma:**

- **Web:** Next.js 16 (App Router) + React 19 + TypeScript 5.9 — **429+ rutas API**, SSR
- **Base de datos:** PostgreSQL 17 — **186+ tablas**, 27 funciones SQL, **pgvector** para búsqueda semántica
- **Multi-proceso (PM2):** servidor web + servidor WebSocket independiente + servicio de indexación RAG + workers de fondo (vigilancia documental, retención de correo, conciliación RAG, auto-deploy)
- **Cliente de escritorio (Electron 28):** **70+ canales IPC** con whitelist estricta, **scraping del portal SII vía Playwright**, bandeja de sistema, splash screen, **auto-actualización con instalador NSIS**, sincronización de archivos con motor Rust
- **Seguridad:** JWT + refresh tokens, bcrypt, control de acceso por roles (RBAC), TOTP 2FA, context isolation + sandbox, monitoreo Sentry

**Módulos desarrollados:**

| Dominio | Módulos |
|---|---|
| Contabilidad / SII | Libros de compras y ventas, declaraciones mensuales, ajustes contables (código 48), exportación CSV SII, certificación SII, verificación F29 |
| Remuneraciones | Liquidaciones de sueldo, finiquitos, proceso Previred |
| Finanzas | Estado financiero, panel de cobros PayBoard (integrado) |
| Comunicación | Mail corporativo completo (compose, búsqueda global, cola de reintentos, administración), chat de equipo con adjuntos (HeChat) |
| Documentos | Gestión documental con watcher en tiempo real, **búsqueda IA con RAG + pgvector**, extracción de datos con IA |
| Operación | Motor de workflows con recordatorios y aprobaciones, Gantt de proyectos, asistencia, atención de clientes con reasignación de cartera, coordinación de equipo, informes exportables a Excel |
| Administración | Gestión de equipos y roles, logs de auditoría, settings, registro con aprobación |

**Ingeniería avanzada:** grafo de conocimiento del codebase (**14.009 nodos, 46.142 aristas, 512 comunidades** detectadas) para análisis arquitectónico y detección de deuda técnica. Suite de tests Vitest + Playwright.

> Proyecto confidencial: clientes, datos y arquitectura interna detallada no públicos. Alcance conversable bajo NDA.

### 🔒 PayBoard — Motor financiero nativo (Confidencial)

Panel de administración financiera de escritorio para gestionar los cobros mensuales de carteras de ~1.000 clientes de contabilidad. Reconstruido como **aplicación 100% nativa en Rust + Tauri 2**.

**Por qué nativo:** reemplaza la arquitectura Node (servidor Next.js + ventana Electron con Chromium embebido) por un **binario único** con webview del sistema — de cientos de MB a un binario de unidades de MB, RAM objetivo ~80–150 MB, arranque sub-segundo.

**Motor de dominio (`pb-core`, Rust puro sin dependencias):**

- Propagación de saldos mes a mes: la deuda del mes N pasa al N+1, el sobrepago se convierte en abono — saldos jamás editables a mano
- Anticipos con signo (negativos = a favor del cliente), pagos con valor absoluto
- Parseo monetario CLP estricto (formato `1.500.000`, rechazo de basura — nunca dígitos parciales)
- **Golden tests de paridad** que congelan cada regla de negocio crítica como contrato ejecutable

**Funcionalidad completa:**

- Tabla mensual estilo hoja de cálculo de **21 columnas** (impuestos, contabilidad, previred, visas, certificados, multas, trámites, patentes, rentas…), coloreado en 3 niveles, menú contextual, navegación tipo Excel
- **Comprobantes PDF** individuales y en lote con **fuente CJK embebida** (Noto Sans SC subset) para conceptos bilingües español/chino
- **Modo colaborativo multi-operador:** cola de aprobaciones, indicador de presencia, changelog, notificaciones
- **Verificación F29:** cruce automático del impuesto declarado en el SII contra lo efectivamente cobrado
- Import/export Excel, atajos de teclado configurables, sistema de roles granular
- Sistema de diseño propio inspirado en software contable chileno de referencia

> Proyecto confidencial: código y datos no públicos.

### 🥷 [ShinobiGO](https://github.com/bitupx00/ShinobiGO) — MMORPG online

MMORPG de shinobi ambientado en **Kesshō**, un mundo original. Arquitectura propia: cliente TypeScript (navegador/escritorio), **gateway de borde en Rust (tokio)**, servidor en tiempo real protocolo Tibia 8.60 y MariaDB. Sistema de progresión dual: nivel por combate + rango por Pruebas de Umbral no combativas (8 peldaños: aguantar quieto, detectar firmas falsas, memorizar a oscuras, sostener cercos).

`TypeScript` `Rust` `WebSocket` `MariaDB` `Tauri`

### 🇻🇪 [ReportaVNZLA](https://github.com/bitupx00/reportavnzla) — Plataforma humanitaria

Registro y búsqueda de personas tras el terremoto de Venezuela 2026. Sin fines de lucro, código abierto, **en producción**: [reportavnzla.com](https://reportavnzla.com). Mapa interactivo, búsqueda por nombre/cédula, flujo de reporte optimizado para emergencias.

`Next.js 14` `TypeScript` `Leaflet` `Neon PostgreSQL` `Vercel`

### ⚒️ [OTBForge](https://github.com/bitupx00/otbforge) — Generador de mapas con IA

Describe un mapa en texto → obtén un `.otbm` listo para producción. Generador de terreno con ruido Perlin multi-octava (11 biomas, ríos, islas), mazmorras BSP multi-piso (5 tipos de sala, cofres, pasillos), pueblos con 3 estilos arquitectónicos y NPCs. Funciona con o sin LLM. **Python puro sin dependencias + port Rust**, 492 tests.

`Python` `Rust` `Perlin noise` `BSP` `LLM`

### 🎲 [Ludo Party](https://github.com/bitupx00/ludo-party) — Juego de mesa online

Parchís estilo Ludo Club: **online WebRTC P2P sin servidor de juego** (bot toma el asiento si alguien se desconecta), bots con personalidad, modo pasar-y-jugar, equipos 2v2, stickers, reacciones, sonidos sintetizados, video-chat opcional (PeerJS). Bilingüe ES/EN, PWA mobile-first. **Demo:** [ludo-party.vercel.app](https://ludo-party.vercel.app)

`React` `TypeScript` `WebRTC` `PWA`

### 📊 [HuaboDesk Proyectos](https://github.com/bitupx00/huabodesk-gantproyetos) — Gantt de proyectos

Timeline/Gantt para gestión de plazos y avance de equipo: fases en días hábiles con feriados legales chilenos, progreso automático desde checklists (promedio ponderado), vista pública de solo lectura + modo admin, edición desde el Gantt. SQL parametrizado a mano sobre SQLite.

`Next.js 16` `React 19` `SQLite` `Radix UI` `Vitest`

---

## 🇬🇧 About me

Full-stack developer and IT analyst. I build real enterprise systems — accounting management platforms, government portal automation (Chile's IRS/SII), online games and AI tooling. Fluent across **Rust, TypeScript/React, Python and Electron**, from backend to infrastructure.

**What defines me:** I don't build demos — I build products that run in production for real businesses, with tests, CI and documentation.

---

## 🇬🇧 Featured projects

### 🔒 HuaboDesk — Enterprise accounting platform (Confidential)

All-in-one business management suite for the Chilean market: accounting, payroll, SII tax compliance, document management, email and team collaboration. **14+ modules in production serving real businesses.**

**Platform architecture:**

- **Web:** Next.js 16 (App Router) + React 19 + TypeScript 5.9 — **429+ API routes**, SSR
- **Database:** PostgreSQL 17 — **186+ tables**, 27 SQL functions, **pgvector** for semantic search
- **Multi-process (PM2):** web server + standalone WebSocket server + RAG indexing service + background workers (document watcher, mail retention, RAG conciliation, auto-deploy)
- **Desktop client (Electron 28):** **70+ IPC channels** with strict whitelisting, **SII portal scraping via Playwright**, system tray, splash screen, **NSIS installer auto-updates**, Rust-powered file sync engine
- **Security:** JWT + refresh tokens, bcrypt, role-based access control, TOTP 2FA, context isolation + sandbox, Sentry monitoring

**Modules built:**

| Domain | Modules |
|---|---|
| Accounting / SII | Purchase & sales books, monthly tax filings, accounting adjustments (code 48), SII CSV export, SII certification, F29 verification |
| Payroll | Payslips, termination settlements, Previred process |
| Finance | Financial statements, PayBoard collections panel (integrated) |
| Communication | Full corporate webmail (compose, global search, retry queue, admin ops), team chat with attachments (HeChat) |
| Documents | Document management with real-time watcher, **AI search with RAG + pgvector**, AI data extraction |
| Operations | Workflow engine with reminders and approvals, project Gantt, attendance, client care with portfolio reassignment, team coordination, Excel-exportable reports |
| Administration | Team & role management, audit logs, settings, approval-based registration |

**Advanced engineering:** codebase knowledge graph (**14,009 nodes, 46,142 edges, 512 detected communities**) for architectural analysis and tech-debt detection. Vitest + Playwright test suite.

> Confidential project: clients, data and detailed internal architecture not public. Scope discussable under NDA.

### 🔒 PayBoard — Native financial engine (Confidential)

Desktop financial administration panel managing monthly collections for ~1,000-client accounting portfolios. Rebuilt as a **100% native Rust + Tauri 2 application**.

**Why native:** replaces the Node architecture (Next.js server + Electron window with embedded Chromium) with a **single binary** using the system webview — from hundreds of MB to a single-digit MB binary, ~80–150 MB target RAM, sub-second startup.

**Domain engine (`pb-core`, pure Rust, zero dependencies):**

- Month-over-month balance propagation: month N's debt carries into N+1, overpayment becomes credit — balances are never hand-editable
- Signed prepayments (negative = in the client's favor), absolute-value payments
- Strict CLP money parsing (`1.500.000` format, garbage rejection — never partial digits)
- **Parity golden tests** freezing every critical business rule as an executable contract

**Full feature set:**

- Spreadsheet-style monthly table with **21 columns** (taxes, accounting, payroll, visas, certificates, fines, procedures, licenses, rents…), 3-level color coding, context menu, Excel-like navigation
- **PDF receipts** individual and batch with **embedded CJK font** (Noto Sans SC subset) for Spanish/Chinese bilingual concepts
- **Multi-operator collaborative mode:** approval queue, presence indicators, changelog, notifications
- **F29 verification:** automatic cross-check of tax declared to the SII vs. actually billed
- Excel import/export, configurable keyboard shortcuts, granular role system
- Custom design system inspired by reference Chilean accounting software

> Confidential project: code and data not public.

### 🥷 [ShinobiGO](https://github.com/bitupx00/ShinobiGO) — Online MMORPG

Shinobi MMORPG set in **Kesshō**, an original world. Custom architecture: TypeScript client (browser/desktop), **Rust edge gateway (tokio)**, real-time Tibia 8.60 protocol server, MariaDB. Dual progression: combat levels + rank through non-combat Threshold Trials (8 rungs: hold still, spot false signatures, memorize in the dark, sustain enclosures).

`TypeScript` `Rust` `WebSocket` `MariaDB` `Tauri`

### 🇻🇪 [ReportaVNZLA](https://github.com/bitupx00/reportavnzla) — Humanitarian platform

Registry and search for missing persons after the 2026 Venezuela earthquake. Non-profit, open source, **live in production**: [reportavnzla.com](https://reportavnzla.com). Interactive map, search by name/ID, emergency-optimized reporting flow.

`Next.js 14` `TypeScript` `Leaflet` `Neon PostgreSQL` `Vercel`

### ⚒️ [OTBForge](https://github.com/bitupx00/otbforge) — AI map generator

Describe a map in text → get a production-ready `.otbm` file. Multi-octave Perlin terrain (11 biomes, rivers, islands), multi-floor BSP dungeons (5 room types, chests, corridors), towns with 3 architectural styles and NPCs. Works with or without an LLM. **Zero-dependency Python + Rust port**, 492 tests.

`Python` `Rust` `Perlin noise` `BSP` `LLM`

### 🎲 [Ludo Party](https://github.com/bitupx00/ludo-party) — Online board game

Ludo Club-style parchís: **online WebRTC P2P with no game server** (a bot takes the seat on disconnect), personality bots, pass-and-play, 2v2 teams, stickers, reactions, synthesized sounds, optional video chat (PeerJS). Bilingual EN/ES, mobile-first PWA. **Demo:** [ludo-party.vercel.app](https://ludo-party.vercel.app)

`React` `TypeScript` `WebRTC` `PWA`

### 📊 [HuaboDesk Projects](https://github.com/bitupx00/huabodesk-gantproyetos) — Project Gantt

Gantt timeline for deadline and team progress tracking: business-day phases with Chilean statutory holidays, automatic progress from checklists (weighted average), public read-only view + admin mode, edit-from-Gantt popups. Hand-written parameterized SQL over SQLite.

`Next.js 16` `React 19` `SQLite` `Radix UI` `Vitest`

---

## Contacto / Contact

📧 mbitupx@gmail.com · 💬 [Telegram](https://t.me/I_Am_Bitupx) · 🐙 [github.com/bitupx00](https://github.com/bitupx00)

*Disponible para proyectos freelance — desarrollo full-stack, sistemas en Rust, automatización e integraciones.*
*Available for freelance work — full-stack development, Rust systems, automation and integrations.*
