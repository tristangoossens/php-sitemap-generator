## Sitemap generator

---

Object based PHP script that generates a XML sitemap with the given config options. I made this script because I wanted to automate making a sitemap for google indexing and because there were not a lot of open source sitemap generators out there.

Sitemap format: [http://www.sitemaps.org/protocol.html](http://www.sitemaps.org/protocol.html)

### Features

Feel free to help me implement any of the missing features or add extra features

- [x] Generate a sitemap for your website
- [x] Multiple options for generating sitemaps
- [ ] Option to only look through certain filetypes
- [ ] Load client side Javascript content when crawling
- [ ] Parse all relative link types (// , # , ?) and more

### Installation

Installing this script is simply just downloading both `sitemap_config` and `sitemap_generator` and placing them into your project(same directory).

### Usage

After installing the script you can use the script by including it into your script

```php
include "/path/to/sitemap-generator.php";
```

And initializing the class by calling the constructor

```php
// Create an object of the generator class passing the config file
$smg = new SitemapGenerator(include("sitemap-config.php"));
// Run the generator
$smg->GenerateSitemap();
```

### Config

You can alter some of the configs settings by changing the config values.

```php
// Site to crawl and create a sitemap for.
// <Syntax> https://www.your-domain-name.com/ or http://www.your-domain-name.com/
"SITE_URL" => "https://student-laptop.nl/",

// Boolean for crawling external links.
// <Example> *Domain = https://www.student-laptop.nl* , *Link = https://www.google.com* <When false google will not be crawled>
"ALLOW_EXTERNAL_LINKS" => false,

// Boolean for crawling element id links.
// <Example> <a href="#section"></a> will not be crawled when this option is set to false
"ALLOW_ELEMENT_LINKS" => false,

// If set the crawler will only index the anchor tags with the given id.
// If you wish to crawl all links set the value to ""
// <Example> <a id="internal-link" href="/info"></a> When CRAWL_ANCHORS_WITH_ID is set to "internal-link" this link will be crawled
// but <a id="external-link" href="https://www.google.com"></a> will not be crawled.
"CRAWL_ANCHORS_WITH_ID" => "",

// Array with absolute links or keywords for the pages to skip when crawling the given SITE_URL.
// <Example> https://student-laptop.nl/info/laptops or you can just input student-laptop.nl/info/ and it will not crawl anything in that directory
// Try to be as specific as you can so you dont skip 300 pages
"KEYWORDS_TO_SKIP" => array(
    "http://localhost/student-laptop/index", // I already have a href for root ("/") on my page so skip this page
    "/student-laptop/student-laptop.nl/", // Invalid link example
),

// Location + filename where the sitemap will be saved.
"SAVE_LOC" => "sitemap.xml",

// Static priority value for sitemap
"PRIORITY" => 1,

// Static update frequency
"CHANGE_FREQUENCY" => "daily",

// Date changed (today's date)
"LAST_UPDATED" => date('Y-m-d'),
```

### Output

Example output when generating a sitemap using this script

```XML
<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
  <!-- 3 total links-->
  <!-- PHP-sitemap-generator by https://github.com/tristangoossens -->
  <url>
    <loc>https://student-laptop.nl/</loc>
    <lastmod>2021-03-10</lastmod>
    <changefreq>daily</changefreq>
    <priority>1</priority>
  </url>
  <url>
    <loc>https://student-laptop.nl/underConstruction</loc>
    <lastmod>2021-03-10</lastmod>
    <changefreq>daily</changefreq>
    <priority>1</priority>
  </url>
  <url>
    <loc>https://student-laptop.nl/article?article_id=1</loc>
    <lastmod>2021-03-10</lastmod>
    <changefreq>daily</changefreq>
    <priority>1</priority>
  </url>
</urlset>
```
