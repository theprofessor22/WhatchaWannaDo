# WhatchaWannaDo 
A Nashville night planner with the specific goal of helping users find out what shows are going on and where you can get eat, drink, and be merry before or after the show.

Project interface is a Tableau dashboard with the geospatial locations for 7 Nashville music venues<sup>[1](#myfootnote1)</sup> and the locations of every restaurant/bar/liquor store within a half mile of each venue<sup>[2](#myfootnote1)</sup>. The maximum distance from venue for all food/drink locations can be adjusted using a slider. There is a calendar that allows the user to change months/dates and thus the events displayed on the map. Hovering the cursor over the venue name will display a tooltip containing the date, event name, the ticket price, and the show time for that venue<sup>[3](#myfootnote1)</sup>. Clicking on the venue name will bring up a web browser with the event's ticket seller's website. If non-event locations are hovered over the tooltip displays the name of establishment, address, the Yelp categories it falls under, the distance in miles from the nearest venue, and the Yelp star rating. The Yelp categories are also used to make a wildcard filter, allowing users to enter their preferred criteria to narrow the search, for example: 'chicken', 'craft beer', or 'sushi'. 

# Issues

Some websites were not as amenable to being scraped and this would sometimes not become apparent until well into the process. One for Exit/In in Nashville worked well for the first few days until the ticket seller website was changed to one that didn't like robots. Even those amenable were different enough to make it difficult to know what method of extraction could work, at first. The event data scraped isn't uniform or easily cleaned, even among entries within the same website, which makes it difficult to implement some ideas that I'm still working on, such as the ability to filter available events on the dashboard by music genre.

# Future Additions

Hoping to add more venues to the list as well as the ability to search for events by genre and preview the artist's work. 

<sub><a name="myfootnote1">1</a>: <i>Geolocations for venues obtained by first getting the latitude and longitude from Google Maps, then Python- Point from shapely.geometry to make a 'geometry' column and creating a GeoDataFrame.</i></sub>

<sub><a name="myfootnote2">2</a>: <i>The method for creating this GeoDataFrame is similar except the latitudes, longitudes, and any non-event data were taken from the Yelp dataset available here: https://www.yelp.com/dataset/download. Read the dataset into Python and filtered irrelevant data by city and category. Used geopy.distance and a nested For Loop comparing each venue to every location in the dataframe that remained, which narrowed it down to only those locations within a half mile of each venue.</i></sub> 

<sub><a name="myfootnote3">3</a>: <i>Event information was gathered using BeautifulSoup, requests in Python. Each venue website's calendar iterated over to create a list of all event ticket url's and a For Loop over that list to grab all relevant information from each page. All of this data is put into dataframes, which are then cleaned up to ensure uniformity between venues and then concatenated. The result exported as a csv.</i></sub>
