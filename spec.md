# Jobsite Weather Planner

## Project Overview

The Jobsite Weather Planner is a web app that helps construction managers plan outdoor construction activities around weather conditions. Users select a jobsite on a map, choose a construction activity, and view a 7-day weather forecast.

The app evaluates weather conditions for crane lifts, concrete pours, and roofing work. Each day receives a Go, Caution, or No-Go rating based on the forecast and the activity's weather limits. Users can click on a day to see the weather information and the reason for its rating.

The app will use the free Open-Meteo weather API and will not require an API key. The goal is to make weather information easier for construction teams to understand and use when planning work.

The interactive map will use Leaflet with OpenStreetMap map tiles.

## 1. Purpose

The purpose of this app is to help construction managers make better decisions about scheduling outdoor construction activities.

Weather can affect worker safety, construction quality, equipment operation, and project schedules. This app will organize weather information into simple daily ratings so users can identify days that may be suitable for work and days that may require extra planning.

The app is a planning tool and does not replace professional judgment, jobsite safety procedures, manufacturer instructions, or project specifications.

## 2. Inputs

The app will use the following inputs:

- **Jobsite location:** The user clicks on a map to select a construction site.
- **Latitude and longitude:** Automatically determined from the map selection and displayed in decimal degrees.
- **Map implementation:** The app will use Leaflet and OpenStreetMap. Clicking any point on the map will select or change the jobsite location.
- **Construction activity:** The user selects one of three activities:
- Crane lifts
- Concrete pours
- Roofing
- **Forecast period:** The app automatically displays 7 days: today and the following six days.
- **Weather data:** The app retrieves hourly information from Open-Meteo, including:
- Air temperature in degrees Fahrenheit.
- Sustained wind speed in miles per hour.
- Wind gust speed in miles per hour.
- Probability of precipitation as a percentage.
- Precipitation amount in inches.

The user must select a jobsite location and construction activity before viewing the daily activity ratings.

The app will use the local time zone of the selected jobsite when displaying forecast information.

The app will not save locations, activity choices, work hours, or crane limits after the page is refreshed. The default values will be used again.

## 3. Calculations

The app will evaluate hourly weather conditions during the selected work hours and use those conditions to assign a daily rating.

The initial work hours will be 7:00 AM to 5:00 PM local jobsite time. A forecast hour at 7:00 AM is included. A forecast hour at 5:00 PM is excluded.

For example, 7:00 AM through 4:59 PM are included in the default work hours. The app will not include 5:00 PM or later hours.

### Crane Lifts

The app will compare forecast wind speeds and wind gusts with the selected crane wind limits.

Initial demonstration limits:
- Sustained wind speed limit: 20 mph.
- Wind gust limit: 25 mph.

Ratings:
- **Go:** All forecast sustained wind speeds and gusts are below their limits.
- **Caution:** A forecast wind speed or gust reaches 80% or more of its limit but does not exceed it.
- **No-Go:** A forecast wind speed or gust reaches or exceeds its limit.

Examples with the initial 20 mph sustained wind limit and 25 mph gust limit:
- Sustained wind: 15.99 mph is below 80% of 20 mph and would be Go if no other crane measurement is worse.
- Sustained wind: exactly 16 mph reaches 80% and is Caution, unless gust or sustained wind reaches a No-Go limit.
- Sustained wind: exactly 20 mph is No-Go.
- Sustained wind: 21 mph is No-Go.
- Gust: exactly 20 mph reaches 80% of the 25 mph gust limit and is Caution, unless a measurement reaches a No-Go limit.
- Gust: exactly 25 mph is No-Go.
- Gust: 26 mph is No-Go.

These initial values are demonstration settings only. Actual crane limits must be checked against the crane manufacturer's instructions and the lift plan. The user should be able to change the limits.

### Concrete Pours

The app will compare forecast air temperatures with a 40°F cold-weather planning threshold.

Ratings:
- **Go:** All forecast work-hour temperatures are above 40°F.
- **Caution:** At least one forecast work-hour temperature is 33°F to 40°F.
- **No-Go:** Any forecast work-hour temperature is 32°F or lower.

Clear boundary examples:
- 41°F is Go if all work-hour temperatures are above 40°F.
- Exactly 40°F is Caution.
- Exactly 33°F is Caution.
- Exactly 32°F is No-Go.
- 31°F is No-Go.

The 40°F threshold is based on American Concrete Institute cold-weather guidance. Actual concrete placement decisions must also consider the concrete mix, concrete temperature, protection period, curing, and project specifications.

### Roofing

The app will compare the forecast probability of precipitation during work hours with the following planning thresholds:

- **Go:** Maximum hourly precipitation probability is below 20%.
- **Caution:** Maximum hourly precipitation probability is 20% to 50%.
- **No-Go:** Maximum hourly precipitation probability is above 50%.

Clear boundary examples:
- 19% is Go.
- Exactly 20% is Caution.
- Exactly 50% is Caution.
- 51% is No-Go.
- 60% is No-Go.

These precipitation thresholds are planning assumptions for this app, not official roofing safety standards. Actual roofing decisions must consider the roofing material, roof conditions, manufacturer instructions, and jobsite safety requirements.

### Daily Rating Rules

Each day will receive one rating for the selected activity.

The app will:
1. Retrieve the hourly forecast for the selected location.
2. Identify forecast hours within the work schedule.
3. Compare the forecast values with the activity thresholds.
4. Assign one rating for the entire day using the worst hourly rating:
   - No-Go takes priority over Caution.
   - Caution takes priority over Go.
   - A day with a combination of Go and Caution hours is Caution.
   - A day with any No-Go hour is No-Go.
5. Display the reason for the rating.

If required weather data is missing, the app will display "Unavailable" instead of assuming conditions are safe:
- Crane lifts require sustained wind speed and wind gust speed for every work-hour forecast period.
- Concrete pours require air temperature for every work-hour forecast period.
- Roofing requires precipitation probability for every work-hour forecast period.

If one required value is missing for an activity, that activity's rating for the day is Unavailable. Other activities may still receive ratings if their required data is available.

If the Open-Meteo weather API fails or cannot be reached, the app will display a clear error message, such as "Weather data could not be retrieved. Please check your internet connection and try again." The app should not show Go, Caution, or No-Go ratings when the forecast data cannot be retrieved.

## 4. Outputs

The app will display:

- An interactive map for selecting the jobsite.
- The selected jobsite's latitude and longitude.
- A 7-day weather forecast.
- A daily Go, Caution, or No-Go rating for the selected activity.
- Daily high and low temperatures.
- Forecast wind speeds and wind gusts.
- Probability of precipitation.
- A detailed explanation of why each day received its rating.
- A message when weather data cannot be retrieved.

The user can click on an individual day to see more detailed hourly weather information and the calculations used to determine the rating.

The app will use clear colors:
- Green for Go.
- Yellow for Caution.
- Red for No-Go.
- Gray for unavailable weather data.

## 5. Look and Feel

The app should have a clean, professional design that would be easy for a construction manager or field supervisor to use.

The design should include:

- A title at the top: Jobsite Weather Planner.
- A short explanation of what the app does.
- An interactive map near the top of the page.
- A dropdown menu for selecting a construction activity.
- A display showing the selected jobsite.
- Seven daily forecast cards.
- Clear color-coded ratings.
- A section showing detailed weather information when a user selects a day.

The app should work on both desktop computers and mobile devices.

The layout should be simple, readable, and easy to navigate.

## 6. Validation

The app must be tested using hand-worked examples to confirm that the ratings match the calculation rules.

### Hand-Worked Case 1: Crane Lifts

Inputs:
- Sustained wind speed: 12 mph.
- Wind gust speed: 18 mph.
- Sustained wind limit: 20 mph.
- Wind gust limit: 25 mph.

Calculations:
- 12 mph is below the 20 mph sustained wind limit.
- 18 mph is below the 25 mph gust limit.

Expected output:
- Rating: Go.
- Reason: Sustained wind speed and wind gusts are below the selected limits.

### Hand-Worked Case 2: Concrete Pours

Inputs:
- Forecast work-hour temperatures: 45°F, 42°F, 38°F, 41°F, and 44°F.

Calculations:
- The lowest forecast temperature is 38°F.
- 38°F is below 40°F but above 32°F.
- This falls within the Caution range.

Expected output:
- Rating: Caution.
- Reason: At least one forecast work-hour temperature is below 40°F.

### Hand-Worked Case 3: Roofing

Inputs:
- Forecast work-hour precipitation probabilities: 10%, 20%, 35%, 50%, and 15%.

Calculations:
- The maximum hourly precipitation probability is 50%.
- 50% is inside the Caution range.

Expected output:
- Rating: Caution.
- Reason: At least one forecast work-hour precipitation probability is 20% to 50%.

### Additional Crane Lifts Boundary Case

Inputs:
- Sustained wind speed limit: 20 mph.
- Wind gust limit: 25 mph.
- Sustained wind speeds: 15 mph and 16 mph.
- Wind gust speeds: 18 mph and 20 mph.

Calculations:
- 16 mph is exactly 80% of the 20 mph sustained wind limit.
- 20 mph is exactly 80% of the 25 mph gust limit.
- Both readings are Caution thresholds.

Expected output:
- Rating: Caution.
- Reason: A forecast sustained wind speed or gust is at least 80% of its selected limit.

### Additional Concrete Pours Boundary Case

Inputs:
- Forecast work-hour temperatures: 32°F and 33°F.

Calculations:
- The minimum temperature is 32°F.
- A temperature at or below 32°F is No-Go.
- The 33°F reading does not change the 32°F result.

Expected output:
- Rating: No-Go.
- Reason: At least one forecast work-hour temperature is 32°F or lower.

### Additional Roofing Boundary Case

Inputs:
- Forecast work-hour precipitation probabilities: 19%, 20%, 50%, and 51%.

Calculations:
- The maximum hourly precipitation probability is 51%.
- 51% is above the 50% No-Go threshold.

Expected output:
- Rating: No-Go.
- Reason: At least one forecast work-hour precipitation probability is above 50%.

### Missing Data Case

Inputs:
- An hourly work-period forecast that is missing one required value.

Expected output:
- Crane: Unavailable if a sustained wind speed or wind gust speed is missing.
- Concrete: Unavailable if air temperature is missing.
- Roofing: Unavailable if precipitation probability is missing.

The app must not replace missing values with zero or any estimated value.

### Additional Testing

The app will also be tested by:

- Selecting different locations on the map.
- Switching between crane lifts, concrete pours, and roofing.
- Checking that all seven forecast days appear.
- Testing weather conditions above and below each threshold.
- Testing exactly 80% crane limits and exactly at the sustained and gust limits.
- Testing concrete temperatures at 40°F, 33°F, 32°F, and nearby values.
- Testing roofing probabilities at 19%, 20%, 50%, 51%, and nearby values.
- Testing mixed hourly results to confirm that No-Go overrides Caution and Caution overrides Go.
- Testing missing required weather values and the Unavailable rating.
- Testing invalid custom work hours and crane limits.
- Checking that the daily rating explanations match the calculations.
- Testing what happens when the weather API is unavailable.
- Comparing the app's forecast with the National Weather Service forecast for the same location and date.

Custom work hours must be entered as a start time and an end time. The app will not allow the end time to be the same as or earlier than the start time. If the values are invalid, it will show a clear message and keep the previous valid work hours until corrected.

Crane limit inputs must be numbers greater than zero. The app will show a clear message if a limit is missing, is not a number, or is zero or negative.

## 7. Out of Scope

The app will not:

- Replace a construction manager's professional judgment.
- Approve or certify crane lifts.
- Replace crane manufacturer wind limits or lift plans.
- Determine concrete mix designs or curing requirements.
- Approve roofing work or replace roofing manufacturer instructions.
- Guarantee weather conditions.
- Provide emergency weather alerts.
- Replace official weather forecasts or jobsite safety procedures.
- Require users to create an account or log in.

## Features

The following two additional features will be added after the main app is built and validated.

### Feature 1: Custom Crew Work Hours

Users will be able to change the hours that their construction crews normally work.

For example, a crew working from 6:00 AM to 2:00 PM should only have weather conditions during those hours included in its daily rating.

This will make the ratings more useful for different construction schedules.

- The default work hours are 7:00 AM to 5:00 PM.
- The start time is included and the end time is excluded.
- Changes to the work hours will immediately recalculate all seven forecast days.
- The app will not support overnight work-hour ranges.
- Valid start and end times must be in chronological order for the same day.
- Work-hour changes and crane limit changes reset to their defaults when the page is refreshed.

### Feature 2: Printable Daily Field Brief

Users will be able to create a printable daily field briefing for their selected jobsite and construction activity.

The briefing will include:
- Jobsite location.
- Selected construction activity.
- Date.
- Daily weather rating.
- Important forecast information.
- Explanation of weather concerns.
- Suggested planning considerations derived from the rating and explanation.

The printable field brief will use the weather information, rating, and explanation for the day selected by the user. The brief can be printed with the browser print function. It does not need to include an interactive map or hourly charts.

This will give construction managers a simple report they can share with their crews during daily planning meetings.

## Build Stages

### Stage 1: Page Mockup
Create the basic page layout, including the title, map area, activity dropdown, and seven forecast cards. Use sample weather information at first.

### Stage 2: Jobsite Map
Add an interactive map that allows users to click and select a jobsite. Display the selected latitude and longitude.

### Stage 3: Weather API
Connect the app to the Open-Meteo API and retrieve a 7-day hourly weather forecast for the selected location.

### Stage 4: Weather Calculations
Add the calculations for crane lifts, concrete pours, and roofing. Display the daily Go, Caution, and No-Go ratings and their explanations.

### Stage 5: Testing and Validation
Test the app using the hand-worked examples, check different locations and activities, and compare the forecast with the National Weather Service.

### Stage 6: Feature Development
Add custom crew work hours and the printable daily field brief. Test and commit each feature separately.

### Stage 7: Final Review and Publication
Check the app for errors, improve the layout, test it on desktop and mobile, and publish it using GitHub Pages.

## Sources

- Occupational Safety and Health Administration (OSHA), Crane and Derrick Safety: https://www.osha.gov/green-jobs/wind-energy/crane-hoist
- OSHA, 29 CFR 1926.1435, Tower Cranes: https://www.osha.gov/laws-regs/regulations/standardnumber/1926/1926.1435
- American Concrete Institute (ACI), Cold Weather Concrete: https://www.concrete.org/topicsinconcrete/topicdetail.aspx?search=Cold+Weather+Concrete
- Open-Meteo Weather API: https://open-meteo.com/en/docs
- National Weather Service: https://www.weather.gov/