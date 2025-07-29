https://github.com/Senpai-Sama7/ultimate-website-replicator/blob/main/README.md


Ultimate Website Replication Suite v7.0 - The Professional Grade Edition

![alt text](https://img.shields.io/badge/node-%3E%3D18.0.0-brightgreen.svg)


![alt text](https://img.shields.io/badge/License-MIT-yellow.svg)


![alt text](https://img.shields.io/badge/powered%20by-Puppeteer-blue.svg)

A robust, high-performance, and intelligent Node.js tool for comprehensive website replication, archiving, and analysis. This suite is engineered for resilience, efficiency, and respectful crawling of modern web applications.

✨ Key Features

This version integrates cutting-edge web scraping and archiving techniques, making it suitable for professional use cases.

🚀 Core Replication & Performance

True Streaming Pipeline: Assets are streamed directly from the network to disk, minimizing RAM usage and enabling efficient handling of very large files.

Optional Brotli Compression: Significantly reduces the size of text-based assets (HTML, CSS, JS) by applying Brotli compression, saving disk space and bandwidth.

Optimized Image & SVG Handling: Converts images to modern formats (AVIF/WebP) and minifies SVGs on-the-fly, ensuring a lightweight replica.

CSS & HTML Minification: Applies advanced minification techniques to CSS and HTML for leaner output.

🛡️ Network Resilience & Control

Per-Domain Concurrency: Prevents hammering single servers by managing separate, configurable concurrency limits for each domain (main site vs. external CDNs).

Per-Domain Circuit Breakers: Isolates failures. If one external domain becomes unresponsive, its dedicated circuit breaker trips, preventing it from blocking requests to other healthy domains.

Exponential Backoff with Jitter: Intelligently retries failed asset downloads with increasing delays and random jitter, gracefully handling temporary network issues.

Lazy 404 Handling: Caches known failing URLs (e.g., 404s) to avoid redundant re-fetching attempts.

🧠 Advanced Crawling & Discovery

Sitemap.xml Discovery: Automatically finds and parses sitemap.xml (from robots.txt directives and default locations) to discover a comprehensive list of URLs, including those not directly linked.

Intelligent SPA Crawling: Navigates Single Page Applications (SPAs) by simulating user interactions (scrolling, clicking "load more" buttons) and includes cycle detection to prevent infinite loops.

Robots.txt Compliance: Respects robots.txt rules using a spec-compliant parser (robots-parser), ensuring ethical and compliant crawling.

🔄 Integrity & Auditing

Incremental Replication (--incremental): Performs partial updates by loading a previous manifest.json and using ETag and Last-Modified headers to download only changed assets and pages.

Integrity Manifest: Generates a manifest.json containing SHA-256 hashes for all downloaded assets, enabling post-replication verification.

Verification Command: A dedicated CLI command (verify) allows you to re-hash local files and check their integrity against the manifest.

🛠️ Developer Experience

Professional CLI: Powered by yargs, offering clear commands (replicate, verify), options, and auto-generated help text.

Structured Logging: Uses pino for leveled, structured logging, crucial for debugging and monitoring large-scale operations.

Memory Monitoring: Actively monitors memory usage and triggers garbage collection (if enabled) to prevent crashes.

Cross-Platform Compatibility: Automatically polyfills fetch for older Node.js versions (e.g., Node 16 LTS).

📦 Installation

Prerequisites: Ensure you have Node.js (version 18.0.0 or higher recommended for native fetch) and npm installed.

Clone the Repository:

Generated bash
git clone https://github.com/Senpai-sama7/ultimate-website-replicator.git
cd ultimate-website-replicator


Install Dependencies:

Generated bash
npm install
IGNORE_WHEN_COPYING_START
content_copy
download
Use code with caution.
Bash
IGNORE_WHEN_COPYING_END

Note: Puppeteer will automatically download a compatible Chromium browser during installation.

🚀 Usage

The suite provides a command-line interface (CLI) for easy interaction.

Replicate a Website

Use the replicate command to start the mirroring process.

Generated bash
node replicator.js replicate <url> [output_directory] [options]
IGNORE_WHEN_COPYING_START
content_copy
download
Use code with caution.
Bash
IGNORE_WHEN_COPYING_END

Examples:

Basic Replication:

Generated bash
node replicator.js replicate https://example.com ./my-replica
IGNORE_WHEN_COPYING_START
content_copy
download
Use code with caution.
Bash
IGNORE_WHEN_COPYING_END

Replicate with increased crawl depth and responsive screenshots:

Generated bash
node replicator.js replicate https://myspa.com ./spa-archive --depth 3 --responsive
IGNORE_WHEN_COPYING_START
content_copy
download
Use code with caution.
Bash
IGNORE_WHEN_COPYING_END

Incremental update with Brotli compression:

Generated bash
node replicator.js replicate https://myblog.com ./blog-update --incremental --brotli
IGNORE_WHEN_COPYING_START
content_copy
download
Use code with caution.
Bash
IGNORE_WHEN_COPYING_END

Replicate a complex site with specific concurrency settings:

Generated bash
node replicator.js replicate https://complex-site.com ./complex-site --pageConcurrency 2 --baseAssetConcurrency 15 --domainAssetConcurrency 5
IGNORE_WHEN_COPYING_START
content_copy
download
Use code with caution.
Bash
IGNORE_WHEN_COPYING_END
Verify a Replicated Site

Use the verify command to check the integrity of a previously replicated site against its manifest.json.

Generated bash
node replicator.js verify <output_directory>
IGNORE_WHEN_COPYING_START
content_copy
download
Use code with caution.
Bash
IGNORE_WHEN_COPYING_END

Example:

Generated bash
node replicator.js verify ./my-replica
IGNORE_WHEN_COPYING_START
content_copy
download
Use code with caution.
Bash
IGNORE_WHEN_COPYING_END
Get Help

To see all available commands and options:

Generated bash
node replicator.js --help
node replicator.js replicate --help
IGNORE_WHEN_COPYING_START
content_copy
download
Use code with caution.
Bash
IGNORE_WHEN_COPYING_END
⚙️ Configuration

You can configure the replicator's behavior using CLI flags for the replicate command. For more granular control, you can import UltimateWebsiteReplicator and pass an options object directly in your Node.js script.

Option Name	CLI Flag	Type	Default	Description
url	<url>	string	(required)	The target URL to replicate.
outputDir	[outputDir]	string	./replicated-site	The directory where the replicated site will be saved.
maxCrawlDepth	--depth	number	2	Maximum depth for SPA crawling. 0 for main page only.
pageConcurrency	--pageConcurrency	number	4	Maximum number of browser pages to process concurrently.
baseAssetConcurrency	--baseAssetConcurrency	number	10	Max concurrent asset downloads from the main domain.
domainAssetConcurrency	--domainAssetConcurrency	number	3	Max concurrent asset downloads from external domains/CDNs.
maxRetries	--maxRetries	number	3	Number of times to retry a failed asset download.
retryDelayBase	--retryDelayBase	number	1000	Base delay (ms) for exponential backoff retries.
incremental	--incremental	boolean	false	Enable incremental updates (uses ETag/Last-Modified).
crawlSPA	--crawlSPA	boolean	true	Enable crawling of Single Page Applications.
respectRobotsTxt	--respectRobotsTxt	boolean	true	Respect rules defined in robots.txt.
optimizeImages	--optimizeImages	boolean	true	Optimize images (AVIF/WebP conversion, SVG minification).
enableAVIF	--enableAVIF	boolean	true	Enable AVIF image format optimization (falls back to WebP).
minifyCSS	--minifyCSS	boolean	true	Minify CSS content.
captureResponsive	--responsive	boolean	false	Capture screenshots at defined responsive breakpoints.
responsiveBreakpoints	(internal)	array	[{name: 'mobile', ...}, {name: 'desktop', ...}]	Custom responsive breakpoints for screenshots.
enableBrotli	--brotli	boolean	false	Enable Brotli compression for text assets.
downloadExternalAssets	(internal)	boolean	false	Download assets from external domains.
allowedDomains	(internal)	array	[]	List of allowed external domains (e.g., ['cdn.example.com']).
memoryThreshold	(internal)	number	0.85	Memory usage ratio (heapUsed / totalmem) to trigger GC warning.
viewport	(internal)	object	{width: 1920, height: 1080}	Default browser viewport dimensions.
userAgent	(internal)	string	(Chrome default)	User-Agent string for the browser.
timeout	(internal)	number	60000	Default timeout (ms) for page navigation and asset downloads.
💡 Advanced Topics
Incremental Replication

When --incremental is enabled, the replicator will:

Load the manifest.json from the outputDir.

For each asset and page, it will send If-None-Match (with ETag) and If-Modified-Since (with Last-Modified) headers.

If the server responds with 304 Not Modified, the file is skipped, saving bandwidth and time.

Only new or changed files are downloaded and updated in the manifest.

This is ideal for keeping a local replica up-to-date without re-downloading the entire site.

Domain-Based Concurrency

The replicator intelligently manages network requests:

--baseAssetConcurrency: Controls how many assets are downloaded concurrently from the main domain of the target website.

--domainAssetConcurrency: Controls how many assets are downloaded concurrently from each unique external domain (e.g., a CDN, a font server).

This prevents overloading any single server and improves overall download efficiency by parallelizing requests across different hosts.

Brotli Compression

When --brotli is enabled, HTML, CSS, and JavaScript files will be compressed using Brotli and saved with a .br extension (e.g., index.html.br, style.css.br).

To serve Brotli compressed files: Your web server (e.g., Nginx, Apache, Caddy) needs to be configured to:

Check for the .br version of a file when a client sends an Accept-Encoding: br header.

Serve the .br file with the correct Content-Encoding: br header.

If no .br file exists or the client doesn't support Brotli, serve the original uncompressed file.

Memory Management

The replicator includes an active memory monitor. If Node.js is run with the --expose-gc flag (e.g., node --expose-gc replicator.js ...), the monitor can explicitly trigger garbage collection when memory usage approaches a defined threshold (memoryThreshold option), helping to prevent out-of-memory errors on very large crawls.

External Asset Handling

By default, the replicator focuses on the main domain. To include assets from third-party CDNs or other external domains:

Set downloadExternalAssets: true in the options (or modify the code directly).

Optionally, provide an allowedDomains array (e.g., ['fonts.googleapis.com', 'cdnjs.cloudflare.com']) to whitelist specific external domains for download, preventing unwanted assets.

🤝 Contributing

Contributions, issues, and feature requests are welcome! Feel free to check the issues page.

📄 License

This project is MIT licensed.
