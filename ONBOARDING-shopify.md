# Plantilla — Conectar un agente Claude a tu tienda Shopify

Esta guía te permite dar a Claude acceso a la Admin API de **tu propia tienda Shopify**, para poder pedirle cambios de catálogo, contenido, temas o pedidos en lenguaje natural.

## 1. Crear la app en el Dev Dashboard

1. Panel de tu tienda → **Configuración → Apps y canales de venta → Desarrollar apps** (te redirige al Dev Dashboard de Shopify).
2. **Apps → Crear app** → elige "Empezar desde Dev Dashboard" y ponle un nombre (ej. `Claude Agent - {tu nombre}`).
3. **Versiones → Crear versión** → en **Alcances (scopes)**, marca solo los permisos que necesitas (cuantos menos, mejor — ver sección de riesgos más abajo).
4. Pulsa **Publicar**.

## 2. Instalar la app en tu tienda

1. Desde la Información general de la app, en "Instalaciones", pulsa **Instalar app**.
2. Selecciona tu tienda y confirma (el aviso de "app no revisada" es normal en apps privadas propias).
3. En Configuración de la app, copia el **ID de cliente** y el **Secreto** (icono del ojo para revelarlo).

## 3. Guardar las credenciales (fuera del repositorio)

**Nunca pegues el Client ID, el Secreto ni un access_token dentro de un archivo que vaya a un repositorio**, ni siquiera uno privado — el historial de git los conserva aunque los borres después.

Guárdalos en variables de entorno locales, o en el gestor de secretos que use tu equipo (1Password, Vault, variables de entorno del proveedor de hosting, etc.):

```bash
export SHOPIFY_STORE="{tu-tienda}.myshopify.com"
export SHOPIFY_CLIENT_ID="{tu_client_id}"
export SHOPIFY_CLIENT_SECRET="{tu_client_secret}"
```

## 4. Obtener el access token

```bash
curl -s -X POST "https://${SHOPIFY_STORE}/admin/oauth/access_token" \
  -H "Content-Type: application/json" \
  -d "{\"client_id\":\"${SHOPIFY_CLIENT_ID}\",\"client_secret\":\"${SHOPIFY_CLIENT_SECRET}\",\"grant_type\":\"client_credentials\"}"
```

La respuesta incluye un `access_token` (empieza por `shpat_`), válido ~24h.

**El token caduca cada 24h.** Repite este paso cuando caduque — o deja que el propio agente lo regenere automáticamente cuando detecte un 401.

## 5. Patrón de conexión (Python)

```python
import os, urllib.request, json

STORE = os.environ["SHOPIFY_STORE"]
TOKEN = os.environ["SHOPIFY_ACCESS_TOKEN"]  # regenerar si ha caducado, ver paso 4
BASE = f'https://{STORE}/admin/api/2024-01'

headers = {'X-Shopify-Access-Token': TOKEN, 'Content-Type': 'application/json'}
```

## 6. Regla fundamental

Nunca editar páginas, productos o el tema publicado sin confirmación explícita del responsable. Trabajar primero en borradores o en una tienda de pruebas.

## 7. Si sois varias personas en el equipo

Una app por persona, todas apuntando a la misma tienda, cada una con solo los scopes que esa persona necesita. Así cada acceso es identificable y revocable sin afectar al resto — evita compartir unas mismas credenciales entre todo el equipo.

## 8. Antes de tocar el catálogo: ¿de dónde viene el dato?

Si el catálogo de tu tienda (precio, stock, variantes) se alimenta desde un ERP u otro sistema externo mediante una integración a medida, **no lo edites directamente vía la API de Shopify** sin comprobar antes cómo funciona esa sincronización — el siguiente ciclo puede sobrescribir tu cambio o generar inconsistencias. Confirma primero con quien mantiene esa integración si el ERP expone su propia API; en ese caso, es preferible conectar el agente ahí en vez de a Shopify directamente para esos campos.
