# Interactive Weather Forecast App

A responsive, browser-based **weather forecasting application** developed as part of the **Software Development Bootcamp — Interactive Website Project**.

The application retrieves live weather and forecast information from the **Open-Meteo APIs**, supports both city search and browser geolocation, presents current conditions plus hourly and seven-day forecasts, visualizes weekly temperatures with Chart.js, and includes light/dark display modes.

**Developer:** Mohsen Ghazel  
**Project:** Software Development Bootcamp — Project #04  
**Application:** Interactive Weather Forecast App  
**Source version:** 28-Mar-2026

---

## Table of Contents

1. [Project Overview](#project-overview)
2. [Objectives](#objectives)
3. [Key Features](#key-features)
4. [Technology Stack](#technology-stack)
5. [Application Architecture](#application-architecture)
6. [Application Workflow](#application-workflow)
7. [Project Structure](#project-structure)
8. [Weather Data and API Integration](#weather-data-and-api-integration)
9. [Core JavaScript Functions](#core-javascript-functions)
10. [Current Weather Display](#current-weather-display)
11. [Hourly Forecast](#hourly-forecast)
12. [Seven-Day Forecast](#seven-day-forecast)
13. [Temperature Chart](#temperature-chart)
14. [Geolocation](#geolocation)
15. [Theme Support](#theme-support)
16. [Responsive UI Design](#responsive-ui-design)
17. [How to Run the Project](#how-to-run-the-project)
18. [Dependencies](#dependencies)
19. [Testing Checklist](#testing-checklist)
20. [Known Limitations](#known-limitations)
21. [Learning Outcomes](#learning-outcomes)
22. [Future Improvements](#future-improvements)

---

## Project Overview

The **Interactive Weather Forecast App** is a client-side web application for retrieving and presenting current and forecast weather information.

Users can search for a city by name or request weather for their current geographic position. City names are converted into latitude and longitude coordinates through the Open-Meteo Geocoding API. The resulting coordinates are then supplied to the Open-Meteo Forecast API.

The application presents:

- Current temperature.
- Current weather condition.
- Weather icon.
- Wind speed.
- Relative humidity.
- UV index.
- Sunrise and sunset.
- Upcoming hourly conditions.
- Seven-day high/low forecast.
- Weekly temperature chart.

The project is implemented entirely in HTML, CSS, and vanilla JavaScript. It does not require a backend server, database, Node.js build process, or application framework.

---

## Objectives

This project demonstrates practical front-end development concepts including:

- Semantic HTML5.
- Modular CSS styling.
- Responsive layouts.
- JavaScript DOM manipulation.
- Event-driven programming.
- Asynchronous programming with `async` / `await`.
- REST API integration with `fetch()`.
- JSON processing.
- URL encoding for user-supplied city names.
- Browser Geolocation API.
- Weather-code interpretation.
- Dynamic HTML generation.
- Date/time formatting.
- Chart.js data visualization.
- Light/dark UI themes.
- Error handling and user feedback.
- Separation of HTML, CSS, and JavaScript concerns.

---

## Key Features

### Search Weather by City

Users can enter a city name and select **Search**.

The application:

1. Validates that a city was entered.
2. Sends the city name to the Open-Meteo Geocoding API.
3. Retrieves the first matching location.
4. Extracts its latitude and longitude.
5. Requests weather data for those coordinates.
6. Displays the returned conditions and forecasts.

---

### Weather for Current Location

The **Use My Location** feature uses:

```javascript
navigator.geolocation.getCurrentPosition()
```

to obtain the user's latitude and longitude.

The coordinates are passed directly to the weather request.

Browser permission is required before location information can be accessed.

---

### Current Weather Conditions

The current-weather panel displays:

- Location.
- Temperature in °C.
- Weather description.
- Weather icon.
- Wind speed in km/h.
- Relative humidity.
- UV index.
- Sunrise.
- Sunset.

---

### 12-Hour Forecast

The application identifies the first forecast time at or after the current time and renders up to the next **12 hourly forecast entries**.

Each hourly card includes:

- Time.
- Weather icon.
- Temperature.
- Relative humidity.

---

### Seven-Day Forecast

The daily forecast displays up to **7 days**.

Each forecast row includes:

- Date/day label.
- Weather icon.
- Daily maximum temperature.
- Daily minimum temperature.

---

### Weekly Temperature Chart

Chart.js is used to visualize daily forecast temperatures.

The chart is generated from Open-Meteo daily data and provides a graphical view of the forecast temperature trend.

---

### Weather-Code Mapping

Open-Meteo weather codes are mapped to intuitive emoji icons.

Examples include:

| Code | General Condition | Icon |
|---:|---|---|
| 0 | Clear sky | ☀️ |
| 1 | Mainly clear | 🌤️ |
| 2 | Partly cloudy | ⛅ |
| 3 | Overcast | ☁️ |
| 45 / 48 | Fog | 🌫️ |
| 61–65 | Rain | 🌧️ |
| 71–75 | Snow | ❄️ |
| 95–99 | Thunderstorm | ⛈️ |

The JavaScript also converts codes into human-readable descriptions.

---

### Light/Dark Theme Toggle

The theme button toggles the page between:

```text
light-mode
dark-mode
```

and changes its label between:

```text
🌙 Dark
☀️ Light
```

---

### Clear Weather

The **Clear** control resets the displayed weather information through the project's `clearWeather()` function.

---

## Technology Stack

| Technology | Purpose |
|---|---|
| **HTML5** | Application structure |
| **CSS3** | Layout, weather cards, themes, responsive design |
| **JavaScript ES6+** | Application logic and dynamic rendering |
| **Fetch API** | Open-Meteo API requests |
| **Async/Await** | Asynchronous API workflow |
| **Open-Meteo Geocoding API** | City-to-coordinate lookup |
| **Open-Meteo Forecast API** | Current, hourly, and daily weather data |
| **Browser Geolocation API** | Current-position weather lookup |
| **Chart.js** | Weekly temperature visualization |
| **Bootstrap 5.3.2** | Responsive utilities and UI support |
| **Google Fonts** | Inter and Poppins typography |

---

## Application Architecture

```text
+-----------------------------+
|        weather_app.html     |
|-----------------------------|
| Search controls             |
| Weather panels              |
| Forecast containers         |
| Chart canvas                |
| Theme controls              |
+-------------+---------------+
              |
              v
+-----------------------------+
|      weather_styles.css     |
|-----------------------------|
| Layout                      |
| Current-weather card        |
| Hourly forecast             |
| Daily forecast              |
| Light/dark themes           |
| Responsive design           |
+-------------+---------------+
              |
              v
+-----------------------------+
|       weather_script.js     |
|-----------------------------|
| Event listeners             |
| Geocoding requests          |
| Forecast requests           |
| DOM updates                 |
| Forecast rendering          |
| Chart rendering             |
| Formatting utilities        |
+-------------+---------------+
              |
              v
+-----------------------------+
|        External APIs        |
|-----------------------------|
| Open-Meteo Geocoding        |
| Open-Meteo Forecast         |
+-----------------------------+
```

---

## Application Workflow

### City Search

```text
User Enters City
      |
      v
Validate Input
      |
      v
Open-Meteo Geocoding API
      |
      v
Latitude + Longitude
      |
      v
Open-Meteo Forecast API
      |
      v
Parse Weather JSON
      |
      v
Update Current Conditions
      |
      +--------------------+--------------------+
      |                    |                    |
      v                    v                    v
Hourly Forecast      Daily Forecast      Temperature Chart
```

### Current Location

```text
User Selects "Use My Location"
      |
      v
Browser Geolocation Permission
      |
      v
Latitude + Longitude
      |
      v
Open-Meteo Forecast API
      |
      v
Render Weather UI
```

---

## Project Structure

```text
swd_interactive_weather_forecast_app_swd_bootcamp_project_04/
|
|-- assets/
|   `-- logo/
|       `-- js-animation.gif
|
|-- css/
|   |-- home_styles.css
|   `-- weather_styles.css
|
|-- js/
|   |-- home_script.js
|   `-- weather_script.js
|
|-- output/
|   `-- weather-app/
|       `-- weather-app.png
|
|-- weather_app.html
`-- .git/
```

### Core Weather Application Files

| File | Responsibility |
|---|---|
| `weather_app.html` | Main application markup, controls, weather panels, forecast areas, chart, footer, CDN imports |
| `css/weather_styles.css` | Weather-specific styling, cards, themes, responsive behavior |
| `js/weather_script.js` | Search, geolocation, API requests, weather rendering, charting, utilities |
| `assets/logo/js-animation.gif` | Animated JavaScript logo used in the application header |
| `output/weather-app/weather-app.png` | Stored project output/screenshot |

The archive also contains `home_styles.css` and `home_script.js`, which support other portfolio/home-page functionality and are not part of the core weather-processing logic.

---

## Weather Data and API Integration

### 1. Open-Meteo Geocoding API

City searches use the Open-Meteo geocoding service.

The project constructs a request based on:

```javascript
https://geocoding-api.open-meteo.com/v1/search
```

with parameters including:

```text
name=<city>
count=1
language=en
format=json
```

The city value is safely incorporated using:

```javascript
encodeURIComponent(city)
```

The first returned location supplies:

- Latitude.
- Longitude.
- Location name.
- Country.

---

### 2. Open-Meteo Forecast API

Forecast data is retrieved from:

```text
https://api.open-meteo.com/v1/forecast
```

The request includes:

```text
latitude
longitude
current_weather=true
hourly=temperature_2m,relativehumidity_2m,weathercode
daily=temperature_2m_max,temperature_2m_min,weathercode,sunrise,sunset,uv_index_max
timezone=auto
```

Using `timezone=auto` allows forecast timestamps to correspond to the requested location's timezone.

---

## Core JavaScript Functions

### `getWeatherByCity(city)`

Coordinates city-based weather lookup.

Responsibilities:

1. Construct the geocoding URL.
2. Encode the city name.
3. Fetch geocoding data.
4. Check the HTTP response.
5. Validate that a location was found.
6. Extract coordinates.
7. Call the main weather-fetch function.
8. Catch errors and provide user feedback.

---

### `getWeatherByCoords(lat, lon, label)`

Handles weather requests when coordinates are already known, such as after browser geolocation.

---

### `fetchWeather(lat, lon, label)`

Builds the Open-Meteo Forecast API request and retrieves:

- Current weather.
- Hourly temperature.
- Hourly relative humidity.
- Hourly weather code.
- Daily maximum temperature.
- Daily minimum temperature.
- Daily weather code.
- Sunrise.
- Sunset.
- Daily maximum UV index.

After successful retrieval, it passes the data to:

```javascript
updateUI()
```

---

### `updateUI(locationLabel, data)`

Acts as the central weather-display coordinator.

It:

1. Makes the hidden weather panel visible.
2. Reads current, hourly, and daily data.
3. Updates current-weather values.
4. Maps the current weather code to an icon.
5. Displays humidity.
6. Displays UV index.
7. Formats sunrise and sunset.
8. Calls `renderHourly()`.
9. Calls `renderDaily()`.
10. Calls `renderChart()`.

---

### `renderHourly(hourly)`

Builds the upcoming hourly forecast cards.

The function:

1. Clears previous hourly content.
2. Locates the first forecast timestamp at or after the current time.
3. Selects up to 12 forecast entries.
4. Dynamically creates a card for each hour.
5. Displays time, icon, temperature, and humidity.

---

### `renderDaily(daily)`

Builds the daily forecast list.

It limits the displayed forecast to:

```javascript
Math.min(7, daily.time.length)
```

and dynamically generates each forecast row.

---

### `renderChart(daily)`

Creates or refreshes the Chart.js weekly temperature visualization using daily forecast values.

The global:

```javascript
let tempChart = null;
```

allows the application to manage the active chart instance when new weather data is displayed.

---

### `clearWeather()`

Resets the weather display and clears the current application presentation.

---

### Formatting Utilities

The project contains dedicated helper functions:

```javascript
formatTimeFromISO()
formatHourFromISO()
formatDateLabel()
formatShortDateLabel()
```

These convert ISO date/time strings into user-friendly labels.

---

### `describeWeatherCode()`

Converts Open-Meteo numeric weather codes into readable weather descriptions.

This separates API-specific numeric values from the text shown to users.

---

## Current Weather Display

The current-weather section combines several API datasets.

### Current Weather Object

The application uses:

```javascript
data.current_weather
```

for values including:

- Temperature.
- Wind speed.
- Weather code.

### Hourly Data

Relative humidity is obtained from the hourly response.

### Daily Data

The current day's daily data supplies:

- UV index.
- Sunrise.
- Sunset.

This demonstrates how multiple API response sections can be combined into one user-facing panel.

---

## Hourly Forecast

The application does not simply display the first 12 entries returned by the API.

Instead, it compares each forecast timestamp with:

```javascript
const now = new Date();
```

and finds the first entry that is at or after the current time.

It then displays up to the next 12 hourly entries.

This makes the forecast more relevant to the user's current time.

---

## Seven-Day Forecast

The daily forecast uses:

- `daily.time`
- `daily.temperature_2m_max`
- `daily.temperature_2m_min`
- `daily.weathercode`

The output is presented as a readable list with daily weather icons and maximum/minimum temperatures.

---

## Temperature Chart

The project includes Chart.js through a CDN and uses it to convert forecast arrays into a visual temperature trend.

This supplements the textual daily forecast with a graphical representation, making temperature changes easier to interpret.

---

## Geolocation

Current-location weather depends on the browser's Geolocation API.

The application first checks:

```javascript
if (!navigator.geolocation)
```

If geolocation is available, it requests the user's position.

Success provides:

```javascript
latitude
longitude
```

which are sent directly to the weather service.

Possible failure conditions include:

- User denies location permission.
- Browser does not support geolocation.
- Position cannot be determined.

The application provides alert-based feedback for these cases.

---

## Theme Support

The project supports light and dark themes by toggling CSS classes on the `<body>` element.

The JavaScript alternates:

```text
light-mode
dark-mode
```

and synchronizes the theme-button text with the active mode.

This keeps theme state implementation simple and entirely client-side.

---

## Responsive UI Design

The application uses custom CSS together with Bootstrap utilities.

Major UI areas include:

- Header/banner.
- Hero area.
- City-search controls.
- Geolocation control.
- Clear control.
- Theme toggle.
- Current-weather card.
- Weather metric cards.
- Horizontal hourly forecast.
- Seven-day forecast list.
- Temperature chart.
- Footer.

The stylesheet includes responsive behavior so the interface can adapt to desktop, tablet, and mobile screen sizes.

---

## How to Run the Project

### Option 1 — Open Directly in a Browser

1. Extract the ZIP archive.
2. Open the extracted project folder.
3. Open:

```text
weather_app.html
```

4. Enter a city and select **Search**, or use **Use My Location**.
5. Allow location permission if using browser geolocation.

An Internet connection is required for weather data and CDN-hosted resources.

---

### Option 2 — VS Code + Live Server

For development:

1. Open the project directory in Visual Studio Code.
2. Install the **Live Server** extension if desired.
3. Right-click `weather_app.html`.
4. Select **Open with Live Server**.

A local URL similar to this will open:

```text
http://127.0.0.1:5500/weather_app.html
```

Using a local HTTP server is particularly useful when testing browser features such as geolocation.

---

### Option 3 — Simple Local HTTP Server

If Python is already installed:

```bash
python -m http.server 8000
```

Then navigate to:

```text
http://localhost:8000/weather_app.html
```

Python is not an application dependency; it is only an optional development server.

---

## Dependencies

The project has no npm, Python-package, database, or backend-framework requirements.

### External Browser Dependencies

| Dependency | Purpose |
|---|---|
| **Open-Meteo Geocoding API** | City lookup |
| **Open-Meteo Forecast API** | Weather and forecast data |
| **Chart.js** | Temperature visualization |
| **Bootstrap 5.3.2** | Responsive UI utilities |
| **Google Fonts** | Inter and Poppins |

### Browser Requirements

A modern browser supporting:

- JavaScript ES6+.
- Fetch API.
- Async/Await.
- Promises.
- DOM APIs.
- Geolocation API for location-based weather.
- Canvas rendering for Chart.js.

### Network Requirements

Internet connectivity is required for:

- Open-Meteo API requests.
- Chart.js CDN.
- Bootstrap CDN.
- Google Fonts.

---

## Testing Checklist

Recommended manual verification:

- [ ] Application loads without JavaScript errors.
- [ ] Weather panel is initially hidden as designed.
- [ ] Empty city search displays validation feedback.
- [ ] Valid city search returns weather data.
- [ ] City and country label display correctly.
- [ ] Invalid/nonexistent city produces appropriate feedback.
- [ ] Current temperature displays in °C.
- [ ] Current weather description displays.
- [ ] Weather icon corresponds to the weather code.
- [ ] Wind speed displays.
- [ ] Relative humidity displays.
- [ ] UV index displays.
- [ ] Sunrise displays.
- [ ] Sunset displays.
- [ ] Up to 12 upcoming hourly cards are generated.
- [ ] Hourly temperature displays.
- [ ] Hourly humidity displays.
- [ ] Daily forecast contains up to 7 days.
- [ ] Daily maximum/minimum temperatures display.
- [ ] Weekly chart renders.
- [ ] Searching a second city updates the chart correctly.
- [ ] Use My Location requests browser permission.
- [ ] Approved geolocation retrieves weather.
- [ ] Rejected geolocation displays feedback.
- [ ] Dark mode activates.
- [ ] Light mode restores correctly.
- [ ] Theme button label changes with the theme.
- [ ] Clear control resets the weather display.
- [ ] Interface remains usable on mobile-sized screens.

---

## Known Limitations

- The application depends on external Open-Meteo services and Internet connectivity.
- City search uses only the first geocoding result (`count=1`), so ambiguous city names cannot currently be disambiguated by the user.
- Geolocation depends on browser support, user permission, and secure-context/browser rules.
- Weather units are fixed by the current implementation rather than selectable by the user.
- Temperature is displayed in Celsius.
- Wind speed is presented as km/h in the UI.
- The current humidity value is taken from the first hourly humidity entry rather than explicitly matching the `current_weather` timestamp.
- Weather icons are emoji rather than a dedicated weather-icon asset set.
- Error feedback is primarily provided with browser `alert()` dialogs.
- Theme preference is not persisted across page reloads.
- The application does not cache weather data for offline use.
- There is no automated unit/integration test suite.
- No request cancellation is implemented if users initiate several searches rapidly.
- There is no loading indicator while API requests are in progress.
- The application does not display precipitation probability, pressure, visibility, or air quality.

---

## Learning Outcomes

This project reinforces important software-development concepts:

1. **REST API integration** — consuming live data from external services.
2. **Asynchronous JavaScript** — coordinating API requests with `async` and `await`.
3. **Geocoding** — translating human-readable city names into geographic coordinates.
4. **Geolocation** — using browser-provided device/location capabilities.
5. **Data transformation** — converting raw API data into meaningful UI values.
6. **DOM manipulation** — dynamically creating forecast cards and updating weather fields.
7. **Data visualization** — presenting forecast trends using Chart.js.
8. **Date/time processing** — formatting ISO timestamps for users.
9. **Conditional mapping** — translating weather codes into descriptions and icons.
10. **Error handling** — responding to invalid locations, failed HTTP requests, and geolocation errors.
11. **State management** — maintaining and replacing the active chart.
12. **Responsive design** — building a UI that adapts to multiple viewport sizes.
13. **Theme management** — changing presentation by toggling CSS state classes.
14. **Separation of concerns** — organizing HTML, CSS, and JavaScript into dedicated files.

---

## Future Improvements

Potential enhancements include:

- Add °C / °F unit selection.
- Add km/h / mph wind-speed selection.
- Add geocoding result selection for ambiguous city names.
- Add search autocomplete.
- Add recent-search history.
- Persist theme preference using `localStorage`.
- Persist favorite cities.
- Add loading indicators/skeleton states.
- Replace alerts with inline error components.
- Add precipitation probability.
- Add precipitation amount.
- Add atmospheric pressure.
- Add visibility.
- Add apparent/feels-like temperature.
- Add air-quality data.
- Add wind direction.
- Add more detailed weather icons.
- Add hourly temperature charting.
- Add precipitation charts.
- Add chart tooltips and richer visualization.
- Add severe-weather information where supported.
- Add request cancellation with `AbortController`.
- Add retry/backoff behavior for temporary network failures.
- Improve current-hour humidity matching.
- Add automated unit tests for weather-code and date-formatting helpers.
- Add API integration tests.
- Add accessibility and keyboard-navigation improvements.
- Add Progressive Web App support.
- Add offline caching and service-worker support.

---

## Developer

**Mohsen Ghazel**  
Software Development Bootcamp  
Interactive Website Project  
Interactive Weather Forecast App  
2026
