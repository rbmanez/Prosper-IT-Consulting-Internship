# Python Live Project Sprint 4
## Table of Contents
- Sprint 4 General Information
  - Project Overview
  - List of Technologies Used
  - User Story Overview
- User Story 1: Location Data Redesign
- User Story 2: Restaurant Redesign
- User Story 3: Navbar Hover Upgrade




## Sprint 4 General Information
#### Project Overview
The Space Bar is an interactive Django based site for researching things about space. It uses APIs from NASA and other sources, web scraping from sites like Wikipedia, and packages like BeautifulSoup, Pandas, Selenium, and more.

#### List of Technologies Used
- Python and Django Web Framework
- HTML, CSS, JavaScript
- Bootstrap 4
- Leafletjs and Openstreet API (Map)
- Openweather API (Local Weather Information)
- Django Crispy Forms (Django App for Styling Forms)
- Virtualenv (Python Library)
- VS Code (Code Editor)
- DevOps (Project Management)
- Git (Source Control)
- Slack and Google Meet (Team Communication and Stand Ups)

#### User Story Overview
For each user story I answer the following questions:
1. What is the issue?
2. Why is this an issue? (If applicable)
3. How is the issue resolved?
4. What is the end result?



## User Story 1: Location Data Redesign
[]()

#### What is the issue?
The issue with this story was that the layout for the Location Data App was visually unorganized and. This story required clearly separating each section into their own container and adding their own image or graphic.

This story had optional requirements to include a map of the user's current location and also to include an additional API source for local information.

###### App before fix (top half of the page)
[]()
	
###### App before fix (bottom half of the page)
[]()

#### Why is this an issue?
The reason why the page was visually unorganized is because the previous developer used the home page's "cafe" section as a template and applied it here.

The code's functionality did not trasfer over well to the Location Data template and required more adjustments to make it more visually effective.

###### Location Data App template code before fix (notice `id="cafe"`)
```html
<section id="cafe" class="about-section text-center">
  <div class="container">
    <div class="row">
      <div class="col-lg-6 mx-auto">
        <h2 class="text-white mb-4">Local Sunrise and Sunset</h2>
        <p class="text-white-50">Below are the local sunrise and sunset times based on your location! These times are for the current date.</p>
          <div class="sunrise-display">
              <h2 class="text-white mb-4">Sunrise</h2>
              <p class="text-white-50">{{ sunrise }}</p>
          </div>
          <div class="sunset-display">
              <h2 class="text-white mb-4">Sunset</h2>
              <p class="text-white-50">{{ sunset }}</p>
          </div>
      </div>
      <div class="col-lg-6 mx-auto">
        <h2 class="text-white mb-4">Radiation Exposure</h2>
        <p class="text-white-50">
          Sources of radiation are all around us all the time. Some are natural and some are man-made. 
          The amount of radiation absorbed by a person is measured in dose. 
          A dose is the amount of radiation energy absorbed by the body.
        </p>
          <div class="sunrise-display">
              <h2 class="text-white mb-4">Dose Rate for {{dateOfRadiation}}:</h2>
              <p class="text-white-50">{{ radiation }}</p>
          </div>
      </div>
    </div>
    <div class="" style="display:inline;color:lightgrey;">
      <strong>{{ latitude }}</strong>, 
      <strong>{{ longitude }}</strong> 
    </div>
    <img class="img-thumbnail" src="../static/images/sunrise.jpg" class="img-fluid" alt="">
  </div>
</section>
```

#### How is the issue resolved?
I fixed the layout by first removing all unnecessary Bootstrap and CSS styling. This removed the black background and revealed the main app's very appealing background that was underneath it, which extended from the main app's base.html.

Then I replaced all of the div tags with semantic tags to give it more structure and meaning. I added an `h1` tag. I added images for each section.

For styling I took a minimalist and clean approach. I used Bootstrap 4's `.container`, `.row`, and `.column` for layout structure. The project already had global styles for the `h1`, `h2`, and `p` tags so I used those as well to keep a uniform look with the rest of the site.

Then I created CSS classes specific to only the Data Location App to fix margin spacing, font size, and to style the map that I created for one of the optional requirements.
	
###### Location Data App template's code
```html
<!-- LOCATION DATA PAGE -->
<main class="container">
  <h1 id="location-data">Location Data</h1>
  <!-- top row section -->
  <section class="row location-data-section">
  <!-- left side article of top row for sunrise/sunset -->
  <article class="col-md-5">
    <h2 class="location-data-heading">Local Sunrise/Sunset</h2>
    <p>Below are the local sunrise and sunset times based on your location! These times are for the current date.</p>
    <p>Sunrise: {{ sunrise }}</p>
    <p>Sunset: {{ sunset }}</p>
    <img class="img-thumbnail" src="../static/images/sunrise.jpg" alt="sunrise">
  </article>
  <!-- right side article of top row for radiation -->
  <article class="col-md-5 offset-md-2">
    <h2 class="location-data-heading">Radiation Exposure</h2>
    <p>
    Sources of radiation are all around us all the time. Some are natural and some are man-made. 
    The amount of radiation absorbed by a person is measured in dose. 
    A dose is the amount of radiation energy absorbed by the body.
    </p>
    <p>Dose Rate for {{dateOfRadiation}}:</p>
    <p>{{ radiation }}</p>
    <img class="img-thumbnail" src="../static/images/radiation.jpg" alt="radiation">
  </article>
  </section>
  <!-- bottom row section -->
  <section class="row location-data-section">
  <!-- left side article of bottom row for map -->
  <article class="col-md-5">
    <h2 class="location-data-heading">Map Location</h2>
    <p>This is your current location on the map.</p>
    <div id="location-data-map"></div>
  </article>
  <!-- right side article of bottom row for local weather -->
  <article class="col-md-5 offset-md-2">
    <h2 class="location-data-heading">Local Weather</h2>
    <p>Below is the current weather for your local area.</p>
    <img src="http://openweathermap.org/img/wn/{{ icon }}@2x.png" alt="weather icon">
    <p>Weather Description: {{ weather_description }}</p>
    <p>Average Temperature: {{ average_temp }} &#8457</p>
    <p>High Temperature: {{ high_temp }} &#8457</p>
    <p>Low Temperature: {{ low_temp }} &#8457</p>
    <p>Humidity: {{ humidity }}%</p>
  </article>
  </section>
</main>
```

###### CSS styles specific to only the Location Data App from static/styles.css
```css
/* LOCATION DATA STYLE */

/* map */
#location-data-map {
  position: relative;
  border: 5px solid white;
  border-radius: 5px;
  height: 300px;
  width: 100%;
}

/* h1 */
#location-data {
  margin: 20rem 0 20rem 0;
}

/* section tag */
.location-data-section {
  margin: 10rem 0 5rem 0;
}

/* h2 */
.location-data-heading {
  font-size: 1.8rem;
  margin-bottom: 3rem;
}

/* LOCATION DATA STYLE ENDS */
```

As for the optional requirements, I incorporated Openweathermap API as a source of local weather data and signed up to acquire the API key.

Inside the views, there was already two functions (`User_Latitude` and `User_Longitude`) that used IP-API to return the user's location coordinates (used for the `RadiationExposure` function).

I used those two functions to pass the user's latitude and longitude values into my `local_weather` function.

From the Openweathermap API's JSON object response, I extracted the values for weather description, average temp, high temp, low temp, humidity, and the weather icon code.

I wrapped all of this data into a dictionary to be returned. From the `index` function, I updated the `context` with the `local_weather`'s data to be rendered and used in the template using django template tags.

###### `local_weather` function from the views
```python
def local_weather(latitude, longitude):
  api_key = "api_key_hidden_for_privacy"
  # make api request
  response = requests.get("https://api.openweathermap.org/data/2.5/weather?lat=" + latitude + "&lon=" + longitude + "&appid=" + api_key)
  # "main" and "weather" are JSON object keys
  main = response.json()["main"]
  weather = response.json()["weather"][0]
  # the next 6 lines are JSON object key values
  weather_description = weather["description"].capitalize() + "."
  average_temp = kelvin_to_fahrenheit(main["temp"])
  high_temp = kelvin_to_fahrenheit(main["temp_max"])
  low_temp = kelvin_to_fahrenheit(main["temp_min"])
  humidity = main["humidity"]
  icon = weather["icon"]
  context = {
    "weather_description": weather_description,
    "average_temp": average_temp,
    "high_temp": high_temp,
    "low_temp": low_temp,
    "humidity": humidity,
    "icon": icon,
    # latitude_only and longitude_only is for map
    "latitude_only": latitude,
    "longitude_only": longitude
  }
  return context
```

###### `index` function from the views (I added lines 5 and 6)
```python
def index(request):
  location = User_Location()
  context = suntracker(location)
  context.update(RadiationExposure())
  # update context with data from local_weather method
  context.update(local_weather(User_Latitude(), User_Longitude()))
  return render(request, 'my_Location/my_LocationData.html', context)
```

The temperature values returned from Openweathermap API was in Kelvin. I created a function to convert Kelvin to Fahrenheit, then returned that value as a string so it can be used in the template.

###### `kelvin_to_fahrenheit` function from the views
```python
def kelvin_to_fahrenheit(k_temp):
  # convert kelvin to fahrenheit and round
  f_temp = round((k_temp-273.15)*9/5+32)
  # return fahrenheit as string
  return str(f_temp)
```

For some reason, the `User_Latitude` and `User_Longitude` functions (created by a previous developer) were producing user's location coordinates for West Chicago when it should've been for my location in Colorado Springs.

I brought this to the project manager's attention and she said the issue may be the IP-API itself or the way the previous developer incorporated it. Either way, I was instructed to go ahead and continue to use those functions and she will create a new user story to handle that issue.

I accomplished the other optional requirement of including a map of the user's current location by using Leafletjs and Openstreet API. I used the pre-existing `User_Latitude` and `User_Longitude` functions to get the user's coordinates for the map.

###### Required link and script tags for leaflet map
```html
<!-- Include Leaflet CSS file -->
<link rel="stylesheet" href="https://unpkg.com/leaflet@1.5.1/dist/leaflet.css"
  integrity="sha512-xwE/Az9zrjBIphAcBb3F6JVqxf46+CDLwfLMHloNu6KEQCAWi6HcDUbeOfBIptF7tcCzusKFjFw2yuvEpDL9wQ=="
  crossorigin=""/>
<!-- Include Leaflet JavaScript file after Leaflet’s CSS -->
<script src="https://unpkg.com/leaflet@1.5.1/dist/leaflet.js"
  integrity="sha512-GffPMF3RvMeYyc1LWMHtK8EbPv0iNZ8/oTtHPx9/cc2ILxQ+u905qIwdpULaqDkyBKgOaB57QTMg7ztg8Jm2Og=="
  crossorigin=""></script>
```

###### JavaScript code for creating the map
```html
<!-- JAVASCRIPT FOR LOCATION DATA'S MAP -->
<script>
  // Create map options
  var mapOptions = {
  center: [parseFloat("{{ latitude_only }}"), parseFloat("{{ longitude_only }}")],
  zoom: 10
  }
  // Create map object
  var map = new L.map('location-data-map', mapOptions);
  // Create Layer object
  var layer = new L.tileLayer('http://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
  attribution: '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors'});
  // Add layer to the map
  map.addLayer(layer);
  // Create marker and add it to map
  var marker = L.marker([parseFloat("{{ latitude_only }}"), parseFloat("{{ longitude_only }}")]).addTo(map);
</script>
```

###### CSS styling for the map
```css
/* map */
#location-data-map {
  position: relative;
  border: 5px solid white;
  border-radius: 5px;
  height: 300px;
  width: 100%;
}
```

#### What is the end result?
The end result is a visually structured, appealing, and functional page for Location Data. The page looks uniform with the rest of the site and it includes data for user location's sunrise/sunset time and radiation exposure.

It now also includes the new features I added: user's local map location and weather data.

###### App after fix (top third of the page)
[]()

###### App after fix (middle third of the page)
[]()

###### App after fix (bottom third of the page)
