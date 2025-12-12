# Common Retail APIs

A curated list of publicly discoverable web APIs used by major U.S. beauty and department store retailers. Inspired by [public-apis/public-apis](https://github.com/public-apis/public-apis), this repository documents endpoints, request patterns, and headers needed to experiment with Macy's, Sephora, Ulta, and Nordstrom data.

## Contents

| API | Base URL | Category | Notes |
| --- | --- | --- | --- |
| API | Base URL | Method | Example Query | Required Headers | Notes |
| --- | --- | --- | --- | --- | --- |
| Macy's Catalog Search | `https://www.macys.com/xapi/discover/v1/catalog/search` | `GET` | `?searchphrase=lipstick&page=1&pageSize=40&sortBy=ORIGINAL` | `Accept: application/json, text/plain, */*`<br>`Content-Type: application/json`<br>`Origin: https://www.macys.com`<br>`Referer: https://www.macys.com/shop/featured/lipstick`<br>`User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/124.0 Safari/537.36` | Pagination controlled via `page`/`pageSize`. Browser-like `User-Agent` prevents 403 responses. |
| Sephora Catalog Search | `https://www.sephora.com/api/catalog/search` | `GET` | `?keyword=lipstick&pageSize=60&currentPage=1` | `Accept: application/json, text/plain, */*`<br>`Origin: https://www.sephora.com`<br>`Referer: https://www.sephora.com/search?keyword=lipstick`<br>`User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/124.0 Safari/537.36`<br>`X-Requested-With: XMLHttpRequest` | `keyword` parameter required; pagination uses `currentPage` + `pageSize`. Keep origin/referer aligned with onsite search page. |
| Ulta Product Search | `https://services.ulta.com/search/v2/search/product` | `GET` | `?keyword=lipstick&page=1&pageSize=24&sortBy=bestSeller` | `Accept: application/json, text/plain, */*`<br>`Origin: https://www.ulta.com`<br>`Referer: https://www.ulta.com/search?keyword=lipstick`<br>`User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/124.0 Safari/537.36`<br>`x-ulta-api-version: 2`<br>`x-ulta-platform: web` | `keyword` drives base search; optional filters include `sortBy`, `categoryIds`, `pageSize`. Custom lowercase headers required. |
| Nordstrom Search Suggestions | `https://www.nordstrom.com/api/search/data` | `GET` | `?keyword=lipstick&top=20&skip=0` | `Accept: application/json, text/plain, */*`<br>`Origin: https://www.nordstrom.com`<br>`Referer: https://www.nordstrom.com/sr?keyword=lipstick`<br>`User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/124.0 Safari/537.36`<br>`x-country-code: US`<br>`x-language: en-US` | `top` controls returned records; `skip` is the offset. Match locale headers to target site language. |

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
