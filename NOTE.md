## What I picked
Optimizing the Product Detail Page (PDP) page speed and Largest Contentful Paint (LCP) by fixing the lazy-loading behavior on the primary featured product image.

## Why it's the highest-impact thing here
The featured product image is the most crucial asset loaded above the fold. The original code set `fetchpriority="high"` but inadvertently forced a global `loading="lazy"` attribute onto the main image from the parent loop framework. This tells the browser to delay loading the most critical item on the screen, heavily damaging the page's mobile technical performance and LCP score. Fixes like this directly protect store conversion rates.

## What I did
Inspected the code architecture down to `snippets/product-media.liquid`. I modified the initialization block where `is_main_product_media` is validated. By injecting a conditional override (`assign loading = 'eager'`) immediately alongside the existing `fetch_priority = 'high'` assignment, I structurally prevented the parent component from passing down `lazy` instructions to the primary hero canvas.

## What I'd do next
I would write a dynamic preload hook into the global theme layout header to preload the primary hero image URL selectively on incoming PDP router strings, completely eliminating asset discovery delays.
