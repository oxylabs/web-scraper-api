# web-scraper-api
[![web-scraper-api](https://github.com/oxylabs/web-scraper-api/blob/main/Github-banner-Web%20Scraper%20API-1532x354.jpg)]([https://oxylabs.io/products/residential-proxy-pool](https://oxylabs.io/products/scraper-api/webs))

[![](https://dcbadge.limes.pink/api/server/Pds3gBmKMH?style=for-the-badge&theme=discord)](https://discord.gg/Pds3gBmKMH) [![YouTube](https://img.shields.io/badge/YouTube-Oxylabs-red?style=for-the-badge&logo=youtube&logoColor=white)](https://www.youtube.com/@oxylabs)

# Web Scraper API
- [What is Web Scraper API?](#what-is-web-scraper-api)
- [Key Features](#key-features)
  - [All-in-One Web Data Collection](#all-in-one-web-data-collection)
  - [Dedicated Scrapers and Parsers](#dedicated-scrapers-and-parsers)
  - [JavaScript Rendering and Browser Instructions](#javascript-rendering-and-browser-instructions)
  - [Geolocation and Localization](#geolocation-and-localization)
  - [Custom Parser](#custom-parser)
  - [Scheduler](#scheduler)
  - [OxyCopilot](#oxycopilot)
- [How Does Web Scraper API Work?](#how-does-web-scraper-api-work)
  - [Integration Methods](#integration-methods)
  - [Request Example](#request-example)
- [Supported Targets](#supported-targets)
- [Web Scraper API vs. Web Unblocker vs. Headless Browser](#web-scraper-api-vs-web-unblocker-vs-headless-browser)
  - [When to Choose Each](#when-to-choose-each)
- [Common Use Cases](#common-use-cases)
- [Output Formats and Delivery](#output-formats-and-delivery)
- [Rate Limits and Batch Requests](#rate-limits-and-batch-requests)
- [Learn More](#learn-more)
- [Contact Us](#contact-us)

Welcome to the official repository overview for Oxylabs' [Web Scraper API](https://oxylabs.io/products/scraper-api/webs). This guide is a developer-focused, technical reference covering what Web Scraper API is, how it works, its key features, supported targets, and when it fits your web scraping pipeline. It also serves as the central hub linking to all Web Scraper API-related repositories, code examples, and integrations.

## What is Web Scraper API?

Web Scraper API is an all-in-one web data collection solution designed for extracting real-time data at scale from any public website. It combines proxies, uninterrupted access, crawling, and parsing into a single API, so you don't have to manage separate tools or maintain scraping infrastructure yourself.

The product covers every stage of web scraping – from sending requests and handling interferences with IPs and CAPTCHAs, to rendering JavaScript, parsing the response, and delivering the result to your preferred storage. You send a single API request specifying a target URL or query, and Web Scraper API returns either raw HTML or structured JSON ready for use.

Web Scraper API is built to meet enterprise standards, including SOC 2 Type II compliance, and runs on fast-adapting infrastructure maintained by Oxylabs' in-house engineering team. This makes it suitable for high-volume, production-grade data extraction across search engines, e-commerce marketplaces, travel platforms, real estate sites, and generic web pages.


## Key Features

Web Scraper API is designed around three core capabilities: reliable access request handling, accurate structured data extraction, and flexible automation for custom workflows.

### All-in-One Web Data Collection

Web Scraper API consolidates the entire scraping stack – proxy rotation, automated access management, CAPTCHA handling, JavaScript rendering, parsing, and delivery – behind a single API endpoint. There is no need to combine separate proxy providers, uninterrupted access layers, headless browser setups, and parsers. One request returns the data.

The built-in proxy rotator uses Oxylabs' ethically sourced proxy network, and IP interruptions plus CAPTCHA challenges are handled automatically as part of the request lifecycle.

### Dedicated Scrapers and Parsers

In addition to a `universal` source that works with any public website, Web Scraper API ships with dedicated sources tuned for popular targets. These return ready-to-use structured JSON without you having to write or maintain parsing logic.

Dedicated sources include search engines (Google Search, Google Ads, Google Trends, Google Lens, Bing), AI platforms (ChatGPT, Perplexity, Google AI Mode), and major e-commerce marketplaces (Amazon, Walmart, eBay, Etsy, Best Buy, Target, Costco, AliExpress, Alibaba, Lazada, Flipkart, MercadoLibre, and many more). See the full list under our [Supported Targets](https://developers.oxylabs.io/api-targets).

For our targets, you can pass either a full URL or parametrized inputs like a search query, product ID, or video ID, or set `"parse": true` to receive structured JSON instead of HTML.

### JavaScript Rendering and Browser Instructions

For dynamic, JavaScript-heavy pages, Web Scraper API supports JavaScript rendering through its Custom Browser feature. Set the `render` parameter to `html` to retrieve the rendered HTML, or to `png` to receive a Base64-encoded screenshot.

When pages require user-like interaction – clicks, form input, scrolling, or waiting for elements to load – you can pass a list of [browser instructions](https://developers.oxylabs.io/products/web-scraper-api/features/js-rendering-and-browser-control#browser-instructions) in the `browser_instructions` parameter. 
Example: input `"pizza boxes"` into an eBay search field, click the submit button, then wait for results.

```json
{
  "source": "universal",
  "url": "https://www.ebay.com/",
  "render": "html",
  "browser_instructions": [
    { "type": "input", "value": "pizza boxes", "selector": { "type": "xpath", "value": "//input[@class='gh-tb ui-autocomplete-input']" } },
    { "type": "click", "selector": { "type": "xpath", "value": "//input[@type='submit']" } },
    { "type": "wait", "wait_time_s": 5 }
  ]
}
```

Browser instructions can be generated and tested without manual coding through the Web Scraper API Playground in the Oxylabs dashboard.

### Geolocation and Localization

The `geo_location` parameter lets you choose the proxy server location, returning data as if you were browsing from that country, state, or city. Its exact behavior differs by source category:

- For [SERP sources](https://developers.oxylabs.io/products/web-scraper-api/features/localization/serp-localization), `geo_location` adjusts the search results page to reflect what users in that location would see.
- For [E-commerce sources](https://developers.oxylabs.io/products/web-scraper-api/features/localization/e-commerce-localization), specific values are required by certain marketplaces – check the per-target documentation.

Additional `domain`, `locale`, and `results_language` parameters customize the top-level domain, interface language, and result language for region-specific extraction.

### Custom Parser

Custom Parser is a free feature that lets you define your own parsing logic on top of a raw scraping result, returning only the fields you care about in a structured format. It is configurable through the API or the dashboard, and Parser Presets let you save, manage, and reuse parsing configurations across jobs.

See the [Custom Parser](https://developers.oxylabs.io/products/web-scraper-api/features/custom-parser) and [Parser Presets](https://developers.oxylabs.io/products/web-scraper-api/features/custom-parser/parser-presets) documentation for details.

### Scheduler

Scheduler is a complimentary feature that lets you automate recurring scraping jobs. Instead of issuing identical requests on a timer from your side, you submit a schedule once – with a cron expression, target parameters, an optional end time, and optional callback or cloud storage URLs – and Web Scraper API runs the jobs on the defined cadence.

Example payload running every hour until a specified end date:

```json
{
  "cron": "0 * * * *",
  "items": [
    {
      "source": "universal",
      "url": "https://example.com",
      "parse": true,
      "render": "html"
    }
  ],
  "end_time": "2026-12-01 00:00:00"
}
```

`POST` to `https://data.oxylabs.io/v1/schedules`. See the [Scheduler](https://developers.oxylabs.io/products/web-scraper-api/features/scheduler) documentation for the full parameter list.

### OxyCopilot

[OxyCopilot](https://developers.oxylabs.io/products/web-scraper-api/web-scraper-api-playground/oxycopilot) is an AI-powered assistant inside the Scraper API Playground that generates scraping requests and parsing instructions from plain-English prompts. Describe the page you want to scrape and the fields you need, and OxyCopilot produces a ready-to-use API request along with a parsing template, including for nested or listed data. It is intended to reduce setup time for new targets and adapt quickly to layout changes.

## How Does Web Scraper API Work?

You send an authenticated HTTP request specifying what to scrape (URL or query), which source to use, and any optional parameters (geolocation, rendering, parsing, callback, storage). Web Scraper API handles proxy rotation, retries, automated request management, JavaScript rendering, and parsing as part of the request lifecycle, then returns the result either synchronously or via callback/storage.

### Integration Methods

Web Scraper API offers three integration methods, chosen per request:

| Method | Type | Endpoint | When to use it |
| --- | --- | --- | --- |
| [Realtime](https://developers.oxylabs.io/products/web-scraper-api/integration-methods/realtime) | Synchronous | `https://realtime.oxylabs.io/v1/queries` | One-off requests where you want results in the same connection. |
| [Push-Pull](https://developers.oxylabs.io/products/web-scraper-api/integration-methods/push-pull) | Asynchronous | `https://data.oxylabs.io/v1/queries` | Large workloads. Recommended for high volumes. Results remain available for at least 24 hours. |
| [Proxy Endpoint](https://developers.oxylabs.io/products/web-scraper-api/integration-methods/proxy-endpoint) | Synchronous | `https://realtime.oxylabs.io:60000` | URL-based scraping when you want to use Web Scraper API as a regular HTTPS proxy. Only accepts a limited set of additional parameters. |

Push-Pull supports [batch requests](https://developers.oxylabs.io/products/web-scraper-api/integration-methods/push-pull) – up to 5,000 `query` or `url` values in one POST to `https://data.oxylabs.io/v1/queries/batch`. Each entry is treated as a separate job and can be returned via callback or written directly to AWS S3 or Google Cloud Storage. Realtime and Proxy Endpoint do not support batch.

Authentication for all methods is HTTP Basic Auth with your dashboard `USERNAME` and `PASSWORD`.

### Request Example

Realtime request against the `universal` source:

```bash
curl 'https://realtime.oxylabs.io/v1/queries' \
  --user "USERNAME:PASSWORD" \
  -H "Content-Type: application/json" \
  -d '{
    "source": "universal",
    "url": "https://sandbox.oxylabs.io/",
    "geo_location": "United States"
  }'
```

Realtime request against a dedicated source returning parsed JSON:

```bash
curl 'https://realtime.oxylabs.io/v1/queries' \
  --user "USERNAME:PASSWORD" \
  -H "Content-Type: application/json" \
  -d '{
    "source": "amazon_product",
    "query": "B07FZ8S74R",
    "geo_location": "90210",
    "parse": true
  }'
```

Push-Pull request with delivery to S3:

```bash
curl 'https://data.oxylabs.io/v1/queries' \
  --user "USERNAME:PASSWORD" \
  -H "Content-Type: application/json" \
  -d '{
    "source": "google_search",
    "query": "adidas",
    "geo_location": "California,United States",
    "parse": true,
    "callback_url": "https://your.callback.url",
    "storage_type": "s3",
    "storage_url": "s3://your.storage.bucket.url"
  }'
```

Each response includes a `job_id` (also returned in the `x-oxylabs-job-id` header), which is the identifier used for troubleshooting and result retrieval.

## Supported Targets

Web Scraper API ships with dedicated `source` values for many high-priority targets, plus a `universal` source that works against any public website. Dedicated sources accept either URLs or parametrized inputs (queries, product IDs, video IDs), and most support structured JSON output via `"parse": true`.

Categories with dedicated sources include:

- **Search engines:** Google, Bing.
- **AI platforms:** ChatGPT, Perplexity.
- **Video and social:** YouTube (search, video metadata, transcripts, subtitles, channel, download), TikTok Shop.
- **Global e-commerce:** Amazon, Walmart, eBay, Etsy, Best Buy, Target, Costco, Kroger, Menards, Petco, Grainger, etc.
- **International marketplaces:** Alibaba, AliExpress, Allegro, Idealo, Taobao, MediaMarkt, Rakuten, Tokopedia, Flipkart, MercadoLibre, etc.
- **Travel and real estate:** Airbnb, Zillow.
- **Anything else:** the `universal` source, for any public URL.

The full, up-to-date list of sources and their parametrized inputs is in the official [documentation](https://developers.oxylabs.io/products/web-scraper-api).

## Web Scraper API vs. Web Unblocker vs. Headless Browser

Oxylabs offers three scraping products, each suited to a different level of control and complexity. Choose based on what you actually need from the response and how much of the scraping pipeline you want to own.

| Feature | Web Scraper API | Web Unblocker | Headless Browser |
| --- | --- | --- | --- |
| **Main purpose** | All-in-one data collection: send a request, get structured results | Proxy-style access to raw web content with automatic access | Full remote browser automation for the toughest targets |
| **Request input** | URL or query + source + optional parameters | URL via proxy connection (with optional headers) | Automation script (Puppeteer / Playwright / CDP) |
| **Output** | Raw HTML or structured JSON, Screenshot image, and Markdown | Full HTML | HTML, screenshots, network logs, anything your script extracts |
| **JavaScript rendering** | Yes, via `render` parameter | Yes | Yes (native – runs JS as a real browser) |
| **Parsing built-in** | Yes (dedicated parsers + Custom Parser) | No | No |
| **CAPTCHA handling** | Automatic | Automatic | Automatic + manual trigger support |
| **Ease of use** | Easiest – minimal code, focus on results | Intermediate – you handle HTML yourself | Advanced – you write full automation scripts |
| **Billing** | Per successful result | Per successful request traffic | Per traffic (GB) used |

### When to Choose Each

- [Web Scraper API](https://oxylabs.io/products/scraper-api/web) – you want ready-to-use data with a single API call. Best for e-commerce, SERP scraping, AI training data collection, and any workflow where you'd otherwise build your own proxy + uninterrupted access + parser stack.
- [Web Unblocker](https://oxylabs.io/products/web-unblocker) – you have an existing scraping pipeline and need a drop-in proxy replacement that handles anti-bot challenges automatically. You keep control of parsing.
- [Headless Browser](https://oxylabs.io/products/headless-browser) – you need full browser control for JavaScript-heavy SPAs, multi-step interactions, login flows, AI-driven web automation, or workflows that require visual rendering and stateful sessions.

For Oxylabs' AI-tuned search retrieval product (different category – LLM-grade search results rather than scraping), check out [Fast Search API](https://oxylabs.io/products/scraper-api/fast-search).

## Common Use Cases

Web Scraper API is the right choice when your goal is reliable, structured data from public websites at scale, without owning the scraping infrastructure. Common scenarios include:

1. **E-commerce intelligence** – real-time pricing, stock levels, product details, and reviews across competitor marketplaces for dynamic pricing, assortment monitoring, and brand reputation tracking.
2. **SEO and LLM monitoring** – scraping SERP data (Google, Bing) and AI platforms (ChatGPT, Perplexity) to monitor brand visibility, rankings, AI-generated mentions, featured snippets, and local pack results. Useful for combined SEO and GEO (generative engine optimization) strategies.
3. **AI development and training data** – high-quality, structured datasets from multiple sources (text, video metadata, e-commerce listings) for training and fine-tuning language and multimodal models, including real-time data to keep models current.
4. **Real estate analytics** – property listings, prices, location data, and rental rates from sources like Zillow and Airbnb for trend analysis and valuation.
5. **Travel industry insights** – flight prices, hotel availability, and customer reviews for competitive analysis and offer optimization.
6. **Entertainment market research** – social signals, ratings, and audience insights from platforms like TikTok, IMDb, or Netflix for content strategy and engagement analysis.
7. **Generic web data extraction** – any public website via the `universal` source, with optional rendering and Custom Parser.

If your task requires real browser interaction (multi-step clicks, form fills, login state across pages), Headless Browser is usually the better fit. If you just need a proxy layer that gives access to targets for an existing pipeline, use Web Unblocker.

## Output Formats and Delivery

Web Scraper API can return:

- **Raw HTML** – the default when `parse` is not set.
- **Structured JSON** – when `"parse": true` is used with a [dedicated parser](https://developers.oxylabs.io/products/web-scraper-api/features/dedicated-parsers) or with [Custom Parser](https://developers.oxylabs.io/products/web-scraper-api/features/custom-parser).
- **Rendered HTML** – set `"render": "html"` for JavaScript-rendered pages.
- **Screenshots** – set `"render": "png"` to receive a Base64-encoded screenshot. For image downloading workflows, see the [Download Images](https://developers.oxylabs.io/products/web-scraper-api/features/download-images) documentation.
- **Markdown** – set `"markdown": true` in your request payload. By default, this parameter is set to `false`. See the [Markdown Output](https://developers.oxylabs.io/products/web-scraper-api/features/result-processing-and-storage/output-types/markdown-output) documentation for more details.

Results can be delivered:

- **Synchronously** in the Realtime response body.
- **Via callback URL (Push-Pull)** – Oxylabs sends a JSON payload to your server on job completion.
- **Directly to cloud storage** – AWS S3 or Google Cloud Storage, by setting `storage_type` and `storage_url`.

Push-Pull job results are available for at least 24 hours after completion.

## Rate Limits and Batch Requests

Job-submission rate limits depend on your subscription plan. We have multiple regular and enterprise plans available, starting from Free trial, Micro, Starter, Advanced, to Venture, Business, Corporate, and even Custom+ plans for you to choose based on your necessity. See the [Rate Limits](https://developers.oxylabs.io/products/web-scraper-api/usage-and-billing/rate-limits) documentation for current values.

For high-volume workloads, Push-Pull's [batch endpoint](https://developers.oxylabs.io/products/web-scraper-api/integration-methods/push-pull) accepts up to 5,000 `query` or `url` values per request. All other parameters in a batch are singular and apply to every job in the batch.

Some additional product limits worth knowing:

- The `query` parameter for `google_search` is limited to 2048 characters (multi-byte characters count as 1).
- A small list of domains is internally interrupted and not accessible via Web Scraper API. If a request to one of these returns with no reliable access, contact support – exceptions are reviewed case by case.

## Learn More

For detailed configuration, advanced usage, and code examples in multiple languages, check the official documentation:

- [Get started with Web Scraper API](https://oxylabs.io/products/scraper-api/web)
- [Web Scraper API documentation](https://developers.oxylabs.io/products/web-scraper-api)
- [Integration methods](https://developers.oxylabs.io/products/web-scraper-api/integration-methods)

## Contact Us

If you have questions or need support, reach out to us at [support@oxylabs.io](mailto:support@oxylabs.io), or through live chat in the [Oxylabs Dashboard](https://dashboard.oxylabs.io/). For enterprise inquiries, contact your dedicated account manager.
