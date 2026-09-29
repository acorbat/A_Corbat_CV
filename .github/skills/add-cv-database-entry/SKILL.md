---
name: add-cv-database-entry
description: "Add a CV item to the English and Spanish databases. Use when adding education, experience, projects, teaching, publications, presentations, courses, language exams, or other CV content to cv_db/cv_en.yaml and cv_db/cv_es.yaml."
argument-hint: "Describe the CV entry and provide any known dates, institution, role, and outcomes"
---

# Add an Entry to the CV Databases

Update the project's English and Spanish CV databases with a new, user-approved entry while preserving their existing YAML structures and bilingual alignment.

## Procedure

1. Read the current `cv_db/cv_en.yaml` and `cv_db/cv_es.yaml` from the workspace. Treat those files as authoritative; do not rely on pasted excerpts if the workspace files are available. Read the relevant sections and nearby entries in both files.
2. Identify the entry type and the best existing section and subsection in each database. Possible destinations include Education, Experience (Academic, Research, Projects, Teaching and Mentoring, or Professional), Production (Publications, Posters and Oral Presentations, or Outreach), courses/conferences, and Languages. Use the actual section names and organization in each file; do not create a new section unless the user requested one and the existing structure cannot represent the entry.
3. Check both databases for an existing equivalent entry to avoid duplication. Compare the English and Spanish structures and follow the local field conventions, ordering, date format, and indentation. Entries are generally list items identified by `name` or `title`; descriptions are generally lists of strings. Do not assume every field used in one language belongs in the other: preserve each file's established schema while keeping the underlying facts and placement aligned.
4. Identify missing or ambiguous facts needed for an accurate entry, such as dates, role, institution, location, project or publication title, contribution, status, or links. Ask the user focused questions and do not invent facts. Prepare the entry in both English and Spanish, translating the supplied wording when needed while preserving its factual meaning. If a term or phrase has multiple plausible translations that could change meaning, ask the user to clarify it.
5. Before editing either file, present the proposed English and Spanish entry text, the exact section/subsection and insertion point in each file, and any assumptions or fields to omit. Ask the user to confirm that both the details and placement are correct. If the user has not explicitly approved both, pause without editing. Incorporate corrections and request confirmation again if they change the proposed entry or location.
6. After confirmation, add the entry to both databases in the approved locations. Keep the two entries factually equivalent and make no unrelated edits. Do not update backup databases, tailored CVs, templates, or generated outputs unless the user separately asks.
7. Validate both files as YAML with an available YAML parser or project validation command. Review the resulting diff to confirm that only the approved entries changed, both languages were updated, the entries are in the agreed locations, and no duplicate was introduced. Report what was changed and any validation that could not be completed.

## Completion Criteria

- The entry type, destination, and any uncertain facts were resolved with the user.
- The user explicitly approved the proposed details and placement before edits.
- English and Spanish entries were added to their respective databases and remain factually aligned.
- YAML validation and a focused diff review were completed, or any unavailable check was disclosed.