# Common Retail APIs

A curated list of publicly discoverable web APIs used by major U.S. beauty and department store retailers. Inspired by [public-apis/public-apis](https://github.com/public-apis/public-apis), this repository documents endpoints, request patterns, and headers needed to experiment with Macy's, Sephora, Ulta, and Nordstrom data.

## Contents

- [Macy's](#macys)
- [Sephora](#sephora)
- [Ulta](#ulta)
- [Nordstrom](#nordstrom)

### Macy's

| API | Base URL | Method | Example Query | Required Headers | Notes |
| --- | --- | --- | --- | --- | --- |
| Product Listing | `https://www.macys.com/xapi/discover/v1/catalog/category/{categoryId}` | `GET` | `?page=1&pageSize=40&sortBy=ORIGINAL&include=FACETS,PRODUCTS` | <details><summary>JSON</summary><code>{"Accept":"application/json, text/plain, */*","Content-Type":"application/json","Origin":"https://www.macys.com","Referer":"https://www.macys.com/shop/makeup","User-Agent":"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/124.0 Safari/537.36"}</code></details> | Replace `{categoryId}` with Macy's numeric ID from nav links (e.g. `46345`). Supports `sortBy`, `page`, `pageSize`, and `include` to control grids/facets. |
| Product Details | `https://www.macys.com/xapi/product/v3/pdp/{productId}` | `GET` | `?experience=pdp&include=AVAILABLE_SIZES,MEDIA,PRICES` | <details><summary>JSON</summary><code>{"Accept":"application/json, text/plain, */*","Content-Type":"application/json","Origin":"https://www.macys.com","Referer":"https://www.macys.com/shop/product?ID=5607075","User-Agent":"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/124.0 Safari/537.36"}</code></details> | `{productId}` aligns with the `ID` query param on PDP URLs. `include` toggles payload slices (images, price blocks, availability, etc.). |
| Product Search | `https://www.macys.com/xapi/discover/v1/catalog/search` | `GET` | `?searchphrase=lipstick&page=1&pageSize=40&sortBy=ORIGINAL` | <details><summary>JSON</summary><code>{"Accept":"application/json, text/plain, */*","Content-Type":"application/json","Origin":"https://www.macys.com","Referer":"https://www.macys.com/shop/featured/lipstick","User-Agent":"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/124.0 Safari/537.36"}</code></details> | Pagination controlled via `page`/`pageSize`. Browser-like `User-Agent` prevents 403 responses. |
| Product Reviews | `https://api.bazaarvoice.com/data/reviews.json` | `GET` | `?apiversion=5.5&passkey=<public-key>&displaycode=macys-en_us&filter=productid:eq:5607075&page=1&page_size=20&sort=submissiontime:desc` | <details><summary>JSON</summary><code>{"Accept":"application/json, text/plain, */*","Origin":"https://www.macys.com","Referer":"https://www.macys.com/shop/product?ID=5607075","User-Agent":"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/124.0 Safari/537.36"}</code></details> | Reviews powered by Bazaarvoice; harvest the `passkey`/`displaycode` from the `BV` script tag. Supports rich filters (photos/videos, rating ranges, locale). |

### Sephora

| API | Base URL | Method | Example Query | Required Headers | Notes |
| --- | --- | --- | --- | --- | --- |
| Product Listing | `https://www.sephora.com/api/catalog/categories/{categoryId}/products` | `GET` | `?currentPage=1&pageSize=60&sortBy=bestSelling` | <details><summary>JSON</summary><code>{"Accept":"application/json, text/plain, */*","Origin":"https://www.sephora.com","Referer":"https://www.sephora.com/shop/makeup","User-Agent":"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/124.0 Safari/537.36","X-Requested-With":"XMLHttpRequest"}</code></details> | Swap `{categoryId}` with Sephora's `catXXXXX` identifier (inspect nav links). Query params paginate/sort results. |
| Product Search | `https://www.sephora.com/api/catalog/search` | `GET` | `?keyword=lipstick&pageSize=60&currentPage=1` | <details><summary>JSON</summary><code>{"Accept":"application/json, text/plain, */*","Origin":"https://www.sephora.com","Referer":"https://www.sephora.com/search?keyword=lipstick","User-Agent":"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/124.0 Safari/537.36","X-Requested-With":"XMLHttpRequest"}</code></details> | `keyword` parameter required; pagination uses `currentPage` + `pageSize`. Keep origin/referer aligned with onsite search page. |
| Product Reviews | `https://api.bazaarvoice.com/data/reviews.json` | `GET` | `?apiversion=5.5&passkey=<public-key>&displaycode=sephora-en_us&filter=productid:eq:P379884&page=1&page_size=20&sort=submissiontime:desc` | <details><summary>JSON</summary><code>{"Accept":"application/json, text/plain, */*","Origin":"https://www.sephora.com","Referer":"https://www.sephora.com/product/rare-beauty?_sku=P379884","User-Agent":"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/124.0 Safari/537.36"}</code></details> | Bazaarvoice hosts Sephora's UGC. Grab `passkey`/`displaycode` from network tab (`Bazaarvoice.config`). Filters can include `rating` and `contentlocale`. |

### Ulta

| API | Base URL | Method | Example Query | Required Headers | Notes |
| --- | --- | --- | --- | --- | --- |
| Product Listing | `https://services.ulta.com/search/v2/search/category` | `GET` | `?categoryId=cat90004&page=1&pageSize=24&sortBy=bestSeller` | <details><summary>JSON</summary><code>{"Accept":"application/json, text/plain, */*","Origin":"https://www.ulta.com","Referer":"https://www.ulta.com/shop/makeup","User-Agent":"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/124.0 Safari/537.36","x-ulta-api-version":"2","x-ulta-platform":"web"}</code></details> | Same payload as onsite category grids; `categoryId` matches `cat#####` value in URL. `sortBy` accepts `topRated`, `priceLow`, etc. |
| Product Search | `https://services.ulta.com/search/v2/search/product` | `GET` | `?keyword=lipstick&page=1&pageSize=24&sortBy=bestSeller` | <details><summary>JSON</summary><code>{"Accept":"application/json, text/plain, */*","Origin":"https://www.ulta.com","Referer":"https://www.ulta.com/search?keyword=lipstick","User-Agent":"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/124.0 Safari/537.36","x-ulta-api-version":"2","x-ulta-platform":"web"}</code></details> | `keyword` drives base search; optional filters include `sortBy`, `categoryIds`, `pageSize`. Custom lowercase headers required. |
| Product Reviews | `https://api.bazaarvoice.com/data/reviews.json` | `GET` | `?apiversion=5.5&passkey=<public-key>&displaycode=ulta-1&filter=productid:eq:2564014&page=1&page_size=20&include=authors` | <details><summary>JSON</summary><code>{"Accept":"application/json, text/plain, */*","Origin":"https://www.ulta.com","Referer":"https://www.ulta.com/p/lipstick?productId=2564014","User-Agent":"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/124.0 Safari/537.36"}</code></details> | Ulta also fronts Bazaarvoice; `passkey`/`displaycode` rendered in `BV` script tag. Supports `incentivizedstats`, `ratingdistribution`, etc. |

### Nordstrom

| API | Base URL | Method | Example Query | Required Headers | Notes |
| --- | --- | --- | --- | --- | --- |
| Product Listing | `https://www.nordstrom.com/api/category/{categoryId}` | `GET` | `?page=1&pageSize=24&sort=featured` | <details><summary>JSON</summary><code>{"Accept":"application/json, text/plain, */*","Origin":"https://www.nordstrom.com","Referer":"https://www.nordstrom.com/browse/women","User-Agent":"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/124.0 Safari/537.36","x-country-code":"US","x-language":"en-US"}</code></details> | Swap `{categoryId}` with numeric dept ID (e.g. `6000002`). Response includes `products` + `facets`; `page`/`pageSize` paginate grid results. |
| Search Suggestions | `https://www.nordstrom.com/api/search/data` | `GET` | `?keyword=lipstick&top=20&skip=0` | <details><summary>JSON</summary><code>{"Accept":"application/json, text/plain, */*","Origin":"https://www.nordstrom.com","Referer":"https://www.nordstrom.com/sr?keyword=lipstick","User-Agent":"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/124.0 Safari/537.36","x-country-code":"US","x-language":"en-US"}</code></details> | `top` controls returned records; `skip` is the offset. Match locale headers to target site language. |
| Product Reviews | `https://api.bazaarvoice.com/data/reviews.json` | `GET` | `?apiversion=5.5&passkey=<public-key>&displaycode=nordstrom-en_us&filter=productid:eq:6525612&page=1&page_size=20&sort=relevancy:desc` | <details><summary>JSON</summary><code>{"Accept":"application/json, text/plain, */*","Origin":"https://www.nordstrom.com","Referer":"https://www.nordstrom.com/s/product/6525612","User-Agent":"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/124.0 Safari/537.36"}</code></details> | Nordstrom exposes Bazaarvoice behind the scenes. Identify the `passkey`/`displaycode` from `Bazaarvoice` script tags. Supports `Filter=HasPhotos:eq:true` for UGC media pulls. |

## Repository goals

- ✅ Provide a single, version-controlled index of high-value retail API endpoints.
- ✅ Document practical request examples (URL + headers) that community members can reproduce.
- ✅ Encourage contributions via Pull Requests, similar to other public API catalogs.


## Contributing

1. Fork the repository and create a topical branch (e.g. `feature/add-kohls-api`).
2. Add or update rows in the "Contents" table above (keep columns in the documented order).
3. Include a short description, verified sample query, and minimum headers required to replay the request.
4. Run any linters or formatters you've configured (none are imposed by default).
5. Open a Pull Request that briefly explains how you discovered or tested the endpoint.

Need help structuring a new entry? Copy/paste an existing table row and adjust the cells for the new API. Feel free to open issues for discussion or share additional context before submitting a PR.

## License

All original content in this repository is released under the [MIT License](LICENSE). API responses belong to their respective owners; please follow each retailer's Terms of Service.
