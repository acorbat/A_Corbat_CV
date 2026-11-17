# CV para puesto posdoctoral en análisis de bioimágenes

CV de dos páginas en español, orientado a investigación en análisis de bioimágenes y visión por computadora aplicada a imágenes médicas.

## Renderizado

Desde la raíz del repositorio:

```powershell
pixi run -e rendercv rendercv render .\bia_universidad_postdoc\Agustin_Corbat_CV_BIA_Universidad_Postdoc.yaml --design .\design_moderncv_es.yaml --locale-catalog .\locale_en.yaml --output-folder-name .\bia_universidad_postdoc\rendercv_output
```

La carpeta `rendercv_output` se crea dentro de este directorio. El CV usa el diseño compartido `design_moderncv_es.yaml` y el catálogo compartido `locale_en.yaml`.
