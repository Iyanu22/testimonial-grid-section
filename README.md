# Frontend Mentor - Testimonials grid section solution

This is a solution to the [Testimonials grid section challenge on Frontend Mentor](https://www.frontendmentor.io/challenges/testimonials-grid-section-Nnw6J7Un7). Frontend Mentor challenges help you improve your coding skills by building realistic projects.

## Table of contents

- [Overview](#overview)
  - [The challenge](#the-challenge)
  - [Progress](#progress)
  - [Screenshot](#screenshot)
  - [Links](#links)
- [My process](#my-process)
  - [Built with](#built-with)
  - [What I learned](#what-i-learned)
  - [Challenges](#challenges)
  - [Continued development](#continued-development)
  - [AI Collaboration](#ai-collaboration)
- [Author](#author)

## Overview

### The challenge

Users should be able to:

- View the optimal layout for the site depending on their device's screen size

### Progress

This solution is a work in progress.

- [x] HTML structure for all five testimonial cards
- [x] SCSS colour palette set up as variables
- [x] Mobile layout: single column of cards using Flexbox
- [ ] Heading and description spacing matched to the design
- [ ] Barlow Semi Condensed font loaded and typography matched
- [ ] Card colours and text opacity matched to the design
- [ ] Desktop layout using CSS Grid
- [ ] Accessibility clean-up (heading hierarchy, alt text)
- [ ] Decorative quote mark on the purple card (desktop)

### Screenshot

![](./design/testimonial_section(2).png)

### Links

- Solution URL: [Add solution URL here](https://your-solution-url.com)
- Live Site URL: [Add live site URL here](https://your-live-site-url.com)

## My process

### Built with

- HTML5 markup
- SCSS (Sass) with variables for the colour palette
- Flexbox (mobile layout)
- CSS Grid with `grid-template-areas` (desktop layout)
- Mobile-first workflow
- [Barlow Semi Condensed](https://fonts.google.com/specimen/Barlow+Semi+Condensed) via Google Fonts

### What I learned

**A universal reset means nothing has spacing until you give it some.**
I started with `* { margin: 0; padding: 0; }`. That's a good baseline, but it means headings and paragraphs sit flush against each other unless a rule targets them. I spent time debugging "margin not working" before realising I had never written a rule for the heading or the description in the first place.

```scss
h1 {
  margin-bottom: 1rem; // space between the heading and the description
}
```

Bottom margin on the upper element is the right tool for spacing between siblings. Padding would enlarge the heading's own box instead.

**SCSS nesting has to mirror the real HTML.**
I had a rule nested as `.author { .details { ... } }`, but in my markup `.details` *wraps* `.author`. It's not inside it. The rule matched nothing and did nothing, and nothing warned me. Comparing the compiled CSS selector against the HTML structure, or checking devtools, catches this quickly.

**CSS Grid with named areas.**
The desktop design has two cards that span two columns and one that spans two rows. A 4-column grid with `grid-template-areas` lets me draw that layout directly in the CSS:

```scss
.container {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-template-areas:
    "first  first  second fifth"
    "third  fourth fourth fifth";
  gap: 2rem;
}

.first-column { grid-area: first; }
```

What I took from this:

- `1fr` means "one share of the leftover space", so four of them make four equal columns.
- The same name in neighbouring cells makes that area stretch across them.
- Every row in the map must have the same number of entries.
- Areas must form solid rectangles.
- A `.` in the map marks a deliberately empty cell.

**Using `opacity` for dimmed text on dark cards.**
White text with `opacity: 0.5` or `0.7` gives the softer secondary text from the design without inventing extra colours. On the white cards it would just wash out the grey, so those get explicit colours instead.

### Challenges

1. **Heading margin not applying.** Root cause: no rule targeted the heading or description, combined with the universal reset.
2. **A dead SCSS rule.** The nested `.details` selector didn't match my HTML structure, so it silently did nothing.
3. **Wrong font.** The serif text in my first screenshot was the browser default, because the design's font wasn't loaded.
4. **Colour mismatches.** I used `$grey-400` for the second card where the design uses the darker `$grey-500`, and I had the same colour on both the heading and description of the white cards.
5. **Understanding the desktop grid.** I had never used `grid-template-areas`, so I had to learn the mental model first: an invisible table, with cards assigned to cells.
6. **Markup issues found in review.** An unclosed `.container` div, five `<h1>` elements on one page, and a copy-pasted `alt` attribute on one avatar.

### Continued development

- Use one `<h1>` per page and make the testimonial headings `<h2>`.
- Rename `.first-column`, `.second-column` etc. to names that describe what the element is (for example `.card--purple`), since their position changes between mobile and desktop.
- Get into the habit of checking the Styles panel in devtools first when a rule "doesn't work", instead of rewriting CSS and hoping.
- Add the decorative quote mark on the purple card at desktop width.
- Test the layout at widths between mobile and desktop, not only at the two extremes.

### AI Collaboration

I used Claude (in the web chat) as a debugging partner and tutor.

- **How I used it:** I shared the design images, my SCSS, my screenshot and my HTML, and asked it to find why my spacing wasn't working. I then asked follow-up questions to understand CSS Grid from scratch.
- **What worked well:** Comparing my screenshot against the design turned up several differences I hadn't noticed (font, colours, missing desktop layout). Asking it to explain *why* things worked, not just to give me code, helped the grid concepts stick.
- **What didn't:** Its first diagnosis of the `.details` issue was partly wrong. It guessed at a specificity conflict before it had seen my HTML, and only corrected itself once I shared the markup. Lesson: give the AI the full context up front (HTML and CSS together), and verify its explanation in devtools before trusting it.

## Author

- Website - [https://your-live-site-url.com]
- Frontend Mentor - [@Iyanu22](https://www.frontendmentor.io/profile/Iyanu22)