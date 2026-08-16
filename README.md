# Brad M Blanco — Portfolio

**IT Analyst · Full-Stack Developer · Systems Builder**
Santiago, Chile · mbitupx@gmail.com · [GitHub](https://github.com/bitupx00) · [X @I_Am_Bitupx](https://x.com/I_Am_Bitupx)

> 🌐 **Sitio web:** [bitupx00.github.io/portfolio](https://bitupx00.github.io/portfolio)
>
> 🇪🇸 Español abajo · 🇬🇧 English below

---

## 🇪🇸 Sobre mí

Desarrollador full-stack y analista IT. Construyo sistemas empresariales reales — plataformas de gestión contable, automatización de portales externos, juegos online y herramientas con IA. Me muevo con soltura entre **Rust, TypeScript/React, Python y Electron**, del backend a la infraestructura.

**Lo que me define:** no hago demos — hago productos que operan en producción con empresas reales, con tests, CI y documentación.

### Stack principal

| Área | Tecnologías |
|---|---|
| Sistemas | Rust (tokio, sqlx, axum, Tauri), Python |
| Web | TypeScript 5.9, React 19, Next.js 14–16, Tailwind, Zustand |
| Desktop | Electron 28, Tauri 2 |
| Datos | PostgreSQL 17 (+pgvector), MariaDB, SQLite, Neon, Drizzle |
| Infra | Docker, PM2, Vercel, GitHub Actions, Linux, Sentry |
| IA | RAG, extracción documental, MCP, integraciones LLM |
| Automatización | Extensiones Chrome, Playwright, WebSocket, anti-detección |
| Juegos | WebRTC P2P, protocolos binarios (Tibia 8.60), TFS 1.5 |

---

## 🇪🇸 Proyectos destacados

### 🏢 HuaboDesk — Plataforma empresarial contable (en producción)

Suite integral de gestión empresarial para el mercado chileno. **14+ módulos, 429+ rutas API, 186+ tablas PostgreSQL** operando con empresas reales.

**Arquitectura de la plataforma:**

- **Web:** Next.js 16 (App Router) + React 19 + TypeScript 5.9 — 429+ rutas API, SSR
- **Base de datos:** PostgreSQL 17 — 186+ tablas, 27 funciones SQL, **pgvector** para búsqueda semántica
- **Multi-proceso (PM2):** servidor web + servidor WebSocket independiente + servicio de indexación RAG + workers de fondo (vigilancia documental, retención de correo, conciliación RAG, auto-deploy)
- **Cliente de escritorio (Electron 28):** 70+ canales IPC con whitelist estricta, automatización web integrada (Playwright), bandeja de sistema, splash screen, auto-actualización con instalador NSIS, sincronización de archivos con motor Rust, **sistema multi-ventana** (cada módulo abre como ventana OS independiente: generador de contratos, generador de documentos, empleados, informes, libros contables)
- **Seguridad:** JWT + refresh tokens, bcrypt, RBAC multi-rol, TOTP 2FA, CSRF tokens, context isolation + sandbox, monitoreo Sentry

**Sistemas y módulos construidos:**

| Dominio | Sistemas |
|---|---|
| CRM / Datos de clientes | Ficha completa de clientes (24+ componentes: búsqueda avanzada, selector de sucursales, cuentas bancarias, vista detallada, formularios SPA), contactos, contratos, empresas y **grupos empresariales** (consolidados multi-empresa) |
| Contabilidad | Libros contables de compras/ventas con edición inline, reglas por cuenta, ajustes contables, declaraciones mensuales, exportaciones CSV estándar, estado financiero con informes |
| Remuneraciones | Empleados v2 (gestión completa), liquidaciones de sueldo, finiquitos, alta de empleados con generador de contratos y documentos, horarios, control de asistencia, evaluaciones de desempeño |
| Finanzas | Panel de cobros PayBoard integrado con bus en tiempo real |
| Chat de equipo — HeChat | Chat completo: grupos con gestión de miembros, **@mentions**, stickers, picker de emojis, indicador de typing, búsqueda en conversaciones, reacciones, adjuntos con visor de imágenes, burbujas con citas, control de acceso por empresa |
| Correo corporativo | Webmail completo: composición, **búsqueda global**, cola de reintentos con panel de fallos, operaciones admin, avatares, retención automática de correos |
| Workflows | Motor de flujos de trabajo: **timeline unificado** tipo chat, estados con acciones, prioridades, comentarios con reacciones, adjuntos, asignación multiusuario, menú contextual, recordatorios |
| Operación | Gantt de proyectos, calendario con eventos + feriados locales, coordinación de equipo (dock + burbujas), atención de clientes con reasignación de cartera e informes, broadcast global de mensajes |
| Documentos | Gestión documental con watcher en tiempo real, integración Dropbox, **búsqueda IA con RAG + pgvector**, extracción documental con IA, visor de imágenes |
| Automatización documental | Pipeline OCR triple motor (**Tesseract** + EasyOCR + Vision API con fallback), renderizado PDF, extracción de identificadores, normalización; **worker IA de autollenado** de fichas de empleados (lee documentos → OCR → extracción IA → rellena la ficha, cola de jobs con reintentos y panel de estado); **generador de contratos y documentos DOCX** (docxtpl/Jinja2 + post-proceso XML) desde datos de empleado/empresa |
| Sincronización Dropbox | Scanners por empresa y de RRHH con indexación automática — submenú de documentos de empleados con exportación, vencimientos y actividad reciente |
| Administración | Gestión de equipos y roles, logs de auditoría, registro con aprobación manual, configuración global, health checks, geocoding/geolocalización, integración de stock photos |

**Ingeniería avanzada:** grafo de conocimiento del codebase (**14.009 nodos, 46.142 aristas, 512 comunidades**) para análisis arquitectónico y detección de deuda técnica. Suite de 143 archivos de tests (Vitest + Playwright).

### 🐙 Optopus — Puente de automatización de navegadores

Sistema de **automatización web adaptativo** que realiza operaciones en portales y sistemas externos usando el **navegador real del usuario** mediante una extensión de Chrome — sin Playwright, sin navegadores headless.

**Qué lo hace distinto:**

- **Navegador y perfil reales:** opera con la sesión logueada del usuario y su fingerprint genuino — evita CAPTCHAs y detección de bots que bloquean herramientas tradicionales
- **Scraping adaptativo** (inspirado en Scrapling): localiza elementos aunque la estructura del sitio cambie — selectores resilientes con recuperación automática
- **Servidor WebSocket/HTTP:** API de control remoto para disparar operaciones desde la plataforma
- **MCP server integrado:** controlable por asistentes de IA (Claude, Cursor, Windsurf) — los agentes pueden ejecutar operaciones de navegador como herramientas
- **Zero-install:** solo la extensión de Chrome, sin descargar navegadores adicionales (~300–500 MB ahorrados vs Playwright)

`TypeScript` `Chrome Extension MV3` `WebSocket` `MCP` `Node.js`

### 💰 PayBoard — Motor financiero nativo

Panel de administración financiera de escritorio para gestionar los cobros mensuales de carteras de ~1.000 clientes de contabilidad. Construido como **aplicación 100% nativa en Rust + Tauri 2**.

**Por qué nativo:** reemplaza la arquitectura Node (servidor Next.js + ventana Electron con Chromium embebido) por un **binario único** con webview del sistema — de cientos de MB a un binario de unidades de MB, RAM objetivo ~80–150 MB, arranque sub-segundo.

**Motor de dominio (`pb-core`, Rust puro sin dependencias):**

- Propagación de saldos mes a mes: la deuda del mes N pasa al N+1, el sobrepago se convierte en abono — saldos jamás editables a mano
- Anticipos con signo (negativos = a favor del cliente), pagos con valor absoluto
- Parseo monetario estricto (formato `1.500.000`, rechazo de basura — nunca dígitos parciales)
- **Golden tests de paridad** que congelan cada regla de negocio crítica como contrato ejecutable

**Funcionalidad completa:**

- Tabla mensual estilo hoja de cálculo con **21 columnas**: deuda_anterior, abono, impuesto, contabilidad (base + recargo por empleados), previsión ×4 (prev_1–prev_4), visa, certificados, legalización, multa, trámites, patente, renta, servicios extra, anticipos, pagos — coloreado en 3 niveles, menú contextual, navegación tipo Excel
- **Comprobantes PDF** individuales y en lote con **fuente CJK embebida** (Noto Sans SC subset) para conceptos bilingües español/chino
- **Modo colaborativo multi-operador:** cola de aprobaciones, indicador de presencia, changelog, notificaciones
- **Verificación tributaria cruzada:** cruce automático del impuesto declarado contra lo efectivamente cobrado
- Import/export Excel, atajos de teclado configurables, sistema de roles granular
- Sistema de diseño propio inspirado en software contable chileno de referencia

`Rust` `Tauri 2` `PostgreSQL` `PDF/CJK` `Golden tests`

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

Full-stack developer and IT analyst. I build real enterprise systems — accounting management platforms, external-portal automation, online games and AI tooling. Fluent across **Rust, TypeScript/React, Python and Electron**, from backend to infrastructure.

**What defines me:** I don't build demos — I build products that run in production for real businesses, with tests, CI and documentation.

---

## 🇬🇧 Featured projects

### 🏢 HuaboDesk — Enterprise accounting platform (in production)

All-in-one business management suite for the Chilean market. **14+ modules, 429+ API routes, 186+ PostgreSQL tables** serving real businesses.

**Platform architecture:**

- **Web:** Next.js 16 (App Router) + React 19 + TypeScript 5.9 — 429+ API routes, SSR
- **Database:** PostgreSQL 17 — 186+ tables, 27 SQL functions, **pgvector** for semantic search
- **Multi-process (PM2):** web server + standalone WebSocket server + RAG indexing service + background workers (document watcher, mail retention, RAG conciliation, auto-deploy)
- **Desktop client (Electron 28):** 70+ IPC channels with strict whitelisting, integrated web automation (Playwright), system tray, splash screen, NSIS installer auto-updates, Rust-powered file sync engine, **multi-window system** (each module opens as an independent OS window: contract generator, document generator, employees, reports, accounting books)
- **Security:** JWT + refresh tokens, bcrypt, multi-role RBAC, TOTP 2FA, CSRF tokens, context isolation + sandbox, Sentry monitoring

**Systems and modules built:**

| Domain | Systems |
|---|---|
| CRM / Client data | Full client profiles (24+ components: advanced search, branch selector, bank accounts, detail views, SPA forms), contacts, contracts, companies & **company groups** (multi-entity consolidation) |
| Accounting | Purchase/sales books with inline editing, per-account rules, accounting adjustments, monthly filings, standard CSV exports, financial statements with reports |
| Payroll | Employees v2 (full management), payslips, termination settlements, employee onboarding with contract & document generators, schedules, attendance control, performance reviews |
| Finance | PayBoard collections panel integrated with a real-time bus |
| Team chat — HeChat | Full chat: groups with member management, **@mentions**, stickers, emoji picker, typing indicator, conversation search, reactions, attachments with image viewer, quoted bubbles, per-company access control |
| Corporate email | Full webmail: compose, **global search**, retry queue with failure panel, admin ops, avatars, automatic mail retention |
| Workflows | Workflow engine: **unified chat-style timeline**, status actions, priorities, comments with reactions, attachments, multi-user assignment, context menu, reminders |
| Operations | Project Gantt, calendar with events + local holidays, team coordination (dock + bubbles), client care with portfolio reassignment & reports, global message broadcast |
| Documents | Document management with real-time watcher, Dropbox integration, **AI search with RAG + pgvector**, AI document extraction, image viewer |
| Document automation | Triple-engine OCR pipeline (**Tesseract** + EasyOCR + Vision API with fallback), PDF rendering, identifier extraction, normalization; **AI auto-fill worker** for employee profiles (reads documents → OCR → AI extraction → fills the profile, job queue with retries and status panel); **DOCX contract & document generator** (docxtpl/Jinja2 + XML post-processing) from employee/company data |
| Dropbox sync | Per-company and HR scanners with automatic indexing — employee documents submenu with export, expiration control and recent activity |
| Administration | Team & role management, audit logs, approval-based registration, global settings, health checks, geocoding/geolocation, stock photo integration |

**Advanced engineering:** codebase knowledge graph (**14,009 nodes, 46,142 edges, 512 detected communities**) for architectural analysis and tech-debt detection. 143 test files (Vitest + Playwright).

### 🐙 Optopus — Browser automation bridge

Adaptive **web automation system** that performs operations on external portals and systems using the **user's real browser** via a Chrome extension — no Playwright, no headless browsers.

**What makes it different:**

- **Real browser & profile:** operates with the user's logged session and genuine fingerprint — bypasses the CAPTCHAs and bot detection that block traditional tooling
- **Adaptive scraping** (Scrapling-inspired): locates elements even when the site structure changes — resilient selectors with automatic recovery
- **WebSocket/HTTP server:** remote-control API to trigger operations from the platform
- **Integrated MCP server:** controllable by AI assistants (Claude, Cursor, Windsurf) — agents execute browser operations as tools
- **Zero-install:** just the Chrome extension, no extra browser downloads (~300–500 MB saved vs Playwright)

`TypeScript` `Chrome Extension MV3` `WebSocket` `MCP` `Node.js`

### 💰 PayBoard — Native financial engine

Desktop financial administration panel managing monthly collections for ~1,000-client accounting portfolios. Built as a **100% native Rust + Tauri 2 application**.

**Why native:** replaces the Node architecture (Next.js server + Electron window with embedded Chromium) with a **single binary** using the system webview — from hundreds of MB to a single-digit MB binary, ~80–150 MB target RAM, sub-second startup.

**Domain engine (`pb-core`, pure Rust, zero dependencies):**

- Month-over-month balance propagation: month N's debt carries into N+1, overpayment becomes credit — balances are never hand-editable
- Signed prepayments (negative = in the client's favor), absolute-value payments
- Strict money parsing (`1.500.000` format, garbage rejection — never partial digits)
- **Parity golden tests** freezing every critical business rule as an executable contract

**Full feature set:**

- Spreadsheet-style monthly table with **21 columns**: prior_debt, credit, tax, accounting (base + per-employee surcharge), payroll ×4 (prev_1–prev_4), visa, certificates, legalization, fines, procedures, license, rent, extra services, prepayments, payments — 3-level color coding, context menu, Excel-like navigation
- **PDF receipts** individual and batch with **embedded CJK font** (Noto Sans SC subset) for Spanish/Chinese bilingual concepts
- **Multi-operator collaborative mode:** approval queue, presence indicators, changelog, notifications
- **Cross-check tax verification:** automatic reconciliation of declared tax vs. actually billed
- Excel import/export, configurable keyboard shortcuts, granular role system
- Custom design system inspired by reference Chilean accounting software

`Rust` `Tauri 2` `PostgreSQL` `PDF/CJK` `Golden tests`

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
