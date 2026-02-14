# CV Analista Senior de Datos/Imágenes Médicas

## Objetivo
CV especializado para aplicación a puesto de analista de datos orientado a análisis de imágenes en empresa de consultoría médica.

## Enfoque del CV

Este CV ha sido diseñado específicamente para destacar:

### Experiencia Profesional y Consultoría
- **Experiencia actual como Analista Senior** en dos instituciones (IFIBA/UBA y BIIF/ScilifeLab)
- Experiencia de investigación postdoctoral en Karolinska Institutet
- **Proyectos de consultoría privada** presentados en sección dedicada (Bohus Biotech, Navinci Diagnostics, Y-TEC)

### Competencias Técnicas Core
- **Análisis cuantitativo de imágenes biomédicas y médicas**
- **Desarrollo de algoritmos y pipelines automatizados**
- **Machine learning y deep learning** aplicado a imágenes
- **Múltiples modalidades de microscopía** incluyendo imágenes médicas (MRI)

### Proyectos Destacados
Se enfatizan proyectos aplicados que demuestran:
- **Consultoría al sector privado** (Bohus Biotech, Navinci Diagnostics, Y-TEC)
- Análisis de imágenes médicas/patológicas del trabajo en BIIF facility (malformaciones cavernosas en MRI, análisis de metástasis)
- Desarrollo de soluciones específicas para problemas de clientes
- Trabajo con imágenes multiplex y análisis espacial

### Formación Multidisciplinaria
- **Doctorado en Física** con enfoque en cuantificación biológica
- **Formación médica** (ciclo troncal completo) que proporciona contexto clínico
- **Experiencia en capacitación** demostrando habilidades de comunicación con audiencias diversas

### Publicaciones Relevantes
Se incluyen solo las publicaciones más relevantes que demuestran:
- Análisis cuantitativo sofisticado
- Colaboración multidisciplinaria
- Publicación en revistas de alto impacto (Science, Development, JCS)

## Contenido Filtrado/Omitido

Para mantener ~2 páginas y enfoque profesional, se omitió:
- Detalles extensos de docencia universitaria
- Premios y distinciones de secundaria
- Lista completa de conferencias y pósters
- Cursos no directamente relacionados con análisis de datos/imágenes
- Proyectos puramente académicos sin aplicación práctica clara

## Estructura del CV

1. **Resumen**: Perfil profesional enfatizando experiencia senior y consultoría
2. **Educación**: Doctorado + Licenciatura en Física + formación médica
3. **Experiencia**: 
   - Posiciones actuales como analista
   - Consultoría profesional
   - Experiencia de investigación aplicada
4. **Proyectos Destacados**: Casos de estudio de proyectos reales de consultoría
5. **Formación y Capacitación**: Experiencia en enseñanza (demuestra comunicación)
6. **Publicaciones Relevantes**: 5 publicaciones clave
7. **Habilidades Técnicas**: Lista detallada de tecnologías y herramientas
8. **Cursos Especializados**: Formación técnica reciente
9. **Idiomas**: Español, Inglés, Francés

## Notas de Renderizado

Para generar el PDF, usar:

```powershell
cd analista_datos_medico
pixi run -e rendercv rendercv render .\Agustin_Corbat_Analista_Senior.yaml --design ..\design_moderncv_es.yaml --locale-catalog ..\locale_en.yaml
```

**Estado actual**: El CV generado tiene **3 páginas**. Si se requiere reducir a 2 páginas estrictas, considerar:
- Reducir el número de proyectos destacados de 4 a 2-3 (mantener los más relevantes médicos)
- Condensar la sección de "Formación Continua" a solo los cursos más relevantes
- Reducir el número de publicaciones de 4 a 3
- Ajustar el espaciado en el archivo de diseño (design_moderncv_es.yaml)

El contenido actual prioriza mostrar experiencia concreta de consultoría y análisis aplicado, lo cual es más valioso que reducir arbitrariamente a 2 páginas si eso significa perder información relevante.
