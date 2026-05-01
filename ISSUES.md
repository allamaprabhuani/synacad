# SynaCAD site — issues & TODO (audit 2026-05-01)

---

## P0 — Credibility

- [ ] **`github.com/allamaprabhuani/synacad` is linked twice (header CTA, hero, footer) but no public repo exists at that path** that demonstrates the tool. Either:
  - (a) push a placeholder repo with a README that states "private until v0.1, sign up here for notify", OR
  - (b) point the CTA at the contact email (`mailto:`) until the code is ready.
  - Right now a curious reviewer (OSV, journalist, recruiter) clicks "Code on GitHub" and lands on a 404 or an empty repo. That actively hurts the pitch.
- [ ] **"cites the textbook page or the standard it came from"** — User feedback on the OSV pitch was *"an agent that cites the textbook for every number is unnecessary."* Soften this rule on the site too, or scope it to the **engineering report**, not every conversational turn.
- [ ] **"Every dimension, tolerance, and material call is computed by a validated solver"** — a strong claim made on a site for a tool that isn't shipping yet. Add a small "(planned)" or "(in development)" qualifier somewhere in the §moat block, or move the moat text under a "How it will work" heading. Reviewers can spot vapourware claims, and you don't need them to.
- [ ] **"At work" example: 6 mm aluminium bracket, 30 kg load** — confirm the math (a 6 mm-thick 6061-T6 L-bracket holding 30 kg is well within capacity for any reasonable geometry, but if a stress engineer eyeballs the lede they'll do back-of-envelope on it). Not strictly an error, but be ready to defend it.

## P0 — Bugs

- [ ] **Google Fonts loaded but Newsreader (italic) and Inter weights 400/500/600/700 may not all render.** Confirm in DevTools that all four Inter weights are actually used; otherwise drop the unused ones to shave ~30 KB.
- [ ] **`<a href="#">` on the brand link** — clicking it scrolls to top, which is fine, but `#` is technically a no-op anchor and screen readers may announce it oddly. Use `href="/"` or `href="#top"`.
- [ ] **`vision-fab` floating link** — confirm it doesn't overlap the chat / cookie / accessibility widgets that some browsers inject. On mobile, confirm it doesn't sit over the iOS bottom-bar gesture area.

## P1 — Accessibility

- [ ] **Hero animation SVG** — `aria-hidden="true"` is set, good. But it's a 360x320 fixed-size SVG; on phones <360 px wide it'll overflow horizontally if the parent isn't `width: 100%; max-width: …`. Verify in style.css.
- [ ] **`<a class="display-link">` with a tooltip span** — the tooltip is decorative; screen readers will read the entire SynaCAD heading + tooltip text together. Move the tooltip to a `title=""` attribute or hide it from a11y tree.
- [ ] **Colour contrast** — the `accent` colour `#b4471a` on a light background is fine, but on the dark-mode body (if any) the dot indicators may fall below WCAG AA. No dark mode visible in the SynaCAD CSS — confirm one isn't auto-applied via system preference.
- [ ] **Focus styles** — the `cta-mini` and `btn` should have a visible focus ring for keyboard users. Audit in style.css.

## P1 — Content / consistency

- [ ] **"Bound by the rules of mechanics" appears 3 times** (title tag, hero, §moat). Differentiate the wording or the repetition will read as a tic.
- [ ] **"Validated solver" claim repeated 3 times** (lede, §moat first bullet, footer-adjacent emit-card). Once is strong; thrice is suspicious.
- [ ] **Roadmap M10–12 example: "kitchen-chair clip rebuilt from a photo, a stress bracket, a fatigue lug, and a pressure-vessel section"** — pressure vessels involve ASME BPVC, not Bruhn/Niu/ESDU. Either drop the pressure-vessel example or add ASME BPVC to the Built-On list.
- [ ] **"ASME Y14.5-compliant" and "Bruhn, Niu, ESDU, Lekhnitskii"** — these are aerospace standards. Bracket-and-clip examples lean light-mech / consumer. Consider either dropping the aerospace standard names from the home page (and putting them in a /standards page) or adding 1-2 examples that justify Bruhn (e.g., a wing-skin coupon, a riveted joint).
- [ ] **"At home" copy in §moat** says "An STL or 3MF file ready for any 3D printer, plus a short note on how strong the part will be and what it can take." That's two outputs; consider listing the analysis note explicitly as a deliverable.

## P1 — SEO / metadata

- [ ] **No JSON-LD on synacad index.** Add a `SoftwareApplication` schema block with `name`, `description`, `applicationCategory: EngineeringApplication`, `creator: { name: "Allamaprabhu Ani", url: "https://allamaprabhuani.github.io" }`, `license: "MIT"`. This is what makes Google show "by Allamaprabhu Ani · open source" in the SERP snippet.
- [ ] **No `<link rel="canonical">`** — set to `https://allamaprabhuani.github.io/synacad/`.
- [ ] **No `og:image`** — add a SynaCAD wordmark or hero render (1200×630 PNG) so LinkedIn / Twitter / iMessage previews look polished. Critical for OSV pitch — the moment a reviewer pastes this in Slack, the preview card sells you.
- [ ] **No `twitter:card` meta** — add `summary_large_image` for X/Twitter previews.
- [ ] **No `<meta name="author">`**.

## P2 — Performance

- [ ] **Two Google Fonts requests** — Inter (4 weights) + Newsreader (regular + italic). ~80 KB total. Acceptable, but consider self-hosting via woff2 (you already do this on the parent site) so the SynaCAD page renders identically when fonts.googleapis.com is blocked (corporate firewalls, China, EU privacy filters).
- [ ] **No font-display in the link rel="stylesheet" call.** Add `&display=swap` (already there) — confirm not blocked by a CSP.
- [ ] **No favicon set on synacad** — inherits / nothing? Confirm. Add `<link rel="icon" href="/favicon.png">` consistent with parent site.

## P2 — UX

- [ ] **"Get notified" mailto** — use a Tally / Formspark / Google Form for actual email collection. mailto:s don't work on locked-down corporate Macs and discard everyone who doesn't have a mail client configured.
- [ ] **No analytics**. If you want to measure OSV-driven traffic, drop in [Plausible](https://plausible.io) or [Simple Analytics](https://simpleanalytics.com). GoatCounter is free.
- [ ] **No "share" button or copy-link** for visitors who want to forward the page.

## P3 — Nice-to-haves

- [ ] **Add a one-line status update** at the top: *"Last updated: 2026-05-01 · Currently building the intake layer (M1-3)."* Shows momentum; reviewers love it.
- [ ] **Embed a 30-s explainer video** when you record one for OSV. Same asset, two uses.
- [ ] **Consider a small `<pre>` block** showing what an actual SynaCAD prompt-and-response looks like — even a mocked one would make the pitch concrete.
- [ ] **Add a "/manifesto" redirect** that points to the blog vision post, so people can quote `synacad.dev/manifesto` (or your custom domain equivalent) in talks.
