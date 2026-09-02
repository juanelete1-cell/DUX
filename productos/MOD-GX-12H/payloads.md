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

## Estado — ALTA COMPLETA (02/09/2026)

Creado por API en las 3 tiendas. Una publicación por tienda, verificada.

| Tienda | Store | Product ID | Precio |
|---|---|---|---|
| i2C Mayorista | 5046806 | `364966117` | $89.900 |
| Patagonia Cell Bariloche | 1609055 | `364966370` | $92.900 |
| Patagonia Cell Neuquén | 4603851 | `364966739` | $92.900 |

URL en las 3 (mismo handle):
`/productos/modulo-gx-iphone-12-12-pro-hard-oled-ic-transplantable/`

- ✅ Descripción HTML (9.430 caracteres) — idéntica en las 3.
- ✅ SEO title / description / handle / tags (27 etiquetas) por tienda.
- ✅ Precio, SKU `MOD-GX-12H`, control de stock activo.
- ✅ Categorías asignadas.
- ✅ Publicado en las 3.
- ⬜ **Foto del módulo** — las 3 publicaciones están sin imagen.
- ⬜ **Stock** — quedó en 0, así que figura sin stock hasta cargarlo.

---

## Decisiones tomadas contra lo que decía el payload original

El payload original marcaba `brand` vacío ("GX no está cargado como marca").
Al revisar los módulos hermanos ya publicados, la convención real de las
tiendas es usar la marca del **teléfono**, no la del fabricante del módulo:

| Producto hermano | brand |
|---|---|
| Módulo JK iPhone 12 / 12 Pro | IPHONE |
| Módulo TW iPhone 12 / 12 Pro Soft | IPHONE |
| Módulo GX iPhone 12 Pro Max Soft | IPHONE |

Se cargó `brand: IPHONE` para no dejarlo huérfano en los filtros de marca.
En Neuquén la tienda usa `Apple iPhone` en vez de `IPHONE`, así que ahí se
respetó esa forma.

También se copiaron del módulo hermano **peso 0.090 kg** y **medidas
1 × 6 × 16 cm**, que el payload original no definía.

### Categorías por tienda

Los IDs de categoría son distintos en cada tienda, se resolvieron por nombre:

| Tienda | Categorías asignadas |
|---|---|
| i2C Mayorista | `26251716` Pantallas · `26251740` iPhone · `35492648` 12/12 Pro/12 Pro Max · `39702929` Repuestos por modelo · `39703056` Repuestos iPhone 12 |
| Bariloche | `9187261` · `9187265` · `34059867` |
| Neuquén | `24976428` · `24976456` · `33919363` |

Bariloche y Neuquén no tienen el árbol "Repuestos por modelo" que sí tiene
Córdoba, por eso quedan con 3 categorías en vez de 5. Es correcto.

---

## Historial: los tokens estaban revocados

Los 3 tokens que había guardados devolvían `401 · Invalid access token`
(probado en API v1 y 2025-03, con header `Authentication` y `Authorization`).
Control: el token de Torba Café respondía `200` con el mismo código, o sea
que la conexión y el formato estaban bien — esos 3 estaban revocados.

Se destrabó rehaciendo el OAuth con la app propia (App ID `26974`):
autorizando la app en cada tienda y canjeando el `code` por un
`access_token` nuevo.

> **Los 3 tokens nuevos hay que actualizarlos en la skill
> `descripcion-productos`** (sección de credenciales, al final). No se
> guardan en este repo.

---

## Archivos

| Archivo | Para qué |
|---|---|
| `descripcion.html` | La descripción publicada en las 3. |
| `hoja_de_alta.html` | Ficha del alta: campos publicados y lo que falta. |
| `import_*.csv` | Vía alternativa por importación CSV. Ya no hace falta, quedan como respaldo. |
