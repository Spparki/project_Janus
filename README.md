JANUS - crawler project 

(1) The goal of the project is to code high-efficency web crawler.

(2) The crawler should consist of:

    I - URL FRONTIER
        what ulrs are already known, what urls may be never visited again, what URL to visit next
        Responsibilities: store pending URLS, store visited URLS, prevent duplicates, allow concurrent access
        Data structures: queue (FIFO or priority-based), hash set for visited URLs

    II - SCHEDULER
        decides when a URL may be fetched
        Responsibilities: enforce max current requests, enforce per-domain rate limits, delay requests when necessary

    III - Fetcher
        it performs the actual HTTP requests
        Responsibilities: download html content, measure response time, handle timeouts, capture HTTP status codes

    IV - PARSER
        extracts new URLs from downloaded HTML

    V - STATE MANAGEMENT
        keeps global crawler state

    VI - STATISTICS
        measures how well crawler works
        Metrics: total pages fetched, pages per second, average respons time, error rate, memory usage

    VII - CONTROL AND LIFECYCLE MANAGEMENT
        starts the crawler, stops it safely, handles shutdown, 

        Parts run concurrently, not sequentially. 

(3) Basic parameters of planned system:
    I - STOP CONDITIONS
        max pages: 1 000 - 10 0000
        max depth: 3-5 link hops from seed 
        time limit: 5-15 minutes or queue exhaustion

    II - CONCURRENCY
        20-100 concurrent requests (start with 20-30)
        1-2 concurrent requests per domain

    III - RATE LIMITING
        delay between requests per domain: 500ms - 2s

    IV - URL FILTERING RULES
        accept only: http:// or https://, valid hostnames, non-binary content
        reject: mailto:, tel:, ftp:, .pdf, .jpg, .zip, .png, URLs with excessive query parameters

    V - MEMORY USAGE
        < 300 MB for 5 000 pages

    VI - PERFORMANCE
        10-50 pages per second
        metrics crucial to report: total pages fetched, success vs failure count, average response time, pages per second, 
        peak memory usage, number of unique domains
--------------------------------------------------------------------------------
MILESTONES:

- 1 - 
    Input:
        one URL (hardcoded or via CLI)
    Download:
        Fetch raw bytes
        Capture:
            HTTP status
            Headers
            Body
    Parse:
        Interpret content as text (for now)
        Extract outgoing links
    Output:
        Normalized list of URLs
        Printed or saved somewhere