# CV Generation System - AI Agent Guide

## Project Overview
This is a CV/resume generation system using **RenderCV** (Typst/Markdown-based) with custom Jinja2 templates. The project maintains CVs in multiple languages (English/Spanish) with two output formats:
- **Standard CVs**: Generated via RenderCV with custom Typst templates (moderncv theme)
- **UBA Academic Format**: Special Jupyter-based processor for Universidad de Buenos Aires applications

## Architecture

### Data Layer (`cv_db/`)
- `cv_en.yaml` / `cv_es.yaml`: Complete CV content databases (education, experience, publications)
- `transcript_en.yaml` / `transcript_es.yaml`: Academic transcript data
- **Structure**: Nested YAML with sections like "Career Statement", "Education", "Experience", "Research", etc.
- **Convention**: Use nested dictionaries for hierarchical organization (e.g., Education → University → Ph. D. in Physics)

### Template Layer
Two parallel template systems for different output formats:

**Typst Templates** (`moderncv/`):
- Custom modernCV theme templates using Jinja2 syntax with special delimiters: `((*` and `*))`
- `Preamble.j2.typ`: Sets up Typst variables from YAML design config (colors, fonts, spacing)
- Entry templates: `ExperienceEntry.j2.typ`, `EducationEntry.j2.typ`, `PublicationEntry.j2.typ`, etc.
- **Key Pattern**: Templates use `two-col-entry()` and `one-col-entry()` functions for layout
- Access design config via variables like `design-text-font-size`, `design-colors-section-titles`

**Markdown Templates** (`markdown/`):
- Simpler Jinja2 templates for Markdown output
- Same entry types as Typst templates but with Markdown formatting

### Configuration Files
- `design_moderncv_es.yaml`: Design system config (colors, fonts, spacing, page layout)
- `locale_en.yaml`: Localization settings (date formats, text labels, month names)
- `Agustin_Corbat_CV.yaml`: Main CV file (placeholder/example structure)
- `pixi.toml`: Environment and dependency management

## Key Workflows

### Rendering Standard CV
```powershell
pixi run -f rendercv rendercv render .\Agustin_Corbat_CV.yaml --design .\design_moderncv_es.yaml --locale-catalog .\locale_en.yaml
```
- **Input**: CV YAML + design YAML + locale YAML
- **Output**: PDF via Typst compilation
- **Note**: The command references main YAML file, but actual CV data is in `cv_db/`

### UBA Academic Format Processing
```powershell
pixi run -f uba jupyter lab
# Then open render_uba/render_uba.ipynb
```
- **Purpose**: Transform CV data into UBA's specific academic application format
- **Process**: Loads `cv_db/cv_es.yaml`, restructures data per UBA requirements
- **Sections**: "Antecedentes Docentes" (teaching history), course listings, etc.

### Environment Management
Project uses **pixi** (conda-based) with two environments:
- `rendercv`: Contains rendercv with full extras for CV generation
- `uba`: Contains JupyterLab for notebook processing

Switch environments with: `pixi run -f <environment> <command>`

## Template Development Patterns

### Jinja2 Syntax Specifics
- **Delimiters**: `((*` expression `*))` and `((*` statement `*))` (NOT standard `{{` `}}`)
- **Filters**: Custom RenderCV filters like `|escape_typst_characters`, `|replace_placeholders_with_actual_values`
- **Conditionals**: Check for content existence: `((* if entry.date_string *))`
- **Loops**: Iterate over highlights/descriptions: `((* for item in entry.highlights *))`

### Layout Convention (Typst)
- **Two-column entries**: Date/location on right, content on left (see `ExperienceEntry.j2.typ`)
- **One-column entries**: Full-width content for sections without dates
- **Spacing control**: Use `#v(-design-text-leading)` to adjust vertical spacing between elements

### Design Variable Access
All design settings from YAML are exposed as Typst variables with prefix `design-`:
- Colors: `design-colors-section-titles`, `design-colors-links`
- Typography: `design-text-font-family`, `design-section-titles-font-size`
- Layout: `design-header-photo-width`, `design-entries-date-and-location-width`

## Data Structure Conventions

### CV YAML Schema
- **Dates**: Use `date: YYYY--YYYY` or `date: YYYY--actual` format
- **Hierarchical sections**: Nest related items (e.g., Teaching → Position Title → date/location/description)
- **Descriptions**: Array of strings for bullet points or paragraphs
- **Locations**: Full institutional names with department/faculty details

### Bilingual Content
- Maintain parallel English (`_en`) and Spanish (`_es`) files
- Ensure structural consistency between language versions
- Design/locale files can be language-specific or shared

## Important Notes

- **No direct Python scripts**: All CV generation goes through RenderCV CLI
- **Template modifications**: Changes to `.j2.typ` or `.j2.md` files require re-rendering
- **Photo support**: Design supports profile photos via `photo_width` in header config
- **Page numbering**: Automatic via locale template `page_numbering_template`
- **External links**: Use icon indicators via `use_external_link_icon` setting

## Common Tasks

**Adding a new CV section**: Create YAML entry in `cv_db/cv_*.yaml` + corresponding template file in both `moderncv/` and `markdown/` directories

**Changing design**: Modify `design_moderncv_es.yaml` values (colors, fonts, spacing) and re-render

**Language switching**: Use appropriate locale file (`locale_en.yaml` vs `locale_es.yaml`) and CV database (`cv_en.yaml` vs `cv_es.yaml`)

**UBA format updates**: Edit `render_uba/render_uba.ipynb` notebook to adjust data transformation logic
