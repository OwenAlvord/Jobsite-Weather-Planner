# AI Coding Prompt Log

This file records the prompts used to plan, build, test, and improve the Jobsite Weather Planner.

## Specification Review

Read my `AGENTS.md` and `spec.md` files. I am building a Jobsite Weather Planner for my CCE 270 assignment.

Please review my specification and tell me:

1. What requirements are missing or unclear?
2. Are the weather calculations and rating rules specific enough to implement?
3. Are my two additional features clearly defined?
4. What changes would you recommend before we start building?
Do not write any code or change any files yet. Explain your feedback in simple language.

## Specification Revision

Based on your review, please revise my existing spec.md to address the missing and unclear requirements. Keep the project manageable for a beginner CCE 270 student. Use these decisions: 1. Use Leaflet and OpenStreetMap for the map. 2. Show today and the following six days. 3. Default work hours are 7:00 AM to 5:00 PM. Include 7:00 AM but exclude 5:00 PM. 4. The worst hourly rating determines the daily rating. No-Go takes priority over Caution, and Caution takes priority over Go. 5. Missing required weather data makes that activity's daily rating Unavailable. 6. Show a clear error message if the weather API fails. 7. Changing custom work hours immediately recalculates all seven days. 8. The printable field brief uses the selected day's weather information, rating, and explanation. 9. Settings reset to their defaults when the page is refreshed. Add clear boundary examples and additional validation cases for all three activities. Do not build the app or create index.html yet. Update spec.md only, preserve the existing requirements, and record this request in prompts.md. When finished, summarize what you changed.

## Stage 1 Page Mockup

- Read AGENTS.md and spec.md before starting.
- Build Stage 1 of my Jobsite Weather Planner: the basic page mockup.
- Create a single index.html file with:
  - A professional title and short description.
  - A section showing where the interactive jobsite map will go.
  - A dropdown for selecting Crane Lifts, Concrete Pours, or Roofing.
  - Seven daily forecast cards using sample weather data.
  - Clear Go, Caution, and No-Go ratings.
  - A section that displays details when a user selects a forecast day.
  - A clean, responsive design that works on computers and phones.
- Important:
  - Use simple HTML, CSS, and JavaScript in one index.html file.
  - Use sample weather data for now.
  - Do not connect the map or weather API yet.
  - Do not build the two additional features yet.
  - Follow the specification.
  - Record this exact request in prompts.md.
  - Test the page and fix any errors.
  - Do not change spec.md or AGENTS.md.
- When finished, explain what you built and how I can test it.

## Stage 2 Jobsite Map

Read AGENTS.md and spec.md before making changes.

Build Stage 2 of my Jobsite Weather Planner.

Add an interactive map using Leaflet and OpenStreetMap.

Requirements:

1. Display the map in the existing map section.
2. Allow users to click anywhere on the map to select a jobsite.
3. Place a marker at the selected location.
4. Allow users to click another location to move the marker.
5. Display the selected latitude and longitude.
6. Update the selected jobsite information whenever the marker moves.
7. Keep all existing Stage 1 features working.
8. Do not connect the weather API yet.
9. Keep all HTML, CSS, and JavaScript in index.html.
10. Record this exact request in prompts.md.
Test the map and fix any problems. Do not build the additional features yet. When finished, explain how I can test the map.

## Stage 3 Weather API

Read `AGENTS.md` and `spec.md` before making changes.

Build Stage 3: Connect the Jobsite Weather Planner to the Open-Meteo weather API.

Requirements:

- Use the latitude and longitude from the location selected on the Leaflet map.
- Retrieve a 7-day forecast using the Open-Meteo API. No API key is needed.
- Request hourly temperature, wind speed, wind gusts, precipitation probability, and precipitation amount.
- Request daily high and low temperatures.
- Use Fahrenheit, mph, and inches.
- Use the jobsite’s local timezone with `timezone=auto`.
- Display the actual forecast information in the existing seven daily forecast cards.
- Update the forecast when the user selects a different map location.
- Show a loading message while weather data is being retrieved.
- Show a clear error message if the API request fails.
- Keep the existing map, activity dropdown, daily cards, and selected-day details working.
- Do not implement the activity rating calculations yet. Those will be Stage 4.
- Do not add either extra feature yet.
- Keep the app in the single `index.html` file.
Record my exact request in `prompts.md`. Test the changes and explain how I can check that the weather data is updating correctly.

## Stage 4 Weather Calculations

Read `AGENTS.md` and `spec.md` before making changes.

Build Stage 4: Implement the weather calculations and Go, Caution, and No-Go ratings.

Requirements:

**Crane Lifts**

- Evaluate the highest hourly sustained wind speed and highest hourly wind gust during the work hours.
- Default sustained wind limit: 20 mph.
- Default wind gust limit: 25 mph.
- Go: both wind measurements are below 80% of their limits.
- Caution: either measurement is at least 80% of its limit but remains below its limit.
- No-Go: either measurement reaches or exceeds its limit.
**Concrete Pours**

- Evaluate hourly temperatures during work hours.
- Go: all temperatures are above 40°F.
- Caution: any temperature is above 32°F and at or below 40°F.
- No-Go: any temperature is at or below 32°F.
**Roofing**

- Evaluate the highest hourly precipitation probability during work hours.
- Go: below 20%.
- Caution: 20% through 50%, inclusive.
- No-Go: above 50%.
**General requirements**

- Use the default work hours of 7:00 AM through 5:00 PM, following the jobsite’s local time.
- Apply No-Go before Caution when evaluating the day’s conditions.
- If required weather data is missing, show Unavailable instead of assuming conditions are safe.
- Display the correct rating on each daily forecast card for the selected activity.
- Update the ratings when the user changes the selected activity or jobsite.
- Show a clear explanation in the selected-day details explaining why the rating was assigned, including the relevant weather measurement and threshold.
- Keep the existing map and weather API working.
- Do not build the two extra features yet.
- Keep everything in the single `index.html` file.
Record my exact request in `prompts.md`. Test the calculations, including the boundary values in `spec.md`, and explain how I can check that the ratings work.

## Open-Meteo Fetch Diagnosis

The Open-Meteo API works when I open its URL directly in Edge, but my Jobsite Weather Planner app keeps displaying an internet connection error.

Please investigate the existing `index.html` and find why the app is failing to retrieve weather data.

Requirements:

- Check the API URL and fetch request.
- Check how the app handles API responses and errors.
- Check whether the selected map coordinates are being passed correctly.
- Fix the actual problem without removing existing features.
- Do not change the weather rating calculations unless necessary to fix the issue.
- Keep everything in the single `index.html` file.
- Record my exact request in `prompts.md`.
- Test the fix and explain what you changed.
Do not add any new features.

## Stage 5 Review and Validation

Read `AGENTS.md` and `spec.md`.

Perform Stage 5: Review and validate the complete Jobsite Weather Planner against the requirements in `spec.md`.

Check the following:

1. Interactive map selects a location and updates latitude and longitude.
2. Open-Meteo retrieves the correct seven-day forecast for the selected location.
3. Crane Lift calculations follow all specified limits and boundary conditions.
4. Concrete Pour calculations follow all specified temperature thresholds.
5. Roofing calculations follow all specified precipitation thresholds.
6. No-Go takes priority over Caution, and Caution takes priority over Go.
7. Missing weather data produces Unavailable rather than an incorrect safe rating.
8. API errors display a clear message.
9. Changing activities updates all ratings.
10. Selected-day details explain the rating correctly.
Use the hand-worked examples and boundary tests in `spec.md` to verify the calculations.

Fix any problems you find. Do not add new features or change the approved requirements.

Record my exact request in `prompts.md`. Explain what passed, what failed, and what you fixed. Do not commit changes yourself.

## Extra Feature 1: Custom Crew Work Hours

Read `AGENTS.md` and `spec.md` before making changes.

Build Extra Feature 1: Custom Crew Work Hours.

Requirements:

- Add a clear start-time and end-time setting to the Jobsite Weather Planner.
- Default to 7:00 AM through 5:00 PM.
- Let users change both times.
- Recalculate all seven daily activity ratings using the selected work hours.
- Apply the selected hours to Crane Lifts, Concrete Pours, and Roofing.
- Use the jobsite’s local timezone.
- Make the start time inclusive and the end time exclusive.
- Validate the times and prevent invalid or empty work-hour ranges.
- Keep the existing map, weather forecast, activity ratings, and explanations working.
- Reset to the default hours when the page is refreshed, as specified.
- Keep the app in the single `index.html` file.
- Do not build the printable daily field brief yet.
Record my exact request in `prompts.md`. Test the feature, including changing the hours and checking that all three activity ratings update correctly. Explain how I can test it myself.

Do not commit anything yet.

## Extra Feature 2: Printable Daily Field Brief

Read `AGENTS.md` and `spec.md` before making changes.

Build Extra Feature 2: Printable Daily Field Brief.

Requirements:

- Add a clear “Print Daily Field Brief” button.
- The report must use the currently selected forecast day.
- Include the jobsite latitude and longitude.
- Include the selected date and activity.
- Include the Go, Caution, No-Go, or Unavailable rating.
- Include the day’s high and low temperatures.
- Include relevant weather measurements for the selected activity:

- Crane Lifts: highest sustained wind and highest wind gust during work hours.
- Concrete Pours: temperatures during work hours.
- Roofing: highest precipitation probability during work hours.
- Include the explanation for the activity rating.
- Include the selected crew work hours.
- Add practical planning considerations based on the rating and weather conditions.
- Format the report cleanly for printing on paper.
- Use print-specific CSS so the report prints without the map, controls, or unnecessary page elements.
- Make sure the report reflects changes when the user selects another day, activity, location, or work schedule.
- Keep all existing features working.
- Keep the app in the single `index.html` file.
Record my exact request in `prompts.md`. Test the print feature and explain how I can check the report before printing.

Do not commit anything yet.

## Final Review Before Publishing

Read `AGENTS.md` and `spec.md`.

Perform a final review of the Jobsite Weather Planner before publishing.

Check the following:

1. All required features in `spec.md` are implemented.
2. The interactive map works.
3. The seven-day Open-Meteo forecast works and updates when the location changes.
4. Crane Lifts, Concrete Pours, and Roofing ratings work correctly.
5. Custom Crew Work Hours works and recalculates ratings.
6. Printable Daily Field Brief includes all required information and prints correctly.
7. Error handling and missing-weather-data behavior work.
8. The app works on desktop and mobile screen sizes.
9. `index.html`, `spec.md`, and `prompts.md` are present and complete.
10. `prompts.md` contains the exact prompts used throughout development.
Fix any remaining issues you find. Do not add new features or change the approved requirements.

Record my exact request in `prompts.md`.

At the end, give me a checklist of what passed, anything you fixed, and whether the project is ready to publish.

Do not commit anything or publish the app yet.
