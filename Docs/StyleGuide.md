# StyleGuide

> **Project:** Football Hub (Working Title)
> **Version:** 1.0.0
> **Status:** Active

---

# Overview

This document defines the visual identity and user experience principles of Football Hub.

Its purpose is to ensure that every page, component, and interaction feels like part of the same product.

Consistency is more important than creativity.

Whenever a design decision is unclear, prioritize clarity, accessibility, and usability.

---

# Design Philosophy

Football Hub should feel like a modern SaaS platform rather than a traditional football website.

The interface should communicate:

* Professionalism
* Speed
* Simplicity
* Reliability
* Premium quality

The user should immediately understand where to click and what information is most important.

---

# Design Principles

Every screen should follow these principles.

## Hierarchy

Important information should always stand out.

Visual hierarchy should be created using:

* Size
* Weight
* Contrast
* Spacing

Never rely only on color.

---

## Simplicity

Every component should have a clear purpose.

Avoid:

* Decorative elements
* Unnecessary animations
* Visual clutter
* Duplicate actions

---

## Consistency

The same action should always look and behave the same way.

Examples:

* Primary buttons always use the primary color.
* Delete actions are always destructive.
* Cards follow the same spacing.
* Tables share identical layouts.

---

## Accessibility

Accessibility is mandatory.

Minimum requirements:

* WCAG AA contrast.
* Keyboard navigation.
* Visible focus states.
* Semantic HTML.
* Screen reader compatibility.
* Accessible form labels.

---

# Visual Style

The application should feel:

* Modern
* Clean
* Data-driven
* Minimalistic

Avoid skeuomorphic or overly decorative interfaces.

---

# Color Palette

## Primary

```text id="5gqggo"
Blue 600
```

Primary actions.

---

## Secondary

```text id="3qvg8t"
Slate
```

Navigation.

Secondary controls.

---

## Success

```text id="sxvjlwm"
Green
```

Successful operations.

---

## Warning

```text id="ab89or"
Amber
```

Warnings.

---

## Error

```text id="cqgzms"
Red
```

Validation errors.

Critical actions.

---

## Neutral

Gray scale for backgrounds, borders, and typography.

Dark mode should use neutral tones rather than pure black.

---

# Typography

Primary font

```text id="lhd2lh"
Inter
```

Fallback

```text id="v8j5g3"
system-ui
```

---

## Font Scale

Page Title

48px

---

Section Title

32px

---

Card Title

24px

---

Subtitle

20px

---

Body

16px

---

Small Text

14px

---

Caption

12px

Typography should follow a consistent vertical rhythm.

---

# Spacing System

Use an **8-point spacing system**.

Examples

```text id="rm0fdo"
4px

8px

16px

24px

32px

48px

64px
```

Avoid arbitrary spacing values.

---

# Border Radius

Small

```text id="pqh2w4"
6px
```

Medium

```text id="lgoh8n"
10px
```

Large

```text id="efvctm"
16px
```

Rounded corners should remain subtle.

---

# Shadows

Use shadows only to communicate elevation.

Three elevation levels are sufficient.

* Small
* Medium
* Large

Avoid excessive shadow usage.

---

# Layout

Maximum content width

```text id="jlwm9q"
1440px
```

Page content should remain centered.

Large displays should increase whitespace rather than stretching content.

---

# Responsive Design

Breakpoints

| Size          |  Width |
| ------------- | -----: |
| Mobile        |  640px |
| Tablet        |  768px |
| Laptop        | 1024px |
| Desktop       | 1280px |
| Large Desktop | 1536px |

The interface should be fully responsive.

Mobile-first development is preferred.

---

# Navigation

Main navigation should always include:

* Home
* Players
* Teams
* Competitions
* Matches
* Search

Authenticated users additionally see:

* Favorites
* Lists
* Notifications
* Profile

Administrators also see:

* Admin Panel

---

# Cards

Cards are the primary content container.

Every card should contain:

* Header
* Body
* Optional footer

Cards should maintain consistent spacing across the application.

---

# Buttons

## Primary

High emphasis.

Used for the main action.

Examples

* Login
* Save
* Register

---

## Secondary

Supporting actions.

Examples

* Cancel
* Edit
* View Details

---

## Ghost

Low emphasis.

Examples

* Navigation
* Filters
* Toolbar actions

---

## Destructive

Red button.

Reserved for:

* Delete
* Block
* Remove

---

# Forms

Forms should:

* Validate in real time when appropriate.
* Display clear error messages.
* Preserve entered values after validation errors.
* Clearly indicate required fields.

Primary action buttons remain disabled until the form is valid when appropriate.

---

# Tables

Tables should support:

* Sorting
* Pagination
* Responsive layout
* Empty states
* Loading states

Never display horizontal scrolling on common desktop resolutions.

---

# Search Experience

Search should be one of the strongest features of the application.

Requirements

* Instant feedback.
* Debounced requests.
* Keyboard navigation.
* Highlight matching text.
* Recent searches.
* Empty state suggestions.

---

# Loading States

Avoid blank pages.

Preferred loading techniques:

* Skeletons
* Progressive rendering
* Lazy loading

Avoid traditional spinning loaders whenever possible.

---

# Empty States

Every empty state should explain:

* Why nothing is displayed.
* What the user can do next.

Example

```text id="7rz2wa"
No favorite players yet.

Start following players to build your personalized dashboard.
```

---

# Error States

Errors should:

* Explain what happened.
* Suggest a recovery action.
* Never expose technical details.

Bad

```text id="8zk0wr"
500 Internal Server Error
```

Better

```text id="jlwmj9"
Something went wrong while loading this player.

Please try again in a few moments.
```

---

# Icons

Use a single icon library across the project.

Recommended

```text id="gd0qgr"
Lucide React
```

Icons should always reinforce meaning, never replace text.

---

# Images

Player photos

Fixed aspect ratio.

Team logos

Transparent background preferred.

Competition logos

Consistent sizing.

All images should be optimized before rendering.

---

# Animations

Animations should be subtle.

Recommended duration

```text id="pwc67v"
150–250 ms
```

Animations should communicate state changes.

Avoid decorative animations.

---

# Dark Mode

Dark mode should be supported from the beginning.

Requirements

* Equal feature parity.
* Accessible contrast.
* Consistent colors.
* No pure black backgrounds.

---

# Notifications

Notifications should be concise.

Success

Green accent.

Warning

Amber accent.

Error

Red accent.

Notifications should automatically disappear unless user interaction is required.

---

# Data Visualization

Statistics should prioritize readability.

Preferred components

* Progress bars
* Comparison cards
* Radar charts (future)
* Bar charts
* Line charts

Avoid excessive visual complexity.

---

# Football Pages

Player pages should prioritize:

1. Identity
2. Current Team
3. Position
4. Main Statistics
5. Career
6. Transfers

Team pages should prioritize:

1. Club Information
2. Squad
3. Standings
4. Fixtures
5. Statistics

Competition pages should prioritize:

1. Standings
2. Fixtures
3. Results
4. Statistics

Information hierarchy should remain consistent throughout the application.

---

# UX Principles

Every interaction should satisfy these questions:

* Is it obvious?
* Is it fast?
* Is it consistent?
* Is it accessible?
* Is it recoverable if something fails?

If any answer is "No", the interaction should be redesigned.

---

# Definition of Good Design

A screen is considered complete when:

* The purpose is immediately clear.
* Navigation requires minimal effort.
* The user always knows what to do next.
* Visual consistency matches the rest of the application.
* Accessibility requirements are satisfied.
* Performance remains high.

Good design should reduce cognitive load rather than increase it.

---

# Related Documents

This document defines **how the application should look and feel**.

It complements:

* Vision
* Requirements
* Architecture
* CodingStandards

All UI and UX decisions should align with the principles described in this guide.