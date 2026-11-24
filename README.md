# I Know a Spot

A product case study for planning a trip. Users can scroll through uploaded photos of travel spots. When they click on a photo, they will be able to see the address, reviews, hours and crowds. Includes a SQL and Python analysis of itinerary routes.

## The problem
Travel inspiration posts are full of ideas, but trying to find all the information you need to actually plan the trip is a completely different story. There's usually no address and no link, so you can't tell how far apart the stops are or whether the day is realistic.

## The idea
A feed you scroll like any social app. Tap a photo to see the place's address, reviews, nearby spots, hours and how crowded it gets by hour, then save it to a trip folder to build your itinerary.

## The analysis
I used one real shared 9-day Japan itinerary (39 stops) to test whether stop order matters.
- Typed the stops into a table and loaded it into SQLite
- Used SQL to count stops per day and per city and to find stops with no usable location
- Used Python (pandas) to calculate straight-line distance between stops with the haversine formula
- Tested every possible stop order for each day (first stop fixed) to look for a shorter route
- Charted the original order against the shortest order

## Findings
- 33 of 39 stops (85%) could be matched to a location. The rest were transit, vague entries ("Morning in Osaka"), or an outdated TeamLab listing.
- On the 7 days I could measure, reordering stops cut total straight-line distance from 48.1 km to 38.3 km (about 20%).
- The biggest change was Day 8: 14.7 km down to 8.9 km.
- Takeaway for the product: a plan built from posts with real addresses could point out days where the stop order makes the day longer than it needs to be.

## Limits
- Coordinates are approximate. I spot-checked 15 of the 32 distinct places and corrected 2. Testing alternate points for two large sites (Ueno Park, Ponto-cho Alley) left the result at about 20%.
- Distances are straight-line, not walking or transit time
- One itinerary, so these results are not general
- The first stop of each day is fixed, and I did not account for opening hours
- The prototype screens use sample data

## Data source
The itinerary comes from a shared travel itinerary graphic I found online. Original author unknown. I re-typed the stops by hand, and this repo does not redistribute the image.

## Tools
Python, pandas, SQLite, matplotlib, Google Colab

## Files
- `I-Know-A-Spot.ipynb`: the full analysis

## Next steps
- Replace the hand-entered coordinates with a geocoding lookup, so any city's itinerary can be analyzed
- Run the analysis on itineraries from other cities to see whether the savings hold up
- Add a map comparing the original route with the shortest route
- Use real walking or transit times instead of straight-line distance
- Build a working multi-city demo of the feed and place page using openly licensed photos and place data
- Test the prototype with a few travelers and record what they say

## What a full product would need
- Photos and reviews from real users, which means a community, moderation and clear photo ownership rules
- Reliable data for hours, ratings and crowds by hour, which is mostly held by large map providers and is not free
- Enough content in each city for the feed to be useful
