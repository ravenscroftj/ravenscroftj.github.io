---
title: FOAM
tags:
  - software
created: 2024-01-28T21:28
updated: 2024-02-03T21:56
---

Foam is a [[foss]] [[Public/PKM/index]] tool that provides rich linking of notes a bit like [[dendron]] and [[Logseq]] or closed-source solutions like Obsidian or ROAM.

## Foam Templates

It is possible to create templates that FOAM will use to generate new empty notes. I use templates for people, software packages, companies as well as daily and weekly notes.

Templates live within the `.foam` folder in the first project within your VSCode project (the ordering appears to be important for [multi-root](https://code.visualstudio.com/docs/editor/multi-root-workspaces) foam setups like mine).

### Foam Filepath Template Variable

As per the [foam documentation](https://foambubble.github.io/foam/user/features/note-templates#metadata) we can set the `filepath` metadata attribute within `foam_template` to tell foam where to put the new note.

Paths are relative so if you have a multi-root project with a public and a private project, you might want to have templates for public facing notes. For example, my public software page template looks like this:

```yaml
type: note
title: "$FOAM_TITLE"
foam_template:
    filepath: ../public-foam-notes/software/$FOAM_SLUG.md
tags:
 - software
```

Based on a structure like:

```
 workspace/
  |
  |- private-foam-notes 
  |       |
  |       | - templates/
  |       |       |
  |       |       | - public-software.md  <--- the file with the above metadata
  |       |       | ... other templates....
  |       | - note1.md
  |       | ...
  |
  | - public-foam-notes 
  |       | - software/ 
  |       |         | - vscode.md
  |       |         | ... other software...
  |       |      other notes....
```

When creating a note, foam will evaluate the template with the current directory set to be the `private-foam-notes` project so the relative `../public-foam-notes/software` should resolve to the right place.