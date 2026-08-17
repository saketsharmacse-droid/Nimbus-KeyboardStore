# Nimbus Keyboard Store

A mechanical keyboard e-commerce site with an interactive 3D product viewer, built to feel closer to the polished, animation-heavy sites you see on Awwwards than a typical storefront template. Users can rotate and inspect keyboard models in 3D before buying, browse a CMS-driven product catalog, and check out with Stripe.

What started as a "quick weekend build" turned into about three nights of barely sleeping. Somewhere around night two I stopped pretending I was going to bed early, and just accepted I'd be debugging shader-adjacent nonsense at 2 AM, this projct took a lot of debugging and late night sessions of commitment.

## What it does

- Interactive 3D keyboard models you can rotate and zoom into on the product pages
- A product catalog and marketing content managed through a headless CMS instead of being hardcoded
- Scroll-triggered and micro-interaction animations across the site (hero sections, transitions, hover states)
- A full checkout flow wired up with Stripe
- Responsive layout that holds up across screen sizes, including the 3D viewer, which was its own separate fight

## The tech

- **Next.js 15** (App Router, Turbopack) — framework and rendering
- **React 19**
- **Tailwind CSS 4** for styling
- **Prismic** as a headless CMS, so content isn't hardcoded into the pages
- **Three.js + React Three Fiber + Drei** for the interactive 3D keyboard viewer
- **GSAP** for animations and scroll-based motion
- **Radix UI** for accessible modal/dialog primitives
- **Stripe** for checkout

I picked this stack mostly because I wanted the CMS and the 3D piece specifically — I didn't want to hardcode product data, and I wanted the product viewer to feel like an actual feature instead of a static image gallery.

## Problems I ran into

- **The 3D viewer was the biggest headache, by far.** Getting the keyboard model to load, scale, and rotate correctly across screen sizes took a lot of trial and error. Thinking in terms of a scene graph instead of regular DOM took a while to click, and camera positioning that looked fine on my laptop looked broken on a smaller viewport, so I had to redo a chunk of that logic to be responsive.
- **GSAP timing fights.** Getting animations to feel smooth instead of janky, especially once they had to sync with scroll position, meant a lot of refreshing the page and squinting at timelines. A few animations that looked great in isolation looked completely off once stacked with everything else running on the page.
- **Prismic's content modeling** was new to me — figuring out how slices and custom types are supposed to work, instead of just hardcoding everything like I normally would, took some getting used to. I rebuilt a couple of the content models after realizing my first pass didn't scale to how the components actually needed the data shaped.
- **Tailwind v4's config changes** tripped me up more than once, since a lot of the docs and tutorials online are still written for v3 and the setup steps don't quite match anymore.
- **Random hydration errors** that only showed up in production builds and not in dev — one of those bugs where the fix ends up being a single line, but finding that line eats an entire evening.
- Performance was a real concern once the 3D model, GSAP animations, and Prismic content were all loading on the same page — had to be deliberate about lazy-loading and not rendering the 3D scene until it was actually needed.

None of it was dramatic on its own — just the usual "why is this not working" loop that ends with you finding one line you misread three hours ago. But stacked together over a few days, it added up to a lot more debugging than I expected going in.

## License

MIT — feel free to poke around or learn from it.

---

Saket Sharma

saket.sharma.cse@gmail.com
