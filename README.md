# México – Mapa por sector (D3 + TopoJSON)

Publica estos archivos en **GitHub Pages** (misma carpeta) para que el mapa funcione:
- `index.html` – visor D3 (lee TopoJSON + CSV + palette).
- `mx_tj.json` – **TopoJSON de estados** (objeto `states`). Propiedades: `state_code/state_name` o `CVE_ENT/NOM_ENT`.
- `mx_state_sector_codes.csv` – CSV con `state_code,sector` (códigos INEGI de 2 dígitos).
- `palette.json` – (opcional) colores corporativos por sector.

## Cómo publicar
1) Sube estos archivos al repo.  
2) Settings → Pages → Source: `main`/`gh-pages`, carpeta `/root` (o `/docs`).  
3) Abre `https://usuario.github.io/tu-repo/`.

## Generar TopoJSON (ejemplos)
- **topojson (clásico):**
```
ogr2ogr states.shp Entidades_2010_5.shp -t_srs EPSG:4326
topojson -o mx_tj.json -s 1e-7 -q 1e5   -p state_code=+CVE_ENT,state_name=NOM_ENT   states.shp
```
- **mapshaper (rápido):**
```
mapshaper Entidades_2010_5.shp encoding=latin1 -proj wgs84 -clean   -rename-fields state_code=CVE_ENT,state_name=NOM_ENT   -simplify 1% keep-shapes   -o format=topojson precision=0.0001 mx_tj.json
```

## Ajustes en `index.html`
- Si tu objeto no se llama `states`, cambia la línea `const obj = topo.objects.states || ...`.
- Si tus props son `CVE_ENT/NOM_ENT`, el código ya intenta leerlas; no es necesario modificar.

¡Listo para subir a GitHub Pages o usar los enlaces raw en CodePen!