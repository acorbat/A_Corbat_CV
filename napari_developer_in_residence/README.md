# napari Developer-in-Residence Application

Application materials for the napari remote Developer-in-Residence call.

## Files

- `Agustin_Corbat_Napari_Developers_in_Residence_EN.yaml`: tailored CV source.
- `Statement_of_Interest.md`: statement of interest.
- `Representative_Contribution.md`: representative software contribution and repository link.
- `Application_Responses.md`: portfolio, availability, interview window, and contractor-status response.
- `rendercv_output/`: rendered CV files.

## Render the CV

Run from the workspace root:

```powershell
	pixi run -e rendercv rendercv render "napari_developer_in_residence\Agustin_Corbat_Napari_Developers_in_Residence_EN.yaml" --design ".\design_moderncv_es.yaml" --locale-catalog ".\locale_en.yaml" --output-folder-name "napari_developer_in_residence/rendercv_output"
```