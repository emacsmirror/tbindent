---
title: Why 2-Space Indentation is an Accessibility Barrier (And How I Solved It in Emacs)
published: on [Dev.to](https://dev.to/rouleaup/why-2-space-indentation-is-an-accessibility-barrier-and-how-i-solved-it-in-emacs-2g49)
tags: emacs, accessibility, elisp, productivity
description: >
  Rigid 2-space project linting guidelines present a
  real accessibility hurdle for visually impaired developers.
  Here is how tbindent-mode decoupling viewing from saving in Emacs.
---

We’ve all seen it: the modern frontend and backend developer ecosystem has largely consolidated around space-based indentation.
Tools like Prettier and ESLint enforce rigid styling guidelines, and a massive portion of open-source projects have settled on a strict **2-space indentation** standard.


To many, this is seen as a victory for "consistency."
But there is a massive blind spot in this dogmatic approach: **identical formatting is not a feature; it is an accessibility barrier.**

## The Visual Accessibility Blind Spot

When a project forces a 2-space layout directly into the repository files, it dictates exactly how every developer's eyes must process information.

For developers with visual impairments, specific monitor setups, or neurodivergence, a 2-space visual separation is often incredibly strained and difficult to read.
They might *need* 4 or 8 columns of visual separation to comfortably track nested logic blocks.

The standard argument for spaces is that "tabs break layout alignment."
But this completely confuses **indentation** (how deep a line is in the logic tree) with **alignment** (how text aligns relative to a specific character).

Code formatting should be a client-side rendering choice, not a permanent data-layer constraint.

## The Solution: Decoupling Viewing from Saving

I believe that the editor should bend to the user, not the other way around.
To solve this problem for developers who struggle with narrow, unchangeable space-indented codebases, I wrote a minor mode for Emacs called **`tbindent-mode`**.

It allows you to **edit space-based indented files as if they were tab-based**, giving you absolute control over the visual column width while editing, without altering the underlying file content.

Even people without any visual issue benefit from the mode; you can quickly change the way the buffers renders the indentation to highlight some logic, all without changing the content of the file.

### How it works:

1. **On Activation:** It hooks into your major mode, transparently converts each group of spaces into a hard tab, activates `indent-tabs-mode`, and lets you scale the visual width (`tab-width`) to whatever your eyes require (e.g., 4 or 8 columns).
2. **On Save:** When you save the buffer, `tbindent-mode` seamlessly converts the text back to the repository's native space-based indentation scheme before writing to disk.  Your team's CI/CD pipelines and linters never know the difference.
3. **Smart Integration:** It excludes these conversions from the buffer’s undo list (treating it strictly as a visual rendering layer) and pairs with `dtrt-indent-mode` to accurately detect the file's native layout automatically.

## Give it a Try

If you are tired of straining your eyes against rigid 2-space project guidelines, or if you want to reclaim visual control over your editing environment, `tbindent-mode` is available right now on **MELPA**.

* **Repository:** [GitHub - pierre-rouleau/tab-based-indent](https://github.com)

I’ve been incredibly glad to see that the developers most excited about this project are those dealing with visual fatigue or disability problems. Technology should be inclusive, and that includes the environments we use to build it.

I’d love to hear your thoughts—especially if you've run into similar accessibility roadblocks with modern linter configurations!
