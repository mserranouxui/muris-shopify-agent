# Curso Claude · Eunoia Digital

Material del curso interno de Claude Code. Incluye el caso práctico, dos agentes propios y una biblioteca de 160 agentes organizados por área.

## Empezar en 3 pasos

**1. Instalar Claude Code** (solo la primera vez)

```bash
npm install -g @anthropic-ai/claude-code
```

Si no tienes Node.js, instálalo antes desde [nodejs.org](https://nodejs.org) (versión LTS).

**2. Clonar este repositorio**

```bash
git clone https://github.com/mserranouxui/muris-shopify-agent.git
```

**3. Abrir Claude dentro de la carpeta**

```bash
cd muris-shopify-agent
claude
```

> ⚠️ **El `cd` es imprescindible.** Los agentes viven en la carpeta `.claude/` del repositorio: si abres Claude desde otro sitio, no los encontrará.

Para comprobar que ha funcionado, escribe en el chat: *«¿qué agentes tienes disponibles?»*

## Qué hay aquí

| Carpeta / archivo | Qué es |
|---|---|
| [`.claude/agents/`](.claude/agents/) | **160 agentes** por categoría + los dos del proyecto. Ver el [índice](.claude/agents/LEEME-agentes.md) |
| `index.html` · `images/` | Landing del caso práctico → [muris-landing.vercel.app](https://muris-landing.vercel.app) |
| `ONBOARDING-shopify.md` | Plantilla para conectar un agente a tu propia tienda Shopify |
| `resumen-equipo.html` · `.pdf` | Resumen para compartir con el equipo |

## Los dos agentes del proyecto

| Agente | Qué hace |
|---|---|
| **Muris Conector** | Conexión con la Admin API de Shopify, temas Liquid/CSS, SEO técnico on-site |
| **Muris Marketing** | SEO, paid media, social/influencers y growth |

Los dos llevan un **protocolo de doble confirmación**: antes de cualquier cambio real explican qué van a hacer, piden confirmación, y la vuelven a pedir justo antes de ejecutar. Es deliberado — un agente con acceso a una tienda en producción no debería poder actuar a la primera.

## Instalación en Windows

Dos cosas que fallan siempre:

1. **PowerShell bloquea npm.** Si ves un error de *Execution Policy*, ejecuta esto y confirma con `S`:
   ```powershell
   Set-ExecutionPolicy -Scope CurrentUser RemoteSigned
   ```
2. **El instalador de Node.js** abre al final una ventana ofreciendo instalar herramientas adicionales (7 GB). **Ciérrala con la X**, no la necesitas.

## Sobre las credenciales

Nunca pegues un Client ID, un secreto o un `access_token` dentro de un archivo del repositorio, ni aunque sea privado: **el historial de git los conserva aunque los borres después.** Usa variables de entorno o el gestor de secretos del equipo. El detalle está en [`ONBOARDING-shopify.md`](ONBOARDING-shopify.md).

---

Eunoia Digital · 2026
