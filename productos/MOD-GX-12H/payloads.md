# MOD-GX-12H — Alta en las 3 Tiendanube

**Producto Dux:** `MOD IP 12 / 12 PRO GX HARD OLED (IC TRANSPLANTABLE - SIN IC)`
**SKU:** `MOD-GX-12H`

Descripción HTML: la misma para las 3 tiendas (no tiene links externos ni menciones de marca, así que no hay riesgo de marca cruzada).

---

## Campos comunes a las 3 tiendas

| Campo | Valor |
|---|---|
| `name` | Módulo GX iPhone 12 / 12 Pro Hard OLED Con Marco - IC Transplantable |
| `handle` | modulo-gx-iphone-12-12-pro-hard-oled-ic-transplantable |
| `sku` (variante) | MOD-GX-12H |
| `published` | true |
| `stock_management` | true |
| `stock` | 0 |
| `brand` | (vacío — GX no está cargado como marca) |
| Categorías | Pantallas → iPhone → 12 |

**Precios (por variante):**

| Tienda | Precio |
|---|---|
| i2C Mayorista (5046806) | $89.900 |
| Patagonia Cell Bariloche (1609055) | $92.900 |
| Patagonia Cell Neuquén (4603851) | $92.900 |

---

## i2C Mayorista — Store 5046806

- **seo_title** (59): `Módulo GX iPhone 12 / 12 Pro Hard OLED Con Marco | i2C Tech`
- **seo_description** (144): `Módulo iPhone 12 / 12 Pro Hard OLED GX, con marco. IC transplantable, Face ID intacto. Garantía 30 días. Mayorista para técnicos. i2C Mayorista.`
- **tags**:
```
modulo iphone 12, modulo iphone 12 pro, modulo gx, gx, hard oled, pantalla iphone 12, pantalla iphone 12 pro, iphone 12, iphone 12 pro, ic transplantable, modulo sin ic, modulo con marco, a2172, a2402, a2403, a2404, a2341, a2406, a2407, a2408, pantalla compatible con iphone 12, repuesto pantalla iphone 12 pro, modulo oled para iphone, mayorista modulos iphone, 30 dias garantia, cordoba, argentina
```

## Patagonia Cell Bariloche — Store 1609055

- **seo_title** (65): `Módulo GX iPhone 12 / 12 Pro Hard OLED | Patagonia Cell Bariloche`
- **seo_description** (144): `Módulo iPhone 12 / 12 Pro Hard OLED GX, con marco. IC transplantable, Face ID intacto. Stock en Patagonia Cell Bariloche. Envíos a todo el país.`
- **tags**: idénticos a i2C, pero cambiando `cordoba` → `bariloche`

## Patagonia Cell Neuquén — Store 4603851

- **seo_title** (63): `Módulo GX iPhone 12 / 12 Pro Hard OLED | Patagonia Cell Neuquén`
- **seo_description** (142): `Módulo iPhone 12 / 12 Pro Hard OLED GX, con marco. IC transplantable, Face ID intacto. Stock en Patagonia Cell Neuquén. Envíos a todo el país.`
- **tags**: idénticos a i2C, pero cambiando `cordoba` → `neuquen`

---

## Estado

- ✅ HTML de descripción — listo (GX con IC transplantable) → `descripcion.html`
- ✅ SEO title / description / handle / tags por tienda — listos.
- ✅ Precios — cargados.
- ✅ Skill actualizada — GX pasó a "IC Transplantable" (02/09/2026).
- ✅ CSV de importación por tienda — listos (`import_*.csv`).
- ✅ Hoja de carga manual — lista (`hoja_de_alta.html`).
- ⛔ **Alta por API bloqueada.** Ver diagnóstico abajo.
- ⬜ Imágenes — falta la foto del módulo.

---

## Diagnóstico de los tokens (02/09/2026)

Las 3 tiendas devuelven lo mismo contra `GET /store`:

```json
{ "code": 401, "message": "Unauthorized", "description": "Invalid access token" }
```

Probado y descartado:

| Variante | Resultado |
|---|---|
| `v1` + header `Authentication: bearer` | 401 |
| `v1` + header `Authorization: bearer` | 401 |
| `2025-03` + header `Authentication: bearer` | 401 |

No es un problema de formato de header ni de versión de API: los tokens están
revocados. Tampoco se pueden refrescar — no hay `client_id` / `client_secret`
de Tiendanube guardado en ninguna skill (los que están guardados son de
Mercado Libre y Google).

**Para destrabarlo:** reinstalar la app de integración en cada tienda
(Mi Tiendanube → Aplicaciones) o generar tokens nuevos desde
partners.tiendanube.com, y actualizar los 3 `access_token` en la skill
`lapyme-i2c-test` (sección 3.1). Con eso el alta sale por API en un solo paso.

---

## Vías de alta disponibles mientras tanto

### A. Importación por CSV (recomendada)

Un archivo por tienda, ya con todos los campos:

| Archivo | Tienda | Precio |
|---|---|---|
| `import_i2c_5046806.csv` | i2C Mayorista | $89.900 |
| `import_bariloche_1609055.csv` | Patagonia Cell Bariloche | $92.900 |
| `import_neuquen_4603851.csv` | Patagonia Cell Neuquén | $92.900 |

Panel TN → Productos → Importar/Exportar → Importar. Subir el CSV de esa tienda.

Columnas usadas (plantilla estándar de exportación de Tiendanube):
`Identificador de URL`, `Nombre`, `Categorías`, `Precio`, `Stock`, `SKU`,
`Mostrar en tienda`, `Envío sin cargo`, `Descripción`, `Tags`,
`Título para SEO`, `Descripción para SEO`, `Producto Físico`.

> Si el export de la tienda trae columnas distintas, exportar 1 producto
> cualquiera y remapear el CSV contra ese encabezado antes de importar.

### B. Carga a mano

`hoja_de_alta.html` — hoja con cada campo listo para copiar, selector de
tienda y checklist de avance por sucursal.

---

## Pendiente en las 3 tiendas después del alta

- Subir la foto del módulo.
- Verificar que las categorías hayan quedado en `Pantallas → iPhone → 12`
  (la importación por CSV crea la categoría si no matchea el nombre exacto).
- Cargar peso y dimensiones si la tienda calcula envío por peso — no estaban
  definidos en el payload original.
