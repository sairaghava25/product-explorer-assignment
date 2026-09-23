# Notes

> Fill this in as you work. This document is assessed alongside your code.

## Bugs I found

For each: what was wrong, **why** it was wrong, and how I fixed it.



1 .Repeated API requests in useProducts

What was wrong: The useEffect depended on products, while the effect itself updates products.

Why it was wrong: Updating products caused the effect to run again, which triggered another API request and could lead to repeated fetching.

How I fixed it: Changed the effect dependency array to [] so the products are fetched once when the component mounts. I also changed the product state and API response types to use the Product interface instead of any.

2 .Search and category filtering did not work together

What was wrong: Search was only applied when the category was set to "all". Also, the search comparison was case-sensitive.

Why it was wrong: Selecting a category bypassed the search condition, and users searching with different capitalization could get unexpected results.

How I fixed it: Created separate matchesSearch and matchesCategory conditions and required both to be true. Converted both the product title and search text to lowercase before comparing them.

3.Product grid used array indexes as React keys

What was wrong: Products were rendered with key={index}.

Why it was wrong: Array indexes are not stable identifiers when a filtered list changes, which can cause React to associate the wrong component instance with a product.

How I fixed it: Changed the key to the product's stable unique ID: key={product.id}.

4 .Error state was not displayed

What was wrong: The useProducts hook exposed an error value, but the page did not render it.

Why it was wrong: If the API request failed, the user would not receive useful feedback about what happened.

How I fixed it: Added a visible error message when error is present and prevented the product grid from rendering while the app is in an error state.

5.Product modal opened and closed without animation

What was wrong: The modal appeared and disappeared immediately.

Why it was wrong: The assignment requires a meaningful Framer Motion transition for the modal.

How I fixed it: Added AnimatePresence and motion components from Framer Motion. The backdrop fades in/out while the modal scales and moves into position.

6 .TypeScript any usage in product fetching

What was wrong: The products state and API response were typed as any.

Why it was wrong: any removes TypeScript's type checking and violates the assignment requirement to avoid any.

How I fixed it: Used the existing Product interface for the product state and typed the API response as Product[].


## Features I completed

-Responsive product grid using Tailwind CSS with 1 column on mobile, 2 columns on small screens, and 3 columns on large screens.
-Case-insensitive product title search.
-Category filtering combined with search.
-product details modal when a product card is selected.
-Framer Motion animation for product cards and the product modal.
-Loading state while products are being fetched.
-Error state when product loading fails.
-Empty state when no products match the selected filters.
-TypeScript type safety without using any. 

## Decisions

Anywhere I had to choose between options — and why I chose what I did.

-Kept the existing Product interface and reused it throughout the application instead of creating duplicate product types.
-Used the product ID as the React key because it is a stable identifier for each product.
-Used AnimatePresence for the modal so the exit animation can run when the selected product becomes null.
-Kept the existing Tailwind responsive grid approach because it satisfies the assignment requirements without adding another UI library.
-Kept the existing Framer Motion product-card animation and added the required modal animation rather than replacing working functionality.

## With more time

What I'd improve or add next.

-Add a retry action for failed API requests.
-Improve accessibility with keyboard focus management and closing the modal with the Escape key.
-Replace the native image elements with Next.js Image after configuring the external image domain.
-Add automated tests for filtering, loading, error handling, and modal behavior.
-Consider adding pagination or sorting if the product catalogue becomes larger.
