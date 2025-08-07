# U-TURN: the transit transformation denounced as a disaster

_This project analysed changes in public transit access — particularly bus stop locations and frequent service routes — following the implementation of Winnipeg Transit’s new route network. Here's how._

_By Julia-Simone Rutgers_
_Aug 2025_

---

### Why do this investigation?

On June 29, Winnipeg Transit overhauled its bus network practically overnight — the largest single-day change in the service’s 142-year history. 

The city’s goal is to make transit more convenient and accessible by streamlining the network, adding more frequent routes and upgrading infrastructure. 

One month after rolling out the Primary Transit Network, however, public reviews have been mixed.

Many complaints centre on the fact the city removed more than 1,700 bus stops and cut more than a dozen routes as part of its streamlining efforts. For some riders, that’s meant longer walks to the bus stop, more transfers and more waiting in the elements. (The city also added 450 stops, for a net loss of 1,265 bus stops.)

But the city did not release data showing exactly where stops were removed from. One opinion in the Winnipeg Free Press noted transit users in the city’s North End felt particularly disadvantaged by the cuts, which anecdotally seemed more significant in the historically less-affluent neighbourhood compared to wealthier, southern parts of town. Other anecdotal reports echoed this claim, noting it was more complicated to get to the north end via transit.

This project set out to test that theory, understand exactly where the stops had been removed from and whether there was correlation between the demographics of people who need transit most and the number of bus stops cut from service. 

It also set out to analyse whether those stop removals had worked as the city intended by improving access to frequent transit. 

---

### What’s included in the final product?

The project centres around a series of maps showing the change in bus stops per square kilometre in each of the city’s census tracts, and the proportion of residents in those same areas who A - live below the poverty line and B - regularly commute via public transit, according to the 2021 Census.

It also features maps showing the change in stop locations between the original and updated networks, and maps that outline the parts of the city within walking distance of frequent transit service before and after the route overhaul.

#### In this repo:

**Notebooks:**

[Spatial Analysis using Pandas and Geopandas](notebooks/01_transit_change_geographic_analysis.ipynb)

[Transit headway (frequency) analysis using R](notebooks/02_transit_frequency_analysis/transit-frequency-analysis.Rmd)

[Basic compiling and cleaning of census data](notebooks/03_transit_census_data_compiling/census-mapping-transit.ipynb)

**Data Folders:**

[Transit Data for the original network](old_network/)

[Transit Data for the new network](new_network/)

["Scraped" ward-level census data (in xlsx)](ward_data/)

[Final datasets used for QGIS mapping](data_output/)

---

### What were the results?

Between the old network and new network, there are 2.7 fewer bus stops per km2 across the entire city. On average, the city removed 3.6 stops and added one stop per km2.

As the rate of people living below the poverty line increases, so too does the number of stops removed.

In high-needs areas of the city, where the proportion of residents below the poverty line  is between 20 and 29 per cent, there are now 6.7 fewer bus stops per km2.

Areas where at least 30 per cent of residents live below the poverty line have lost nearly 8 stops per km2, more than twice the city average.

There’s a similar pattern when it comes to the neighbourhoods who use transit most.
In areas of the city, where the transit commuters make up between 20 and 29 per cent of the population there are now 5.7 fewer bus stops per km2.

While areas where more than 30 percent of the population commute via transit have lost nearly 12 stops per km2. That's more than 4 times the city-wide average.

However, access to frequent transit service has improved. The portion of the population within a 15-minute walk of a bus stop delivering frequent service (defined as buses that arrive at least every 15 minutes) has increased by nearly 70 per cent.

---

### Where did the data come from?


Bus stop locations were sourced from the General Transit Feed Specification, an open-source database that allows transit networks to publish schedules and real-time data in a standardized format. 

For the purposes of this project, I selected two Winnipeg transit feed specifications to represent the original and new route networks respectively. Each feed data set included text files listing: 


-   The applicable service dates, including dates where service was altered as a result of holidays or other exceptions
-   The location, number and name of all bus stops 
-   The name and number of each bus route
-   The path of each bus trip (a segment of a route specific often specific to the day of the week, time of day and direction of travel)
-   The schedule for each stop


Census data was sourced from Statistics Canada’s Census Program Data Viewer. I selected the Census Tract geographic level — the smallest available — for the Winnipeg Census Metropolitan Area (CMA) and selected the following indicators from the 2021 Census:

- Population change between 2016 - 2021
- Population density 
- Percentage of population commuting on public transit
- 2020 poverty rate


Council level census data — including the same indicators used for census tract analysis — was sourced from the City of Winnipeg, which released census data summaries for each ward. I used a bit of browser automation to gather the ward-level census data from the municipal website. This was entirely unneccessary, as all I had to do was click download for each of the 15 files. But I wanted to practice.

---

### How was the analysis conducted?

This page is an abridged version of the full methodology, which includes several links, explanations of data limitations and a somewhat exhaustive (exhausting?) breakdown of the analysis process. 

In short, I used geopandas and QGIS to determine the net change in stops for each census tract, then merged these stop changes with census data regarding poverty rates and transit use, and analysed trends between the data sets. 

I also used QGIS' service area feature to calculate the area within a 10 or 15 minute walk of frequent transit in both the new and original networks. 

(Determining which routes counted as "frequent" on the original transit network required analyzing the GTFS data using the R tidytransit package.)

---

### What would I have done differently?

If you are a fellow LEDE Student, a TA or Soma himself, you may notice I ignored the advice to avoid unweildy projects about current events. I understand now why that advice was doled out, but I have absolutely no regrets. This project had been turning in my mind for months, and every time I tried to start something else, this was all I really wanted to be working on. So I did it. 

Looking back, there are small things I would have done differently — using different geographic levels for analysis here and there, picking different measures of poverty, spending a bit more time refining my statistical analysis, learning enough CSS to make my website as cool as I dreamed it could be. None of those things feel especially important. What this project taught me, more than anything, was how to just...figure it out. There were a few iterations of this project in the early stages. Every time I hit a significant roadblock, I put it down for a day or two, worked on something else, then researched a path forward and discovered there was a better, more efficient process out there. For example, I practically stumbled upon the General Transit Feed Specification, I learned R _just_ in time to discover there was a package that could help with the part of the analysis that had most frustrated me, and I had been absolutely baffled by Javascript and D3 until I decided I _had_ to make my scrolling map vision a reality and, well, figured it out. This project is a testament to being stubborn, at least sometimes.

The big vision for this project (which I will carry out soon, mark my words) will involve making a little interactive where users can input two addresses and see how the transit travel between these locations has changed — how long they have to walk for, how many transfers are needed, and how often the buses come. Thanks to all the figuring it out, I have a muddy idea of how I could approach this...and that feels like enough to give it a go.
