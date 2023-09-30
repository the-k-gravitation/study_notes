#nextjs #route
## 基于 app 文件夹的路由规则：

默认下，在 *app* 下的 **components** 为 **React Server Components** .
Next.js uses a file-system based router: 
- Folders are used to define routes. 
- 文件夹下面的 "page.js" 文件为 默认的 Route File.

File 名约定： 

|File名|说明|
|---|---|
|[`layout`](https://nextjs.org/docs/app/building-your-application/routing/pages-and-layouts#layouts)|Shared UI for a segment and its children|
|[`page`](https://nextjs.org/docs/app/building-your-application/routing/pages-and-layouts#pages)|Unique UI of a route and make routes publicly accessible|
|[`loading`](https://nextjs.org/docs/app/building-your-application/routing/loading-ui-and-streaming)|Loading UI for a segment and its children|
|[`not-found`](https://nextjs.org/docs/app/api-reference/file-conventions/not-found)|Not found UI for a segment and its children|
|[`error`](https://nextjs.org/docs/app/building-your-application/routing/error-handling)|Error UI for a segment and its children|
|[`global-error`](https://nextjs.org/docs/app/building-your-application/routing/error-handling)|Global Error UI|
|[`route`](https://nextjs.org/docs/app/building-your-application/routing/route-handlers)|Server-side API endpoint|
|[`template`](https://nextjs.org/docs/app/building-your-application/routing/pages-and-layouts#templates)|Specialized re-rendered Layout UI|
|[`default`](https://nextjs.org/docs/app/api-reference/file-conventions/default)|Fallback UI for [Parallel Routes](https://nextjs.org/docs/app/building-your-application/routing/parallel-routes)| 

only the contents returned by `page.js` or `route.js` are publicly addressable。

