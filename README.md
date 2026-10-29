# Bulk Image Downloader & Converter — Resize, WebP, ZIP — Python, Node.js & cURL examples

**Download images in bulk** from direct image URLs or from whole web pages (img, srcset, lazy-loading), then optionally **resize, compress and convert** them to **JPG, PNG or WebP** (HEIC and AVIF input supported), **remove duplicates**, **skip tiny icons** and tracking pixels and get everything in **one ZIP**.

Hosted on Apify: **[Bulk Image Downloader & Converter — Resize, WebP, ZIP](https://apify.com/tidydata/bulk-image-downloader-converter?fpr=wtg6qt)**. These examples show how to call it from your code; the Actor runs in the cloud, no API key for the source site, no proxies to manage.

## Python

```bash
pip install apify-client
export APIFY_TOKEN=...   # free account at apify.com → Settings → API & Integrations
```

```python
import os
from apify_client import ApifyClient

client = ApifyClient(os.environ["APIFY_TOKEN"])
run = client.actor("tidydata/bulk-image-downloader-converter").call(run_input={
    "urls": [
        {
            "url": "https://en.wikipedia.org/wiki/Photography"
        }
    ],
    "outputFormat": "webp",
    "maxWidth": 1600,
    "quality": 82,
    "minWidth": 200,
    "createZip": True
})
for item in client.dataset(run["defaultDatasetId"]).iterate_items():
    print({k: item.get(k) for k in ['fileUrl', 'sourceUrl', 'width', 'height', 'bytes', 'originalBytes']})
```

## Node.js

```javascript
import { ApifyClient } from 'apify-client';

const client = new ApifyClient({ token: process.env.APIFY_TOKEN });
const run = await client.actor('tidydata/bulk-image-downloader-converter').call({"urls": [{"url": "https://upload.wikimedia.org/wikipedia/commons/a/a9/Example.jpg"}], "outputFormat": "webp"});
const { items } = await client.dataset(run.defaultDatasetId).listItems();
console.log(items.length, items[0]);
```

## cURL (one call, results as JSON)

```bash
curl -s -X POST "https://api.apify.com/v2/acts/tidydata~bulk-image-downloader-converter/run-sync-get-dataset-items?token=$APIFY_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"urls": [{"url": "https://upload.wikimedia.org/wikipedia/commons/a/a9/Example.jpg"}], "outputFormat": "webp"}'
```

## More TidyData Actors

[YouTube Transcript](https://apify.com/tidydata/youtube-transcript-scraper?fpr=wtg6qt) · [YouTube Comments](https://apify.com/tidydata/youtube-comments-scraper?fpr=wtg6qt) · [YouTube Scraper](https://apify.com/tidydata/youtube-channel-scraper?fpr=wtg6qt) · [Website Contacts](https://apify.com/tidydata/website-contact-extractor?fpr=wtg6qt) · [Google News](https://apify.com/tidydata/google-news-scraper?fpr=wtg6qt) · [App Reviews](https://apify.com/tidydata/app-reviews-scraper?fpr=wtg6qt) · [Merge & Dedupe](https://apify.com/tidydata/merge-dedupe-datasets?fpr=wtg6qt) · [all of them](https://github.com/tidydata-dev)

Examples are MIT-licensed.

---
<sub>Links to apify.com include our affiliate ID: if you start a paid Apify plan through them, Apify pays TidyData a commission at no extra cost to you.</sub>
