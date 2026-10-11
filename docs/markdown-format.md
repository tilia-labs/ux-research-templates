# tilia markdown format

Format version 1 · October 2026

tilia can import the structure of a study from a markdown (`.md`) or plain text (`.txt`) file. This page explains exactly what the import reads, what it ignores, and what you still add by hand. Every template in this repo follows these rules.

## What can be imported

| Study type | What the file creates | What you add in tilia |
| --- | --- | --- |
| Tree test | The tree (your navigation, as an indented list) | Tasks and their correct answers |
| Card sort | The cards (a flat list) | Sort type (open or closed) and, for a closed sort, the categories |

Other study types (first-click, five-second, preference and survey) can't be imported from markdown yet. You build those in tilia's study builder.

## The one rule: only bullet lines are read

The import reads every line that starts with `-` or `*` (spaces or tabs before it are fine). Everything else is ignored: headings, paragraphs, numbered lists, tables, links and code fences.

That means a file can hold notes, tasks and instructions alongside the list, as long as none of those lines start with `-` or `*`. Use paragraphs or numbered lists (`1.`, `2.`) for anything that isn't part of the tree or the cards.

A file can be uploaded, or its contents pasted into the import box. Both work the same way.

## Tree tests

A tree test checks whether people can find things in your navigation without the visual design getting in the way. Participants see only the labels, click down through the levels, and pick where they'd expect to find the answer to a task.

### Syntax

Each bullet is one item in the tree. Indentation sets the level: an item indented under another becomes its child.

Minimal example:

```markdown
- Home
  - Products
    - Laptops
    - Phones
  - Support
    - Contact us
```

### How the top of the tree works

If the list has exactly one top-level item (like `Home` above), that item becomes the root of the tree. If it has more than one, tilia wraps them all under a root called `Home`.

The root is the starting point and isn't something participants can choose as an answer. So these two files produce the same tree:

```markdown
- Home
  - Products
  - Support
```

```markdown
- Products
- Support
```

### Indentation

Any consistent indent works: 2 spaces, 4 spaces or tabs. What matters is that an item is indented further than its parent. Don't mix tabs and spaces in one file, because a tab counts as one character of indentation, the same as one space.

### Importing a tree

1. In tilia, choose **+ New study**, then **Tree testing**.
2. With the tree still empty, click **import a markdown file**.
3. Upload the `.md` file, or paste the list, then click **Import**.

The import link only shows while the tree is empty. To re-import, clear the tree first.

You can also import a tree in the **Create with AI** flow, which has its own tree import step.

### Tasks and correct answers

Tasks aren't imported. Each template lists its tasks as a numbered list with the correct answer written as a path, for example:

```markdown
1. You want to check when your parcel will arrive. Where would you go?
   Correct answer: Account › Orders
```

Add each task in tilia under **Tasks**, then select the correct answer in the tree. A task can have more than one correct answer. Paths start below the root, so `Account › Orders` means the `Orders` item inside `Account`.

To publish, a tree test needs at least one task, and every task needs a question and at least one correct answer.

## Card sorts

A card sort shows participants a set of cards and asks them to group them. In an **open sort**, they create and name their own groups, which tells you how people think about your content. In a **closed sort**, they sort cards into categories you've set, which tests whether a proposed structure makes sense.

### Syntax

Each bullet is one card. Indentation is ignored: every bullet becomes a card, however deep it is.

Minimal example:

```markdown
- Change your password
- Download an invoice
- Invite a teammate
- Cancel your plan
```

### Importing cards

1. In tilia, choose **+ New study**, then **Card sort**, and pick **Open sort** or **Closed sort**.
2. With no cards added yet, click **import a markdown file**.
3. Upload the `.md` file, or paste the list, then click **Import**.

### Categories (closed sorts)

Categories aren't imported. Closed-sort templates list suggested categories as a numbered list. Add them in tilia under **Categories**.

To publish, a card sort needs at least 3 cards. A closed sort also needs at least 2 categories.

## Common mistakes

| Mistake | What happens | Fix |
| --- | --- | --- |
| A note or task starts with `-` or `*` | It becomes a tree item or a card | Write it as a paragraph or numbered list |
| A line starts with bold text, like `**Note:**` | It starts with `*`, so it's read as a bullet | Start the line with a word, or put the bold text mid-sentence |
| A horizontal rule (`---` or `***`) | It becomes an item called `--` or `**` | Use a heading to split the file instead |
| Tabs and spaces mixed | Items end up at the wrong level | Pick one and use it throughout |
| Markdown inside a label, like `- [Pricing](/pricing)` | The label shows the raw text, brackets and all | Use plain text labels |
| No bullet lines at all | Import fails with "Couldn't parse this" | Check each item starts with `-` or `*` |

## Checking a file before you upload

Search the file for lines starting with `-` or `*`. Every match should be part of the tree or the card list, and nothing else. In most editors, a regular expression search for `^\s*[-*]` finds them all.

## Changes to this format

Changes to what the import reads are recorded here and in the changelog.

| Version | Date | Change |
| --- | --- | --- |
| 1 | October 2026 | First published version: tree and card import from bullet lists. |
