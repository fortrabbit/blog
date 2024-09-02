---
author: fl
created: 2024-02-12
figure:
  emoji: 🤔
  text: Was it `⌘ + ⇧ + U` or `⌘ + K`?
title: The tyranny of inconsistent keyboard shortcuts
lead: A rant about how difficult it is to adapt keyboard shortcuts across multiple programs as a human.
intro: 'Keyboard shortcuts are my productivity fuel. Navigating inconsistent keyboard shortcut landscapes across different programs feels like an obstacle course. A significant number of interactions remain universal across software. Why then, must we relearn basic actions like "insert link" with every new tool?'
tags:
  - opinion
---

This is specifically about my experience using: Linear, Notion, Slack, 1Password, Intercom, Google Docs, Obsidian and VS Code in parallel. It applies to standalone applications on my macOS system, but also to software in the browser.

## Examples

- Insert a link
  - Slack: `⌘ + ⇧ + U`
  - Most others: `⌘ + K`
- Show the sidebar
  - VSCode: `⌘ + B`
  - Notion: `⌘ + \`
  - Linear: `[`
- Search
  - VS Code: `⌘ + P`
  - Notion: `⌘ + P` or `⇧ + ^ + ⌥ + ⌘ + K`
  - Linear: `/`
  - Slack: `⌘ + G` and `⌘ + F`
  - Intercom: `⌘ + P`
- Command toolbar
  - VS Code: `⌘ + ⇧ + P`
  - Intercom: `⌘ + K`
  - Obsidian: `⌘ + P`
- Inline code block
  - Slack: `⌘ + ⇧ + C`
  - Most others: `⌘ + E`
- Copy the link to the current context
  - Notion: `⌘ + L`
  - Linear: `⌘ + ⇧ + .`
  - Slack: `L` but only if you clicked the menu already

I am German, and certain characters like `[` and `]` are hard to reach on a German keyboard. So I have an English keyboard now and need to do a limbo to type an `Ü`. I can only imagine how hard it is for Dvorak users.

Modern WYSIWYG editors have 'Markdown support', yet I often find myself struggling to escape a code block or changing a headline class. `⌘ + N`, `⌘ + C`, `⌘ + V` are set in stone. But even what the `ESC` key does varies a lot. I hit `⌘ + S` every 5 minutes in any document, it's part of my muscle memory. Now Linear will strike out my text for that. Without warning 1Password recently introduced a global (!) shortcut to open the mini window. Now when I try to indent code in VS Code, 1Password pops up ([Reddit](https://www.reddit.com/r/1Password/comments/wzmh9j/disable_global_keyboard_shortcuts_in_1password_8/)).

Is locking-in users through custom shortcuts your business strategy? At least some programs let you tweak shortcuts.

## A modest proposal

VS Code and other IDEs offer 'keymaps': sets of keyboard shortcuts that are compatible with other programs. Sublime user switching to VS Code? No problem, continue using your shortcuts. That's a good start.

Imagine an operating system providing keymap settings. Or maybe that is happening in the browser. With that, a (web) application doesn't need to know where you are located, which keyboard layout you are using or what your preference is. It just needs to compute after receiving an event.

This is a plea for standardization, advocating for a more harmonious keyboard shortcut landscape. Universal shortcuts: one command, any app, no config hassle.

## My background

We are currently working on a browser based graphical interface (dashboard) for our [new hosting platform](https://new.fortrabbit.com). In addition to mouse navigation, I was keen on creating a system that can be controlled by keyboard in a fast and accessible way. The lack of available standards was the main reason we abandoned the project. As a small team, we can't put much effort into an island solution.

I like standards. Browsers already offer native keyboard navigation. With the `TAB` you can cycle focus through active elements. Use `SPACE` to select things and arrow keys to travel through radio groups. There is accesskey ([MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/accesskey)) and [WebAIM](https://webaim.org/techniques/keyboard/accesskey) as well. But are they suited for modern requirements? I am not so sure.

I will never learn VIM, but I can understand VIM users who don't want to learn something else.

**EDIT**: I was pointed to existing software solutions. There are for sure browser extensions. For macOS there is a (free) App [customShortcuts by Houdah](https://www.houdah.com/customShortcuts/), which also is compatible with [KeyClu](https://github.com/Anze/KeyCluCask).
