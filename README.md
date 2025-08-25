# Sysco Product Scraper

A comprehensive web scraping solution for extracting product data from Sysco's website using Node.js, Puppeteer, and advanced automation techniques.

## Features

- **Advanced web scraping** - Puppeteer with stealth capabilities and anti-detection
- **Robust error handling** - Automatic retry mechanisms and frame recovery
- **Comprehensive data collection** - 28 fields per product including all required data
- **Database storage** - SQLite database with efficient querying and data integrity
- **CSV export** - Multiple export formats with unified data compilation
- **Business intelligence analysis** - comprehensive data visualization and insights
- **Scalable architecture** - Configurable limits and efficient processing
- **Oregon-based collection** - ZIP code 97209 for geographic accuracy

## Quick Start

```bash
npm install
npm run setup
npm run scrape
npm run export
npm run analyze # Generate business analysis and visualizations
```

## Data Collected

For each product, the scraper collects:
- Brand Name
- Product Name  
- Packaging Information
- SKU (Product ID)
- Picture URL
- Description
- Category
- Product URL
- Unit Size
- Case Size
- Weight
- UPC/GTIN
- Supplier
- Manufacturer
- Specifications
- Nutrition Information
- Ingredients
- Allergens
- Storage Instructions
- Shelf Life
- Location ZIP
- Scraped Date
- Updated Date
- Scrape Session ID
- Structured Data

## Output

- **Database**: `data/sysco.db` - SQLite database with all collected data
- **CSV export**: `data/sysco_products_final_2025-08-11.csv` - Complete unified dataset
- **Business Analysis**: `analysis_output/` directory with charts and reports

## Categories Scraped

The scraper processes 10 categories:
1. Meat & Seafood
2. Bakery & Bread
3. Disposables
4. Canned & Dry
5. Frozen Foods
6. Dairy & Eggs
7. Beverages
8. Equipment & Supplies
9. Chemicals
10. Fresh Produce

## Performance

- **Current**: 5,731+ products collected
- **Categories**: 10 categories covered
- **Data Quality**: 96%+ completeness
- **Geographic Focus**: Oregon (ZIP 97209)

## Business Intelligence Analysis

The analysis package generates:

### Visualizations
- **Category Distribution Chart** - Product distribution across categories
- **Top Brands Analysis** - Market concentration and brand performance
- **Data Completeness Chart** - Quality metrics for all collected fields

### Business Report
- **Executive Summary** - Key metrics and achievements
- **Category Analysis** - Performance breakdown by product category
- **Brand Analysis** - Market share and supplier insights
- **Business Recommendations** - Strategic insights for decision-making

### Business Value
- **Market Intelligence** - Comprehensive supplier and product analysis
- **Inventory Planning** - Category-based optimization insights
- **Supplier Relations** - Brand performance and negotiation data
- **Competitive Analysis** - Market positioning and opportunity identification

## Technical Excellence

### Advanced Features
- **Stealth Scraping** - Anti-detection mechanisms for reliable data collection
- **Frame Recovery** - Automatic handling of detached frame errors
- **Duplicate Prevention** - Intelligent deduplication based on SKU
- **Resume Capability** - Interruption recovery without data loss
- **Comprehensive Logging** - Detailed execution tracking and debugging

### Scalability
- **Configurable Limits** - Adjustable page and product limits per category
- **Efficient Processing** - Optimized for large-scale data collection
- **Memory Management** - Resource-efficient operation
- **Error Recovery** - Robust handling of network and browser issues

## Requirements

- Node.js 18+
- Python 3.8+ (for analysis)
- 8GB+ RAM recommended for large datasets

## Configuration

Edit `.env` file to customize:
- `MAX_PAGES_PER_CATEGORY` - Pages to scrape per category
- `MAX_PRODUCTS_PER_CATEGORY` - Products to collect per category
- `DELAY_BETWEEN_PAGES` - Delay between page requests
- `DELAY_BETWEEN_CATEGORIES` - Delay between category switches

## License

MIT License - see LICENSE file for details

## Author

Hod Haim - Comprehensive web scraping and data analysis solution
