# CV Generation System - AI Agent Guide

## Project Overview
This is a CV/resume generation system using **RenderCV** (Typst/Markdown-based) with custom Jinja2 templates. The project maintains CVs in multiple languages (English/Spanish) with two output formats:
- **Standard CVs**: Generated via RenderCV with custom Typst templates (moderncv theme)
- **UBA Academic Format**: Special Jupyter-based processor for Universidad de Buenos Aires applications

## Architecture

### Data Layer (`cv_db/`)
- `cv_en.yaml` / `cv_es.yaml`: Primary CV content databases (education, experience, publications, projects)
- `main.yaml` / `main_en.yaml`: Alternative CV databases (legacy/backup files)
- `transcript_en.yaml` / `transcript_es.yaml`: Academic transcript data
- **Structure**: List-based YAML with sections like "Resumen"/"Career Statement", "Educación"/"Education", "Experiencia"/"Experience" (with subsections: Académico, Investigación, Proyectos, Docencia y Formación, Profesionales), "Producción"/"Production"
- **Convention**: Use **list-based structures** with consistent field names (`name:` or `title:` for entry identification) rather than nested dictionaries. This ensures compatibility with render_uba notebook and template processing.
- **Synchronization**: `cv_en.yaml` and `cv_es.yaml` must maintain parallel structure and content across languages

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
- **Process**: Loads `cv_db/cv_es.yaml` (or `main.yaml` as fallback), restructures data per UBA requirements
- **Sections**: "Antecedentes Docentes" (teaching history), "Proyectos", "Posters y Presentaciones Orales", "Divulgación Científica", course listings
- **Recent Updates**: Notebook cells updated to handle list-based YAML structures with consistent field parsing (title, event, date, authors, description)

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
- **List-based sections**: Each section should contain a list of entries rather than nested dictionaries
- **Entry identification**: Use `name:` or `title:` fields consistently for entry identification
- **Subsections in Experience**: Académico, Investigación, Proyectos, Docencia y Formación, Profesionales
- **Descriptions**: Array of strings for bullet points or paragraphs
- **Locations**: Full institutional names with department/faculty details
- **Avoiding duplicates**: Keep research positions only in Investigación subsection, not in Académico

### Bilingual Content
- Maintain parallel English (`_en`) and Spanish (`_es`) files
- Ensure structural consistency between language versions (matching sections, same number of entries)
- Keep content synchronized: when adding entries to one language, add to the other
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

**Maintaining file synchronization**: 
- When adding entries to `cv_es.yaml`, add parallel entries to `cv_en.yaml`
- Use list-based structures with `name:` or `title:` fields for consistency
- Keep `main.yaml` and `main_en.yaml` as backup/alternative versions
- Avoid duplicating entries across subsections (e.g., keep research only in Investigación, not in Académico)

## Recent Maintenance (February 2026)

**File Synchronization Completed**:
- All CV databases (`cv_en.yaml`, `cv_es.yaml`, `main.yaml`) now use consistent list-based structures
- Separated Proyectos/Projects section from Académico/Academic in all files
- Removed duplicate research positions from cv_es.yaml (kept only in Investigación subsection)
- Added missing content to cv_en.yaml: BIIF facility projects, professional consulting entries (Bohus Biotech, Navinci), High School student supervision
- Aligned dates across language versions (UBA: 2024--actual, Bachelor supervision: 2023--2024)

**Notebook Updates**:
- Updated `render_uba.ipynb` cells to handle list-based YAML structures
- Simplified parsing logic for "Posters y Presentaciones Orales" and "Divulgación Científica"
- Added fallback logic to extract Proyectos from Académico if separate section doesn't exist

**Best Practices Established**:
- Use list-based YAML structures for better template compatibility
- Maintain separate subsections in Experience to avoid structural confusion
- Keep bilingual files synchronized in both structure and content
- Document date formats consistently (YYYY--actual for ongoing positions)
