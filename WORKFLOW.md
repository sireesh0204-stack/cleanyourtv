# Workflow: Antigravity (has project access) + Gemini Argon 4 (NO project access)

## Facts
- Argon 4 only sees what is pasted into its chat. It cannot see any file, resource name, or line number.
- Antigravity handles setup, ADB, settings, builds, and applying code.
- Argon is used only for code generation.

## Rules for every Argon prompt
1. Paste the FULL current text of every method or file Argon must change. Never say "update X" without the code.
2. List the existing resource names it may reference (layouts, drawables, ids). Tell it to use only those.
3. Ask for output as changed methods or a diff only. No whole-file rewrites. No new files unless requested.
4. Tell it: "If something you need is missing, ask. Do not guess names or line numbers."
5. Keep each prompt to one small feature.
6. List every import the new code needs (full package paths) in a separate block. If unsure whether one already exists, list it anyway.

## Before applying Argon's response (Antigravity must do all of these)
1. Check every R.layout / R.id / R.drawable it references exists in the project.
2. Diff each changed file against the original. Flag any removed code that wasn't meant to go.
3. Reject any "replace everything from X to end of file" instruction.
4. Report problems to the user BEFORE editing anything, then apply surgically.
5. Compare the imports Argon listed against the real file's imports. Add missing ones, skip duplicates, and check no used class lacks an import.
