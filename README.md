# global-alert-live

# Global CAP Alerts – Live Aggregated Feed

This project provides a continuously updated, consolidated feed of **Common Alerting Protocol (CAP)** alerts from multiple official sources worldwide.

The feed is exposed in two forms:

- A **live, browser-friendly viewer**
- A **raw XML endpoint** suitable for programmatic use

No account, API key, or setup is required to consume the data.

---

## Live viewer

**Human-readable view (auto-refreshing):**  
https://smbcodes.github.io/global-alert-live/

This page fetches the latest aggregated CAP XML and refreshes automatically. It is intended for quick inspection, debugging, and exploratory analysis.

---

## Raw XML feed

**Machine-readable feed:**

https://gcapalertbucket.s3.eu-north-1.amazonaws.com/global_cap.xml

This URL always serves the **latest consolidated XML document**. The file is overwritten on each update, so the URL remains stable.

The document contains only valid `<alert>` elements and supports both CAP 1.1 and CAP 1.2 namespaces.

---

## What the feed contains

- Official CAP alerts from multiple national and regional sources
- Weather, hazard, and emergency notifications
- Alerts merged into a single XML document
- No transformation of alert semantics
- No filtering by severity, region, or category

This is intentionally a **lossless aggregation**, not an interpretation layer.

---

## Update frequency

The feed is updated **once per hour**.

This cadence balances freshness with stability and avoids unnecessary churn for downstream consumers.

---

## How to use it in your own project

### 1) Fetch the XML directly

Any language with HTTP support works.

**Python example:**

### 1) Fetch the XML directly

Any language with HTTP support works.

**Python example:**

```python
import requests

url = "https://gcapalertbucket.s3.eu-north-1.amazonawsaws.com/global_cap.xml"
xml = requests.get(url, timeout=30).text
print(xml[:500])
```
## 2) Parse alerts

Each `<alert>` element follows the CAP specification.

Typical downstream actions include:

- Filtering by `<event>`, `<area>`, or `<severity>`
- Extracting geospatial polygons
- Converting alerts to GeoJSON
- Feeding alerts into dashboards or alerting pipelines

No pagination, cursoring, or authentication is required.

---

## 3) Use the live viewer for inspection

The live site is useful for:

- Inspecting alert structure
- Verifying namespace handling
- Spot-checking new alert formats
- Quick manual sanity checks

Because it is static HTML with client-side fetching, it can be embedded, forked, or mirrored freely.

---

## Intended use cases

- Research and academic analysis
- OSINT and situational awareness
- Visualization and mapping projects
- Emergency-data experimentation
- Feed normalization pipelines
- Personal dashboards

This is **not** an official alerting service and should not be relied on for life-critical notifications.

---

## Data integrity and limitations

- Alerts are included as provided by upstream issuers
- Availability depends on source feeds
- Temporary outages may result in partial updates
- No guarantees of completeness or timeliness

Consumers should treat this as an **aggregation convenience**, not an authoritative source.

---

## License and usage

The aggregation logic is open source.  
Alert data remains governed by the original issuing authorities.

Attribution is recommended where feasible.

---

## Why this exists

Most CAP feeds are:

- Fragmented
- Inconsistent
- Buried behind national portals

This project reduces friction by offering a **single, stable entry point** without interpretation or editorialization.

---

## Requests and extensions

If you want:

- A JSON or GeoJSON mirror
- Severity-filtered variants
- Region-specific subsets
- Alternative refresh cadences

Fork the viewer or open an issue.
