# NextJS Summary

## Best practices

- Reusability
- Functional components and hooks
- Small components
- Correct use of props, state, context and stores
- Good error handling
- Fallback
- Caching

## Performance Optimizations

- Use react compiler or `useMemo`, `useCallback`
- Keep local state minimal
- Image optimization

## CSS

- CSS modules are isolated for each component `home.module.css`

## Images

- Preventing layout shift automatically when images are loading. (available in html)
- Resizing images to avoid shipping large images to devices with a smaller viewport (available in html)
- Lazy loading images by default (available in html)
- Serving images in modern formats, like WebP and AVIF (NOT available in html)
- Do not get the image if it's hidden ( this is not a feature of next/image but when loading ="lazy" is enabled, this is the default behaviour )

## Links

- In production, links will be automatically prefetched when scrolled ( Production only )

## Partial Rendering

- In a case where `/blogs/[slug]`, and user switches between `/blogs/one` and `/blogs/two`
  only the content in slug will be replaced and common layout will be preserved

# Caching

- Request Memoization (React feature)
  - Only applies to `GET` requests
- Data Cache
- Full Route Cache

## Client-side Router Cache

- Layouts are cached and reused on navigation (Partial rendering)
- Loading states are cached and reused on navigation for instant navigation.
- Pages are not cached by default, but are reused during browser backward and forward navigation. You can enable caching for page segments by using the experimental staleTimes config option

## What is Streaming?

- First, all data for a given page is fetched on the server.
- The server then renders the HTML for the page.
- The HTML, CSS, and JavaScript for the page are sent to the client.
- A non-interactive user interface is shown using the generated HTML, and CSS.
- Finally, React hydrates the user interface to make it interactive.

## Hydration

To hydrate your app, React will “attach” your components’ logic to the initial generated HTML from the server. Hydration turns the initial HTML snapshot from the server into a fully interactive app that runs in the browser.

```js
hydrateRoot(document.getElementById("root"), <App />);
```

## invalidate the Router Cache

- on Server `revalidatePath`
- on Client `router.refresh`

## Server Rendering Strategies

- Static Rendering
- Dynamic Rendering
- Streaming

### Advantages of Server Rendering

- Faster data fetching - usually server is closer to the data source
- Cross user cache - by rendering on the server, the result can be cached and reused on subsequent requests and across users
- Performance by less javascript - Moving non-interactive pieces of your UI to Server Components can reduce the amount of client-side JavaScript needed
- Initial Page Load and First Contentful Paint (FCP)
- Search Engine Optimization and Social Network Shareability
- Streaming: Server Components allow you to split the rendering work into chunks and stream them to the client as they become ready

### Server component rendering steps

- React renders Server Components into a special data format called the React Server Component Payload (RSC Payload).
- Next.js uses the RSC Payload and Client Component JavaScript instructions to render HTML on the server.
- The HTML is used to immediately show a fast non-interactive preview of the route - this is for the initial page load only.
- The HTML is used to immediately show a fast non-interactive preview of the route - this is for the initial page load only.
- The JavaScript instructions are used to hydrate
  Client Components and make the application interactive.

> [!NOTE]
> In Next.js, you can have dynamically rendered routes that have both cached and uncached data.
> This is because the RSC Payload and data are cached separately. This allows you to opt into
> dynamic rendering without worrying about the performance impact of fetching all the data at request time.

## Static Rendering

Component will only be statically rendered at compile time only if all following conditions are met

- No dynamic APIs are used within the server component
  - cookies
  - headers
  - connection
  - draftMode
  - searchParams prop
  - unstable_noStore
- No fetch call are made with `no-store`

30 min theory ( optimized, eye contact )

- Next JS / React ( Clock )
- Graph QL (appolo client, type generation)
- Netlify
- AWS / Kubernetes
- NextJS, Multizone, Microfront
- Java Spring Boot
- BFF (backend for frontend)
- Server less, monolith

1h of live coding

- Some Implementation
- Clock

# TODO

https://developer.mozilla.org/en-US/docs/Web/HTTP/Conditional_requests

https://nextjs.org/docs/app/building-your-application/data-fetching/incremental-static-regeneration

# Kubernetes

Kubernetes, also known as K8s, is an open source system for automating deployment, scaling, and management of containerized applications.
