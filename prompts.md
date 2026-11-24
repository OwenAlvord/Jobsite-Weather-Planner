# AI Coding Prompt Log

This file records the prompts used to plan, build, test, and improve the Jobsite Weather Planner.

## Initial Project Setup

- Create a Jobsite Weather Planner web app based on the requirements in spec.md.
- Follow AGENTS.md and record each new request and prompt throughout the project.
- Based on the previous specification review, revise spec.md to address missing and unclear requirements. Use Leaflet and OpenStreetMap, show today plus the following six days, include 7:00 AM and exclude 5:00 PM, use the worst hourly rating with No-Go over Caution over Go, mark activity ratings Unavailable for missing required weather data, show a clear weather API error, immediately recalculate when custom work hours change, print a selected day's field brief, reset settings on refresh, and add clear boundary examples and additional validation cases. Do not build the app or create index.html. Update spec.md only and record this request in prompts.md.

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
