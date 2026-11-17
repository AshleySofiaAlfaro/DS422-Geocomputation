# DS 422 Geocomputation – Final Project Proposal

**Name:** Ashley Sofia Alfaro

**Date:** Nov 17, 2026

------------------------------------------------------------------------

Fill this out before you start on your analysis. Write your answers under each question. A few sentences is fine for most of them. Be specific, though: "I'll look at land use" is too vague, but "I'll compare sugar land change across Maui from 2001 to 2021" is better.

Download this file and add it to your DS422 Repository, then edit right in the github browser.

------------------------------------------------------------------------

## 1. My research question

What do you want to find out? Phrase it as a question. Mention the place and time period if they are relevant.

<!-- Write your answer below this line -->

**RQ:** How does travel-time access to hospitals and health clinics differ between car and public transport for the elderly population (65+) in Oahu?

From personal observation, I noticed that there are a lot of kupunas who use TheBus, and it made me wonder how easily accessible hospitals and health clinics are for them in the event they don't have their own car or someone to drive them there. It would be interesting to include a vulnerability layer, such as observing disability status and poverty status at a census tract level.

------------------------------------------------------------------------

## 2. The dataset(s) I will use to approach my research question

List each dataset and where it comes from (agency, website, link). Note the format (shapefile, raster, CSV with coordinates, etc.) and the spatial and temporal coverage if you know it.

<!-- Write your answer below this line -->

- [HonoluluGIS](https://honolulu-cchnl.opendata.arcgis.com/datasets/hospitals-and-clinics/explore?location=21.474750,-157.942850,10): Locations of hospitals and clinics. This could be downloaded as a GeoJSON file.
- [HonoluluGIS](https://honolulu-cchnl.opendata.arcgis.com/datasets/bus-routes/explore?location=21.381248%2C-157.925971%2C11): Bus Routes for the City and County of Honolulu
- [TheBus](https://www.thebus.org/transitdata/production/previous.asp): Previous GTFS schedule feed files
- American Community Survey Data (accessed via `tidycensus`)
- US Census Tracts

------------------------------------------------------------------------

## 3. The specific geocomputation techniques I will use to answer my research question

What methods will you actually run? For example, image segmentation, spatial statistics, time series analysis etc.

<!-- Write your answer below this line -->

I will use the ACS data (via `tidycensus`) and sf to build a tract-level dataset of older adult population and households without vehicles (I think the variable is B08201). I may use isochrones (`mapboxapi`) and conduct travel-time analysis to estimate travel times to the nearest facility by car and by TheBus. However, I don't think `mapboxapi` has a transit option, so I may use `tidytransit` instead to compute the estimated travel times, but I won't be able to map them as isochrones. But what is most important is getting the transit travel times so that I could compare it with the car travel times and map the gap between them. Finally, if time permits, I would like to identify priority tracts where large older adult populations, low vehicle access, and poor transit access overlap and possibly do hot spot analysis to test if the tracts cluster geographically.

------------------------------------------------------------------------

## 4. 3-5 peer-reviewed publications or news articles surrounding my research question

Give the link below. Add a sentence or two on why each source is relevant to your project.

1.  <https://pmc.ncbi.nlm.nih.gov/articles/PMC9738403/> — This paper emphasizes how the development of hospitals and other medical services play a role in the development of sustainable cities and their spatial distribtuion directly affects the physical health of urban residents. They also took into account the walking time to and from bus stops, which is something I could consider applying to my research.

2.  <https://www.mdpi.com/2220-9964/13/11/403> — This paper examined the accessibility and equity of hospitals for older adults in Shanghai using spatial analysis.

3.  <https://www.nature.com/articles/s44401-025-00028-1#Abs1> — This paper tested the resilience of hospital and clinic placements and assessed travel-time accessibility. For example, they rearranged hospital placements, then marginally reduced hospital placements to see if they would still be easily accessible.

4.  

5.  

------------------------------------------------------------------------
