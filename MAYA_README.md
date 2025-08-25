# Maya TASE Financial Reports Scraper

A professional web scraper for Maya TASE (Tel Aviv Stock Exchange) financial reports using Puppeteer and Node.js.

## ✅ What's Ready

### **Complete Maya TASE Scraper**
- ✅ **Working CSS Selectors**: Tested and verified against the live Maya TASE site
- ✅ **Data Extraction**: Extracts company name, report period, publish date, and report links
- ✅ **Pagination Support**: Automatically navigates through multiple pages
- ✅ **Database Integration**: SQLite database with proper schema
- ✅ **CSV Export**: Automatic export to CSV files
- ✅ **Error Handling**: Robust retry logic and error recovery
- ✅ **Session Management**: Tracks scraping sessions for audit trails

### **Data Structure**
Each scraped report contains:
```json
{
  "publishDate": "11:28 25/08/2025",
  "companyName": "רימון ה\"ק", 
  "reportPeriod": "רבעון 2 2025",
  "reportLinks": [{"text": "לדיווח", "href": "..."}],
  "scrapedAt": "2025-08-25T09:16:26.067Z",
  "sourceUrl": "https://maya.tase.co.il/he/reports/financial-report",
  "sessionId": "maya-session-2025-08-25T09-16-07-154Z"
}
```

## 🚀 Quick Start

### 1. Run the Scraper
```bash
# Basic scraping (2 pages)
npm run scrape-maya

# With visible browser for debugging
npm run dev-maya

# Test selectors
npm run test-maya
```

### 2. Advanced Usage
```javascript
import { runMayaScraper } from './src/scrapers/maya-tase-scraper.js';

const options = {
  maxPages: 5,           // Number of pages to scrape
  exportCSV: true,       // Export to CSV
  csvPath: './my-reports.csv',
  filters: {
    year: '2025',
    period: 'רבעון 2',
    company: 'רימון'
  }
};

const results = await runMayaScraper(options);
console.log(`Scraped ${results.summary.totalReports} reports`);
```

## 📊 Features

### **Smart Filtering**
- Filter by company name
- Filter by report period (quarterly/annual)
- Filter by year
- Multiple filter combinations

### **Reliable Data Extraction**
- Handles Hebrew text properly
- Extracts all report links per company
- Maintains data integrity with unique constraints
- Real-time database saving

### **Professional Output**
- SQLite database with indexed tables
- CSV export with proper encoding
- Session tracking for audit trails
- Comprehensive logging

## 🗄️ Database Schema

### **financial_reports**
| Column | Type | Description |
|--------|------|-------------|
| publish_date | TEXT | When report was published |
| company_name | TEXT | Company name (Hebrew) |
| report_period | TEXT | Quarter/Year (e.g., "רבעון 2 2025") |
| report_links | TEXT | JSON array of download links |
| session_id | TEXT | Scraping session identifier |

### **scraping_sessions**  
| Column | Type | Description |
|--------|------|-------------|
| session_id | TEXT | Unique session identifier |
| started_at | TEXT | Session start time |
| total_reports | INTEGER | Number of reports scraped |
| filters_applied | TEXT | JSON of applied filters |
| status | TEXT | completed/failed/running |

## 🔧 Configuration

All settings are in `src/config/maya-tase-config.js`:

```javascript
// Key working selectors
reportListing: {
  reportRows: 'tbody tr',                    // Report rows
  reportLinks: 'td a',                       // Download links  
  companyName: 'tbody tr td:nth-child(2)',   // Company names
  reportPeriod: 'tbody tr td:nth-child(3)',  // Report periods
  reportDate: 'tbody tr td:nth-child(1)'     // Publish dates
},

filters: {
  companyInput: '#company',        // Company search
  quarterSelect: '#group',         // Quarter selection
  yearSelect: '#mat-select-2',     // Year selection
  searchButton: 'button:nth-of-type(1)' // Search button
}
```

## 📈 Sample Results

After running the scraper:
```
=== SCRAPING SUMMARY ===
Total reports scraped: 40
Session ID: maya-session-2025-08-25T09-16-07-154Z

Sample companies extracted:
- רימון ה"ק - רבעון 2 2025
- שגריר רכב ה"ק - רבעון 2 2025  
- אורבניקה (פאלו) ה"ק - רבעון 2 2025
- אאורה ה"ק - רבעון 2 2025
```

## 🛠️ Technical Details

### **Browser Automation**
- Puppeteer with stealth plugin
- Handles Angular Material components
- Waits for dynamic content loading
- Supports Hebrew RTL layout

### **Error Handling**
- Automatic retries for failed requests
- Session recovery after errors
- Comprehensive logging
- Database transaction safety

### **Performance**
- Concurrent data extraction
- Smart pagination detection
- Configurable delays
- Memory-efficient processing

## 🔍 Monitoring

Check scraping progress:
```bash
# View logs
tail -f logs/maya-scraper.log

# Check database
sqlite3 data/maya-tase.db "SELECT COUNT(*) FROM financial_reports"

# Export latest data
sqlite3 data/maya-tase.db ".mode csv" ".output reports.csv" "SELECT * FROM financial_reports"
```

## ⚙️ Environment Variables

Create `.env` file:
```bash
# Maya TASE Configuration  
MAYA_DB_PATH=./data/maya-tase.db
HEADLESS=true
MAX_PAGES_PER_CATEGORY=10
DELAY_PAGE_LOAD=5000
LOG_LEVEL=info
```

## 🎯 Ready for Production

This Maya TASE scraper is **production-ready** with:
- ✅ Tested selectors working with live site
- ✅ Database integration with proper schema  
- ✅ Error handling and recovery
- ✅ CSV export functionality
- ✅ Session management and logging
- ✅ Hebrew text support
- ✅ Angular Material compatibility

You can start scraping Maya TASE financial reports immediately!

## 🤝 Usage Examples

```bash
# Quick test (1 page)
node src/scrapers/maya-tase-scraper.js

# Production run (10 pages with CSV export)
HEADLESS=true MAX_PAGES=10 node src/scrapers/maya-tase-scraper.js

# Debug mode (visible browser)
HEADLESS=false node src/scrapers/maya-tase-scraper.js
```

The scraper will create:
- `data/maya-tase.db` - SQLite database
- `data/maya-reports-[session-id].csv` - CSV export  
- `logs/` - Detailed logs
- `maya-page-screenshot.png` - Debug screenshot