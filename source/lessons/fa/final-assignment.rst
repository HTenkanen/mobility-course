Final assignment
================

.. admonition:: Start your final report here

    Start by **downloading the Jupyter Notebook template** for your final report from :doc:`this page <final_assignment>`.

The final assignment is a small research project of your own. You use open data and the tools of this course to study
**spatial accessibility** from social and/or environmental perspectives: how well people can reach the places they need, how much greenhouse-gas emissions
and money their trips cost, and how fairly these benefits and burdens are shared between people and places.
You choose the city, the topic and the questions.

What should you do?
-------------------

Pick a city or region and a question about accessibility that interests you, and answer it with your own analysis.
The topic ideas below show what you can study with ``cafein`` and ``transitio``, the libraries we used in
:doc:`Tutorial II <../L2/cafein_tutorial>` and :doc:`Tutorial III <../L2/cafein_munich>`.
They are suggestions: you can combine them, apply them to any city, or propose a topic of your own.

A good project:

- asks a clear question that matters for the people who live in the area,
- compares something: places, population groups, travel modes, times of the day, or the situation before and after a change,
- looks at more than one side of accessibility, e.g. travel time and emissions, or travel time and how access is shared between population groups,
- discusses the limitations of the data and the methods, and what they mean for the results.

Topic ideas
-----------

Every idea below also works as a comparison between two or more cities: ``transitio`` downloads the same kinds of data for
any place it finds in its feed index.

**Time, emissions and money**

- Which travel mode is the fastest, the cleanest and the cheapest to each part of the city, and where do the answers disagree?
  Calculate travel cost matrices for public transport, cycling and driving (``cafein.TravelCostMatrix``), and add the
  money costs: public transport fares (``cafein.fares``) and the private and societal costs of cycling and driving per
  kilometer (``cafein.costs``).
- How much slower are the cleanest public transport journeys than the fastest ones? Look at the trade-off between travel
  time, emissions and fares with ``cafein.journey_frontier`` or ``cafein.DetailedItineraries(candidates="pareto")``.
- Notice that not every city provide information about the public transport ticket prices. ``cafein`` will raise an error 
  if the GTFS feed does not include this information.

**Accessibility within a carbon budget**

- How many jobs, schools or grocery stores can people reach within 30 minutes, and how many within an emissions budget of,
  say, 500 g CO₂e? Where in the city do the two answers differ the most? ``cafein.Accessibility`` counts the reachable
  destinations within a time, an emissions or a money budget (the emissions and money budgets need a departure time window).

**Who gets access?**

- How unequally is the access to health care, jobs or green areas shared between the residents, and do the residents with
  lower incomes have better or worse access? ``cafein.equity`` calculates inequality measures such as the Gini index,
  the Palma ratio and the concentration index, and draws Lorenz curves.
- Where do poor access and high transport costs come together? ``cafein.equity`` also measures the transport cost
  burden, i.e. the share of income that people spend on travel.

**Different travelers**

- How does the access to services change for people who use a wheelchair, or for older people who walk more slowly?
  A ``cafein.TravelerProfile`` describes the traveler: with ``wheelchair=True``, ``cafein`` uses the accessibility
  information of the GTFS feed, and ``walking_speed_kmph`` and ``max_walking_time`` set the walking speed and the
  longest walk.

**Combining travel modes**

- How much does taking a bike, an e-bike or an e-scooter to the station improve access compared with walking?
  And does park-and-ride save emissions compared with driving all the way? See ``cafein.StreetLegPolicy`` and
  ``cafein.policy.CarParkPolicy``; ``cafein.streets.park_and_ride_facilities`` finds the park-and-ride sites
  from OpenStreetMap.

**Healthy and pleasant trips**

- How much time do children spend in high noise or poor air quality on their way to school, and are there routes that avoid
  them? ``cafein.Exposure`` adds your own exposure layers, e.g. noise maps or air quality data, to the street network.
- How much do hills slow down cycling, and who is affected? Give ``cafein.StreetNetwork.from_osm()`` an elevation model
  with the ``dem`` parameter, as in Tutorial II.

**Changes over the day and the week**

- How does access change between the morning rush hour, the evening and the weekend? With a ``departure_time_window``,
  ``cafein`` calculates the results for every minute of the window and reports them as percentiles.

Data
----

**Download the data with transitio.** As in Exercise 2, ``transitio.fetch(place=...)`` downloads the public transport
timetables (GTFS) that serve a place, together with the OpenStreetMap data of the area, and ``transitio.fetch_pbf()``
downloads only the OpenStreetMap data. To see which feeds serve your area, look the place up in the feed index of
``transitio``, as in Tutorial III. The feed index is downloaded once and takes about 420 MB.

**Use the ready-made data of Helsinki.** ``cafein.sampledata.helsinki`` contains the timetables, OpenStreetMap data and
an elevation model of the Helsinki region, as well as a population grid, income statistics by postal code area,
destinations by category, noise zones, air quality, street-level greenery and the population present in each area
over the day. This makes Helsinki a good choice for projects on equity or exposure.

Other data sources:

- OpenStreetMap data: `Geofabrik <https://download.geofabrik.de/>`__ (countries and regions) and
  `BBBike <https://extract.bbbike.org/>`__ (cities, or an area that you draw yourself).
- Public transport timetables (GTFS): the `Mobility Database <https://mobilitydatabase.org/>`__,
  `Transitland <https://www.transit.land/>`__ and `GTFS.de <https://gtfs.de/>`__ (Germany).
- Destinations: OpenStreetMap, e.g. with ``osmnx`` or ``pyrosm``.
- Population: the `2022 census of Germany <https://www.destatis.de/DE/Themen/Gesellschaft-Umwelt/Bevoelkerung/Zensus2022/_inhalt.html>`__
  publishes its results on a grid, and the `Global Human Settlement Layer <https://human-settlement.emergency.copernicus.eu/download.php>`__
  provides population grids for the whole world.
- `Open geodata of Bavaria <https://geodaten.bayern.de/opengeodata/>`__.

**Emission factors.** The default emission factors of ``cafein`` are calibrated to the Finnish electricity mix. If your
city is in another country, calculate local factors with ``cafein.lca``, as in Tutorial III.

Practical tips
--------------

- **Start small.** Test your workflow with a few origins and a small area, and scale it up when it works.
- **Mind the memory.** Building the networks for a metropolitan region takes several gigabytes of memory (about 6 GB for
  the Munich data of Tutorial III). Keep your study area at the scale of a city or a region, and crop the data to it with
  ``transitio``. Binder does not have enough memory for these analyses, so work on your own computer.
- **Check the dates.** A GTFS feed is valid only for a limited period. Check it with ``network.service_window``, pick a
  departure time inside it, and report the date in your report.
- **Save your results.** Save the results of long calculations to files (e.g. GeoPackage or Parquet), so that you do not need
  to run them again every time you open your Notebook.

What should be returned?
------------------------

Your report is a Jupyter Notebook that documents your work, results and codes. Write about 10 pages of text (A4);
the code does not count towards the page limit. The template suggests a structure for the report: introduction,
data and methods, analysis and results, discussion, and references.

**Return your work by 31 December 2026 as a single ZIP file via Digicampus.** The ZIP file should contain:

- your report Notebook (``.ipynb``) with all its outputs,
- the same report as a PDF file, exported from JupyterLab (if the PDF export does not work on your computer, export
  the Notebook as HTML and print it to PDF from your browser),
- any other files that your Notebook needs, e.g. your own scripts or small data files that you created (such as the
  route lines of a scenario).

Leave out the large data files that you downloaded (e.g. GTFS and OpenStreetMap data): your Notebook should show how
to download them.
