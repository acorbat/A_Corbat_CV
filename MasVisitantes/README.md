# CV académico para +Visitantes (UBA)

CV en español (3 páginas) orientado a docencia universitaria, investigación y transferencia en análisis de bioimágenes.

## Render

```powershell
pixi run -e rendercv rendercv render .\MasVisitantes\Agustin_Corbat_CV_MasVisitantes.yaml --design .\MasVisitantes\design_masvisitantes.yaml --locale-catalog .\MasVisitantes\locale_es.yaml --output-folder-name MasVisitantes\rendercv_output
```

`design_masvisitantes.yaml` es una versión compacta (A4, 9,5 pt) de `design_moderncv_es.yaml` para ajustar a 3 páginas; `locale_es.yaml` localiza fechas y numeración.
