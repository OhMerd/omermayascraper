# Maya TASE Selector Mapping Guide

This guide maps the existing Sysco scraper selectors to their Maya TASE equivalents.

## Key Differences Between Sysco and Maya TASE

### Sysco (E-commerce)
- Product-focused scraping
- Category navigation
- Product detail pages
- Shopping cart functionality

### Maya TASE (Financial Reports)
- Document/report focused
- Search and filter functionality
- Tabular data extraction
- PDF document downloads

## Selector Mapping

### 1. Navigation & Authentication

| Sysco Selector | Purpose | Maya TASE Equivalent | Notes |
|----------------|---------|---------------------|--------|
| `button[data-id="btn_login_continue_as_guest"]` | Guest login | `button:contains("התחברות")` | Hebrew text, may not need guest mode |
| `input[data-id="initial_zipcode_modal_input"]` | Location input | Not applicable | Maya TASE doesn't use location |

### 2. Category/Section Navigation

| Sysco Selector | Purpose | Maya TASE Equivalent | Notes |
|----------------|---------|---------------------|--------|
| `[data-id="lbl_category_app.dashboard.produce.title"]` | Category selection | `nav a[href*="immediate-reports"]` | Navigate to report sections |
| `[data-id="lbl_category_app.dashboard.meatseafood.title"]` | Category selection | `nav a[href*="periodic-reports"]` | Different report types |

### 3. Content Listing

| Sysco Selector | Purpose | Maya TASE Equivalent | Notes |
|----------------|---------|---------------------|--------|
| `a[href*="/product-details/"]` | Product links | `a[href*="report"], a[href*="document"]` | Report/document links |
| Product grid containers | Product listing | `table tbody tr, .report-list .item` | Reports often in tables |

### 4. Detail Page Content

| Sysco Selector | Purpose | Maya TASE Equivalent | Notes |
|----------------|---------|---------------------|--------|
| `[data-id="product_brand_link"]` | Brand name | `.company-name, .entity-name` | Company instead of brand |
| `[data-id="product_packaging_text"]` | Product info | `.report-type, .document-type` | Report type instead |
| `[data-id="pack_size"]` | Size info | Not applicable | No equivalent in financial reports |
| `[data-id="product_id"]` | Product ID | `.report-number, .document-id` | Report numbers |
| `[data-id="main-product-img-v2"]` | Product image | Not applicable | Reports don't have images |
| `[data-id="product_description_section"]` | Description | `.report-content, .summary` | Report content |
| `[data-id="ingredients_text"]` | Ingredients | Not applicable | No equivalent |

### 5. Pagination

| Sysco Selector | Purpose | Maya TASE Equivalent | Notes |
|----------------|---------|---------------------|--------|
| `button[data-id="button_page_next"]` | Next page | `button:contains("הבא"), .next` | Hebrew "Next" |
| `button[data-id^="button_page_"]` | Page numbers | `.pagination button, .page-number` | Generic pagination |

## Maya TASE Specific Selectors

These selectors are unique to Maya TASE and have no Sysco equivalent:

### Search & Filters
```css
/* Date range filters */
input[name*="from"], input[placeholder*="מתאריך"]
input[name*="to"], input[placeholder*="עד תאריך"]

/* Company/Entity filters */
select[name*="company"], .company-filter

/* Report type filters */
select[name*="type"], .report-type-filter

/* Search button */
button:contains("חפש"), button[type="submit"]
```

### Document Specific
```css
/* PDF download links */
a[href*=".pdf"], a[download], .download-link

/* Report metadata */
.report-date, .publish-date, time
.report-number, .reference-number
.entity-id, .company-code

/* Attachments */
.attachment, .file-link, .document-attachment
```

### Data Tables
```css
/* Financial data tables */
table, .data-table, .financial-data
thead tr, .header-row
tbody tr, .data-row
td, .cell, .data-cell
```

## Implementation Notes

1. **Hebrew Text**: Use `:contains()` selectors carefully with Hebrew text
2. **Material Design**: Maya TASE uses Angular Material, look for Material CSS classes
3. **AJAX Loading**: Content may load dynamically, use proper wait strategies
4. **PDF Handling**: Many documents are PDFs, plan for download/parsing
5. **Date Formats**: Israeli date formats (DD/MM/YYYY)
6. **Right-to-Left**: Hebrew sites use RTL layout

## Testing Strategy

1. **Manual Inspection**: Use browser dev tools to identify actual selectors
2. **Incremental Testing**: Test selectors one section at a time
3. **Fallback Selectors**: Always provide multiple selector options
4. **Dynamic Content**: Test with different data loads
5. **Mobile Responsive**: Check selectors work on different screen sizes

## Next Steps

1. Visit https://maya.tase.co.il/he manually
2. Use browser dev tools to identify actual element selectors
3. Update the configuration file with real selectors
4. Test each selector group individually
5. Implement error handling for missing elements