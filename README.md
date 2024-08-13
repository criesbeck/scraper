# Overview

A barebones configurable web-scraper. Upload a configuration file describing what web sites to 
visit and what information to extract. Download spreadsheets of the scraped data.

# Installation

No server is involved. You can use this Github-hosted page, or download ``index.html`` and
``styles.css`` and run ``index.html`` locally.


# Configuration

You specify web-scraping information with an Excel spreadsheet.  Each page of the spreadsheet 
describes how to scrape one URL. When the spreadsheet is uploaded, all URLs will be visted and the scraped data 
will be displayed, along with links to each web site and a button to download the scraped data for
each web site.

Here's an example table to scrape events at [the Chicago Public Libraries](https://chipublib.bibliocommons.com/v2/events).

<table>
  <thead>
    <tr>
      <td>_Site</td>
      <td>Chicago Public Libraries</td>
      <td></td>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>_URL</td>
      <td>https://chipublib.bibliocommons.com/v2/events</td>
      <td></td>
    </tr>
    <tr>
      <td>_Root</td>
      <td>.events-details-container</td>
      <td></td>
    </tr>
    <tr>
      <td>Title</td>
      <td>.cp-event-title h3 .cp-link span</td>
      <td>.cp-event-title h3 .cp-link</td>
    </tr>
    <tr>
      <td>Date</td>
      <td>.cp-event-date-time span[aria-hidden=true]</td>
      <td></td>
    </tr>
    <tr>
      <td>Location</td>
      <td>.cp-event-location span</td>
      <td></td>
    </tr>
    <tr>
      <td>Tags</td>
      <td>.cp-event-taxonomies li a span</td>
      <td></td>
    </tr>
  </tbody>
</table>

The first three rows are special:
 - ``_Site`` gives a title for the site, e.g., "Chicago Public Libraries"
 - ``_URL`` gives the URL for the site.
 - ``_Root`` gives a CSS selector that points to the root of a unit of data to collect.

Every piece of HTML retrieved by ``_Root`` becomes a data row. In this case, the ``_Root``
extracts the smallest root of the HTML that describes an event at the library.

The remaining configuration rows specify what data to extract from each retrieved HTML.
In this case, the Title, Date, Location, and Tags will be extracted, using the given CSS selectors.
Normally only one CSS selector is needed  but the above site is an 
example where the title might be nested in two different ways. The first selector that works is used. 

For the above example, the downloadable spreadsheet will look like this:

|Title                                               |Date               |Location       |Tags                    |
|----------------------------------------------------|-------------------|---------------|------------------------|
|CHIRP Radio Presents: Mini CHIRP Music Film Festival|Saturday, August 17|Sulzer Regional|Summer at CPL           |
|Learn Basic Computer Skills                         |Tuesday, August 13 |South Chicago  |Computers and Technology|
|Lunch and Chill                                     |Tuesday, August 13 |South Shore    |Health and Science      |
|Tech Tuesdays: Blackstone Computer Class            |Tuesday, August 13 |Blackstone     |Computers and Technology|
|Film Screening: Godzilla vs. Kong 2021              |Tuesday, August 13 |Brainerd       |Community Cinema        |
|Programs and Training With YWCA Metropolitan Chicago|Tuesday, August 13 |Pullman        |Jobs and Careers        |

# Libraries Used

 - [Bootstrap v5](https://getbootstrap.com/docs/5.0/getting-started/introduction/)
 - [SheetJS](https://sheetjs.com/)