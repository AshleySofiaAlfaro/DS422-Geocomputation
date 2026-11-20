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

**Initial RQ:** How does travel-time access to hospitals and health clinics differ between car and public transport for the elderly population (65+) in Oahu?

From personal observation, I noticed that there are a lot of kupuna who use TheBus, and it made me wonder how easily accessible hospitals and health clinics are for them in the event they don't have their own car or someone to drive them there. It would be interesting to include a vulnerability layer, such as observing disability status and poverty status at a census tract level.

### New research question framing

There are other transportation services that kupuna could use if they ever have a scheduled non-emergency, medical appointment, such as Catholic Charities Hawaii Senior Transportation, Medicaid (MedQUEST) NEMT, and private NEMT providers. For more context, these are what the services provide kupunas:

- [Catholic Charities' program](https://www.catholiccharitieshawaii.org/senior-services/transportation-services-program/) is for seniors 60 and older who live independently, and priority goes to medical trips. However, riders have to be authorized through the City and County of Honolulu's Elderly Affairs Division and register in advance.
- [Medicaid (MedQUEST) NEMT](https://medquest.hawaii.gov/en/members-applicants/quest-integration-coverage/nemt) is a free ride to medically necessary appointments when you have no other way to get there. This only helps people enrolled in a QUEST plan.
- Private NEMT providers cost money, so they only help people who can pay.

Together, these services will definitely help some kupuna, but they leave others out: those who aren't registered, aren't on Medicaid, or can't afford a private ride. Also, having a service available isn't the same as being able to use it — awareness to these services, registration, and advance scheduling can all be barriers to healthcare access. Meanwhile, TheBus is an option that works for anyone, anytime. So, instead of measuring the gap between car and TheBus travel-times to hospitals and clinics on the island, I can instead identify where public transport is the weakest, and who lives there.

**RQ:** Where do older adults who rely on public transit on Oahu have the poorest bus access to hospital and primary care clinics, and how could this inform where supplemental senior transportation services are most needed?

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

**Initial Methods Write-Up:** I will use the ACS data (via `tidycensus`) and sf to build a tract-level dataset of older adult population and households without vehicles (I think the variable is B08201). I may use isochrones (`mapboxapi`) and conduct travel-time analysis to estimate travel times to the nearest facility by car and by TheBus. However, I don't think `mapboxapi` has a transit option, so I may use `tidytransit` instead to compute the estimated travel times, but I won't be able to map them as isochrones. But what is most important is getting the transit travel times so that I could compare it with the car travel times and map the gap between them. Finally, if time permits, I would like to identify priority tracts where large older adult populations, low vehicle access, and poor transit access overlap and possibly do hot spot analysis to test if the tracts cluster geographically.

### Updated methods to match new research question

I will still use ACS data (via `tidycensus`) and `sf` to build a tract-level dataset of older adult population (65+) and older adults without a vehicle.

Using `tidytransit`, I will read TheBus GTFS schedule data and estimate how long a bus trip takes from each stop to a nearest hospital or primary care clinic on a weekday midday. I might link each tract to the nearest bus stop from its center point. (However, a center point is an oversimplification, since people don't all live at the center of a tract, especially if it's a larger tract, so that's a limitation.) If a bus stop is within 400m (\~5 minute walk) from center point, the tract will get that stop's bus travel time. If not, the tract is flagged as having no walkable bus access. This idea is still subject to change as this may not be the most sufficient way to do it.

Then, I might rank each tract on three measures (older adult pop, share of older households without a vehicle, and bus travel time) and combine them into a priority score to identify tracts where large older adult populations, low vehicle access, and poor bus access overlap.

If time permits, I may (1) add an ACS layer on Medicaid coverage among older adults and (2) test whether the priority tracts cluster geographically (is the problem concentrated in one area or scattered?).

------------------------------------------------------------------------

## 4. 3-5 peer-reviewed publications or news articles surrounding my research question

Give the link below. Add a sentence or two on why each source is relevant to your project.

1.  <https://pmc.ncbi.nlm.nih.gov/articles/PMC9738403/> — This paper emphasizes how the development of hospitals and other medical services play a role in the development of sustainable cities and their spatial distribution directly affects the physical health of urban residents. They also took into account the walking time to and from bus stops, which is something I could consider applying to my research.

2.  <https://www.mdpi.com/2220-9964/13/11/403> — This paper examined the accessibility and equity of hospitals for older adults in Shanghai using spatial analysis.

3.  <https://www.nature.com/articles/s44401-025-00028-1#Abs1> — This paper tested the resilience of hospital and clinic placements and assessed travel-time accessibility. For example, they rearranged hospital placements, then marginally reduced hospital placements to see if they would still be easily accessible.

4.  <https://research.hawaii.edu/rhrpc/wp-content/uploads/sites/23/2025/06/UH-RHRPC-FULL-REPORT-Transportation-Project-June-25-2025-Final.pdf?utm_source=miragenews&utm_medium=miragenews&utm_campaign=news> — This UH report looks at how transportation problems keep people in rural Hawaii from getting healthcare, focusing on emergency services, non-emergency rides, insurance coverage, and maternity care. It combines a lit review with interviews of 40 people (providers, insurers, and transportation workers) to show that long distances, unreliable flights and buses, and insurance rules (mostly just Medicaid covers rides) are major barriers.

5.  

------------------------------------------------------------------------
