# Common Retail APIs

A curated list of publicly discoverable web APIs used by major U.S. beauty and department store retailers. Inspired by [public-apis/public-apis](https://github.com/public-apis/public-apis), this repository documents endpoints, request patterns, and headers needed to experiment with Macy's, Sephora, Ulta, and Nordstrom data.

## Contents

| API | Base URL | Category | Notes |
| --- | --- | --- | --- |
| Macy's Catalog Search | `https://www.macys.com/xapi/discover/v1/catalog/search` | Beauty & Fashion | Provides keyword-driven catalog listings pulled from macys.com XAPI services. |
| Sephora Catalog Search | `https://www.sephora.com/api/catalog/search` | Beauty & Fashion | Backing API for Sephora on-site product search pages. |
| Ulta Product Search | `https://services.ulta.com/search/v2/search/product` | Beauty & Fashion | JSON search index powering Ulta.com storefront. |
| Nordstrom Search Suggestions | `https://www.nordstrom.com/api/search/data` | Beauty & Fashion | Returns product suggestions and listings for Nordstrom search queries. |

Detailed request examples (query parameters + headers) are listed below for quick reference.

## Repository goals

- ✅ Provide a single, version-controlled index of high-value retail API endpoints.
- ✅ Document practical request examples (URL + headers) that community members can reproduce.
- ✅ Encourage contributions via Pull Requests, similar to other public API catalogs.

## Data format

Each API entry is documented directly in this README using the following fields:

- **Company / Name** – Who runs the API and what functionality it exposes.
- **Base URL** – The root endpoint to call.
- **Example** – Method, query parameters, and headers required to replay the request successfully.
- **Notes** – Any practical guidance (pagination, locale, required custom headers, etc.).

## API details

### Macy's Catalog Search

- **Company**: Macys
- **Base URL**: `https://www.macys.com/xapi/discover/v1/catalog/search`
- **Method**: `GET`
- **Example query**: `https://www.macys.com/xapi/discover/v1/catalog/search?searchphrase=lipstick&page=1&pageSize=40&sortBy=ORIGINAL`
- **Required headers**:
  - `Accept: application/json, text/plain, */*`
  - `Content-Type: application/json`
  - `Origin: https://www.macys.com`
  - `Referer: https://www.macys.com/shop/featured/lipstick`
  - `User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/124.0 Safari/537.36`
- **Notes**:
  - Pagination is controlled via `page` and `pageSize` query parameters.
  - A realistic browser `User-Agent` header prevents HTTP 403 responses.

### Sephora Catalog Search

- **Company**: Sephora
- **Base URL**: `https://www.sephora.com/api/catalog/search`
- **Method**: `GET`
- **Example query**: `https://www.sephora.com/api/catalog/search?keyword=lipstick&pageSize=60&currentPage=1`
- **Required headers**:
  - `Accept: application/json, text/plain, */*`
  - `Origin: https://www.sephora.com`
  - `Referer: https://www.sephora.com/search?keyword=lipstick`
  - `User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/124.0 Safari/537.36`
  - `X-Requested-With: XMLHttpRequest`
- **Notes**:
  - `keyword` is required; pagination uses `currentPage` + `pageSize`.
  - Keep `Origin` and `Referer` aligned with the on-site search page for consistent results.

### Ulta Product Search

- **Company**: Ulta Beauty
- **Base URL**: `https://services.ulta.com/search/v2/search/product`
- **Method**: `GET`
- **Example query**: `https://services.ulta.com/search/v2/search/product?keyword=lipstick&page=1&pageSize=24&sortBy=bestSeller`
- **Required headers**:
  - `Accept: application/json, text/plain, */*`
  - `Origin: https://www.ulta.com`
  - `Referer: https://www.ulta.com/search?keyword=lipstick`
  - `User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/124.0 Safari/537.36`
  - `x-ulta-api-version: 2`
  - `x-ulta-platform: web`
- **Notes**:
  - `keyword` drives the base search; optional filters include `sortBy`, `categoryIds`, and `pageSize`.
  - Ulta services expect the lowercase custom headers shown above.

### Nordstrom Search Data

- **Company**: Nordstrom
- **Base URL**: `https://www.nordstrom.com/api/search/data`
- **Method**: `GET`
- **Example query**: `https://www.nordstrom.com/api/search/data?keyword=lipstick&top=20&skip=0`
- **Required headers**:
  - `Accept: application/json, text/plain, */*`
  - `Origin: https://www.nordstrom.com`
  - `Referer: https://www.nordstrom.com/sr?keyword=lipstick`
  - `User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/124.0 Safari/537.36`
  - `x-country-code: US`
  - `x-language: en-US`
- **Notes**:
  - `top` controls the number of returned records; `skip` functions as an offset.
  - Locale headers (`x-country-code`, `x-language`) should match the Nordstrom site locale.

## Contributing

1. Fork the repository and create a topical branch (e.g. `feature/add-kohls-api`).
2. Add or update entries in the "API details" section below by following the documented structure.
3. Include a short description, verified sample query, and minimum headers required to replay the request.
4. Run any linters or formatters you've configured (none are imposed by default).
5. Open a Pull Request that briefly explains how you discovered or tested the endpoint.

Need help structuring a new entry? Copy/paste one of the existing markdown blocks and adjust the details for the new API. Feel free to open issues for discussion or share additional context before submitting a PR.

## License

All original content in this repository is released under the [MIT License](LICENSE). API responses belong to their respective owners; please follow each retailer's Terms of Service.
