# Codex Instructions

## Working environment

Codex should continue using its own temporary work environment / worktree.

It is okay for Codex to make changes, apply patches, run commands, and test code inside its own temporary codebase.

Do not change this workflow.

Do not push to GitHub, create pull requests, create branches, or commit changes unless I explicitly ask for that.

Do not build dist folder
## Preferred output format

After making or proposing changes to Vue files, always provide the final result as full, paste-ready Vue files.

I prefer full file contents over diffs.

Do not make the diff / PR layout the main output unless I explicitly ask for a diff, patch, commit, or pull request.

For every changed `.vue` file, provide the entire final file content in a fenced code block.

Use this format:

File: `src/path/to/Component.vue`

```vue
<full final file content here>
```

The code should be ready to copy and paste directly into my project.

## Vue-specific rules

When editing Vue components, include the complete component, including all relevant sections:

```vue
<template>
  ...
</template>

<script setup>
...
</script>

<style scoped>
...
</style>
```

or, if the file uses another Vue style, preserve that style and still provide the complete file.

Do not provide only the changed methods, partial snippets, or isolated blocks unless I explicitly ask for a partial snippet.

Do not omit imports, props, emits, computed values, watchers, lifecycle hooks, styles, or helper functions that are needed for the component to work.

## Explanation style

Before the code, briefly explain what changed.

Keep the explanation short and practical.

After the code, list anything else I need to manually update, such as related files, dependencies, routes, stores, Firebase rules, or environment variables.

## UI preference

When possible, show the full paste-ready Vue file in chat or in the code/output panel as the primary result.

Avoid presenting the final answer mainly as a diff, patch, or PR-style review unless I explicitly ask for that format.
