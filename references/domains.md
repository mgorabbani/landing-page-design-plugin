# Domain recipes

Twelve recipes, each with the same shape. Treat these as starting points — adapt to what the user actually told you.

Each recipe has:

- **Visitor need** — the feel/know/do for the typical visitor
- **Critical CTA** — the one conversion that matters
- **Section flow** — ordered section list, with count range
- **Aesthetic defaults** — palette hint, typography, motion intensity
- **Component picks** — concrete shortlist per section (registry-qualified)
- **Assets** — icons, illustrations, photos, patterns
- **llms.txt focus** — what to emphasize for crawlers

Registry shorthand: `@shadcn` (default), `@magicui`, `@aceternity`, `@kibo-ui`, `@skiper-ui`, Launch UI (whole-registry init).

---

## 1. Medical / health practice

**Visitor need** — Feel trust and calm. Know the practitioner, services, insurance. Do: book an appointment.

**Critical CTA** — Book appointment (phone, online form, or scheduler link).

**Section flow (4–6 sections)** —
1. Hero (practitioner name, specialty, one-line promise, book button)
2. Services (3–6 services with short descriptions)
3. About / credentials (photo, bio, training, affiliations)
4. Testimonials / reviews
5. Insurance & logistics (accepted insurance, hours, location, parking)
6. Booking CTA (scheduler embed or contact form)

**Aesthetic** — Soft, warm, clinical-but-human. Off-white background, muted blue/teal/sage primary, warm off-black text. Display font: a calm serif (Fraunces, Source Serif, Cormorant) or editorial sans (DM Sans, Plus Jakarta). Body: Inter or Geist. Low motion.

**Component picks** —
- Hero: `@aceternity/spotlight` or `@aceternity/lamp` (subtle) + shadcn Button
- Services: shadcn Card grid OR `@kibo-ui/feature`
- About: split layout (image + bio), shadcn Avatar
- Testimonials: `@magicui/marquee` (slow) or `@kibo-ui/testimonial`
- Booking: shadcn Form + Calendly/scheduler iframe

**Assets** — Lucide (stethoscope, heart, shield, calendar). Real portraits (provided by user, or tastefully staged Unsplash — but flag if using stock). No cartoon illustrations.

**llms.txt focus** — Practitioner name, specialty, location, insurance accepted, booking URL, hours.

---

## 2. SaaS / dev tools

**Visitor need** — Understand the product in 5 seconds. See proof it works. Try it without friction.

**Critical CTA** — Start free trial / Sign up free / Get started.

**Section flow (6–9 sections)** —
1. Hero (tagline, sub, primary + secondary CTA, product shot or animation)
2. Social proof (logo row of customers)
3. Features (bento or alternating splits — 3–6 features)
4. Demo / interactive preview
5. Metrics or outcomes
6. Testimonials
7. Pricing
8. FAQ
9. Footer CTA

**Aesthetic** — Clean, confident, technical. Dark mode often works. Primary = brand hue, accent = subtle neon or graph-line. Display: Geist / Inter Display / Satoshi. Body: Inter / Geist. Medium motion — animated beams, number tickers, subtle gradients are appropriate.

**Component picks** —
- Hero: `@aceternity/hero-parallax` or Launch UI Hero + `@magicui/border-beam` on product card
- Logos: `@magicui/marquee` with customer logos from Simple Icons
- Features: Launch UI Bento or `@aceternity/bento-grid`
- Demo: `@aceternity/macbook-scroll` or `@aceternity/container-scroll`
- Metrics: `@magicui/number-ticker` in a stat row
- Testimonials: `@kibo-ui/testimonial` or `@magicui/marquee`
- Pricing: Launch UI Pricing or `@kibo-ui/pricing`
- FAQ: shadcn Accordion or `@kibo-ui/faq`

**Assets** — Lucide + Simple Icons (for customer logos). Product screenshots. Abstract patterns from Hero Patterns or SVG Backgrounds for section dividers.

**llms.txt focus** — Product name, one-line description, key capabilities, pricing tiers, trial URL, docs URL.

---

## 3. Agency / studio

**Visitor need** — See evidence of taste and skill. Understand services. Inquire easily.

**Critical CTA** — Start a project / Book a call / Get in touch.

**Section flow (5–7 sections)** —
1. Hero (editorial, opinionated — often type-driven, not image-driven)
2. Selected work (case study grid or scroll-reveal gallery)
3. Services (short, confident)
4. About / team
5. Awards / press (optional)
6. Contact CTA (big, unambiguous)

**Aesthetic** — Editorial, confident, often monochromatic with one accent. Display: editorial serif (Playfair, Fraunces) or bold sans (PP Neue Montreal feel — use Geist Mono or Space Grotesk). Body: Inter / Neue Haas clone. High taste, selective motion — one signature moment.

**Component picks** —
- Hero: Custom type-driven composition + `@skiper-ui/*` signature effect
- Work: `@aceternity/hero-parallax`, `@aceternity/sticky-scroll-reveal`, or `@magicui/bento-grid`
- Services: Launch UI Feature or shadcn Tabs
- Team: `@kibo-ui/team`
- Contact: shadcn Form with big type

**Assets** — Real work thumbnails (provided). Minimal icons — Tabler or Phosphor at most. Avoid generic illustrations.

**llms.txt focus** — Studio name, positioning, services, recent clients, contact.

---

## 4. E-commerce / product

**Visitor need** — Browse products. Trust the brand. Buy without friction.

**Critical CTA** — Shop now / Add to cart.

**Section flow (5–8 sections)** —
1. Hero (product-led — big hero image or lifestyle shot + featured CTA)
2. Featured products / collections
3. Brand story
4. Social proof (reviews, UGC, press)
5. Category grid
6. Newsletter / loyalty
7. Footer (policies, shipping, contact)

**Aesthetic** — Product-forward, photography-heavy, restrained type. Let the product breathe — generous whitespace, big images. Display: brand-matched (luxury = serif like Didot feel; streetwear = bold sans; wellness = soft serif). Body: clean sans.

**Component picks** —
- Hero: Custom image hero + shadcn Button
- Products: shadcn Card grid customized or Launch UI Feature
- Reviews: `@kibo-ui/testimonial` or `@magicui/marquee`
- Newsletter: shadcn Form (inline)
- Cart / checkout: shadcn Dialog + Sheet

**Assets** — Real product photography (provided). Phosphor or Lucide for icons. Hero Patterns for subtle section dividers.

**llms.txt focus** — Brand name, product categories, key products, shipping info, return policy.

---

## 5. Personal portfolio

**Visitor need** — Understand who you are, see your work, know if you're available.

**Critical CTA** — Hire me / Contact / Download CV.

**Section flow (4–6 sections, multi-page common)** —
1. Hero (name, role, one-line)
2. Selected projects
3. About
4. Writing / blog (optional)
5. Contact

**Aesthetic** — Editorial, personal, restrained. Often dark mode with one accent color, or warm off-white. Display: editorial serif or distinctive sans. Body: readable. Selective motion.

**Component picks** —
- Hero: `@aceternity/spotlight` or a custom type hero
- Projects: `@aceternity/sticky-scroll-reveal` or `@magicui/bento-grid`
- Writing: shadcn Card list
- Contact: shadcn Form or mailto button

**Assets** — Own photos. Minimal icons. Illustrations only if they fit the personal brand.

**llms.txt focus** — Name, role, specialties, selected projects, contact, availability.

---

## 6. Restaurant / hospitality

**Visitor need** — See the vibe, scan the menu, reserve a table or find the place.

**Critical CTA** — Reserve / Book a table / View menu.

**Section flow (4–6 sections)** —
1. Hero (full-bleed image or video, restaurant name, reserve button)
2. Menu highlights
3. Story / chef
4. Gallery
5. Location & hours
6. Reservation CTA

**Aesthetic** — Photography-led, atmospheric. Warm palette — cream, oxblood, deep green, charcoal. Display: characterful serif (Cormorant, Fraunces) or editorial. Body: quiet sans. Low motion — let photography breathe.

**Component picks** —
- Hero: Full-bleed image + shadcn Button, optionally `@aceternity/background-beams` subtle
- Menu: shadcn Tabs or simple columned layout
- Gallery: `@aceternity/hero-parallax` (slow) or simple masonry
- Reservation: shadcn Form + embed (Resy, OpenTable)

**Assets** — Real food / interior photography (provided). Minimal iconography.

**llms.txt focus** — Restaurant name, cuisine, location, hours, reservation URL, phone.

---

## 7. Creator / course

**Visitor need** — Feel the creator's authority and warmth. See outcomes. Enroll.

**Critical CTA** — Enroll / Join waitlist / Start learning.

**Section flow (6–9 sections)** —
1. Hero (personal, creator-forward)
2. Outcome promise
3. Testimonials (weighted heavily — this sells courses)
4. Curriculum preview
5. About the creator
6. Pricing / tiers
7. FAQ
8. Final CTA

**Aesthetic** — Warm, personable, slightly premium. Accent color that reflects the creator's brand. Display: friendly sans (Plus Jakarta, Inter Display) or warm serif. Medium motion.

**Component picks** —
- Hero: `@aceternity/spotlight` + creator portrait
- Testimonials: `@magicui/marquee` + `@kibo-ui/testimonial` cards
- Curriculum: shadcn Accordion or Launch UI Feature
- Pricing: Launch UI Pricing with clear tier differences
- FAQ: shadcn Accordion

**Assets** — Creator photos (provided). Warm illustrations from Blush or Humaaans if appropriate. Storyset for process diagrams.

**llms.txt focus** — Course / creator name, outcome promise, curriculum modules, enrollment URL, next cohort date.

---

## 8. Nonprofit

**Visitor need** — Understand the mission. Feel the impact. Donate or get involved.

**Critical CTA** — Donate (primary) + Get involved (secondary).

**Section flow (5–7 sections)** —
1. Hero (mission statement + donate button)
2. Impact numbers
3. Programs / initiatives
4. Stories (beneficiaries, case studies)
5. Team / board (optional)
6. Financial transparency
7. Donate CTA (sticky or repeated)

**Aesthetic** — Human, hopeful, credible. Warm palette often works; match cause (environmental = greens, health = blues/teals, education = warm). Display: approachable sans or warm serif. Low-to-medium motion.

**Component picks** —
- Hero: `@aceternity/spotlight` or simple image hero
- Impact: `@magicui/number-ticker` in a stat row
- Stories: `@kibo-ui/testimonial` or a custom card grid
- Donate: shadcn Form + Stripe / Donorbox embed

**Assets** — Real photography of work and beneficiaries (provided). unDraw for diagrams. Lucide for icons.

**llms.txt focus** — Nonprofit name, mission, programs, impact numbers, donate URL, EIN / registration.

---

## 9. Local service (plumber, lawyer, contractor, gym...)

**Visitor need** — Trust you're legit, see reviews, call / request a quote.

**Critical CTA** — Call now + Request a quote.

**Section flow (4–6 sections, usually single-page)** —
1. Hero (service name, city, phone, quote CTA)
2. Services list
3. Why choose us (licensed, insured, years of experience, reviews)
4. Reviews (Google / Yelp embedded or pulled)
5. Service area / coverage map
6. Contact CTA

**Aesthetic** — Trustworthy, local, unpretentious. Strong primary color (navy, deep green, burgundy). Display: solid sans (Archivo, Montserrat) or trustworthy serif. Minimal motion — trust matters more than flash.

**Component picks** —
- Hero: simple image or pattern hero + big phone CTA
- Services: shadcn Card grid
- Reviews: `@kibo-ui/testimonial` or `@magicui/marquee`
- Contact: shadcn Form + click-to-call button

**Assets** — Real photos of work / team. Lucide icons. No illustrations.

**llms.txt focus** — Business name, service categories, service area, phone, license numbers, hours.

---

## 10. Crypto / DeFi

**Visitor need** — Understand the protocol, see credibility signals (TVL, audits), connect wallet.

**Critical CTA** — Connect wallet / Launch app.

**Section flow (6–9 sections)** —
1. Hero (bold, often 3D or animated)
2. Stats (TVL, volume, users — live)
3. How it works
4. Features
5. Audits & security
6. Tokenomics (if applicable)
7. Ecosystem / partners
8. Docs / community CTA

**Aesthetic** — Dark mode default. Neon accents (cyan, violet, electric green). Display: technical sans (Geist, JetBrains, Space Grotesk). High motion — meteors, globes, animated beams are on-brand here.

**Component picks** —
- Hero: `@aceternity/globe` + `@magicui/meteors` + `@magicui/border-beam` + shadcn Button
- Stats: `@magicui/number-ticker` row
- How it works: `@magicui/animated-beam`
- Features: `@aceternity/bento-grid`
- Audits: logo row (Simple Icons / provided)

**Assets** — 3DIcons, Shapefest for 3D crypto abstract. Simple Icons for partner logos. Grid / dot patterns from Hero Patterns.

**llms.txt focus** — Protocol name, chain, category (DEX, lending, etc.), TVL, audits, app URL, docs URL.

---

## 11. AI product

**Visitor need** — See the product doing real work. Understand the model / capability. Try it.

**Critical CTA** — Try it / Join waitlist / Start free.

**Section flow (5–8 sections)** —
1. Hero (tagline + live demo or video)
2. Social proof (backers, customers)
3. Capabilities (what it can do)
4. Demo / use cases
5. Metrics or benchmarks
6. Pricing or waitlist
7. FAQ
8. CTA

**Aesthetic** — Clean, confident, futuristic. Often dark with gradient accents, or clean light with subtle color. Display: Geist / Inter Display. Medium-to-high motion — one signature animation (animated beam, orbit).

**Component picks** —
- Hero: `@aceternity/spotlight` or `@aceternity/background-beams` + shadcn Button + live demo input
- Capabilities: `@aceternity/bento-grid` with animated illustrations
- Demo: embedded iframe or inline component
- Animated beam: `@magicui/animated-beam` for "data flows" diagrams
- Orbit: `@magicui/orbiting-circles` for "integrations" display

**Assets** — Abstract 3D from Shapefest. Lucide + Simple Icons. Hero Patterns.

**llms.txt focus** — Product name, what it does, capabilities, pricing / access URL, docs URL.

---

## 12. Real estate

**Visitor need** — See listings, feel the location, schedule a viewing.

**Critical CTA** — Schedule a viewing / Contact agent.

**Section flow (5–7 sections)** —
1. Hero (full-bleed property image or video)
2. Featured listings
3. Neighborhood / location
4. About the agent / team
5. Testimonials
6. Contact CTA

**Aesthetic** — Photography-driven, premium, quiet type. Neutral palette with one accent — navy / burgundy / forest. Display: editorial serif (Playfair, Fraunces) or premium sans. Low motion.

**Component picks** —
- Hero: Full-bleed image + minimal type overlay + shadcn Button
- Listings: `@aceternity/hero-parallax` or shadcn Card grid with big images
- Neighborhood: map embed + `@kibo-ui/feature` highlights
- Agent: split layout image + bio
- Contact: shadcn Form

**Assets** — Real property photography (provided). Minimal icons (Lucide). No illustrations.

**llms.txt focus** — Agency / agent name, service area, listing count, contact, schedule URL.

---

## Other / unlisted domain

If the user's domain doesn't match any above, work through this framework explicitly:

1. Identify the single most important action for a typical visitor (the critical CTA).
2. List 3 things the visitor needs to believe or understand before they do that action.
3. Map each of those to one section.
4. Add a hero on top and a final CTA on the bottom.
5. Pick the closest-matching recipe above as an aesthetic anchor, then deviate based on what makes this domain distinctive.

Never invent a recipe from scratch when you can anchor to a closer-fit one.
