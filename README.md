# Propeller Data Engineer Challenge

## Background

Propeller's AeroPoints are smart ground control points that are used to accurately geolocate aerial drone imagery. They have high accuracy GPS units inside them and upload their location to Propeller's cloud platform.

AeroPoints come in groups because you often need more than one to accurately geolocate a drone survey. In our database we store these groups in the `aeropoint_groups` table. Each group has a unique `id` and a `name`.

For each AeroPoint group we store the individual AeroPoints in the `aeropoints` table. Each AeroPoint has a unique `id`, and an `aeropoint_group_id` that links it to the group it belongs to.

Every time an AeroPoint uploads its location to Propeller we store that in the `aeropoint_capture` table, which has an `id`, an `aeropoint_id` that links it to the AeroPoint that captured the location, an `easting` and a `northing`, which are its coordinates in a projected coordinate system.

A projected coordinate system is a way of representing the earth's surface on a flat plane. The units of a projected coordinate system are usually meters or feet instead of degrees. Propeller must deal with a lot of different projected coordinate systems, but for this challenge we will assume that all the coordinates are located in the UK and are in the same coordinate system (British National Grid).

You can learn more about coordinate systems [here](https://www.propelleraero.com/blog/understanding-coordinate-systems-and-map-projections/).

## Challenge

As a data engineer at Propeller it will very likely have to pull data from an API, store it in our data warehouse and generate views or export it for others to use.

The challenge is for you to use the data in the provided `challenge.db` SQLite database to produce a CSV export that lists AeroPoint groups that have been used at least once in London.

The report should include the following columns:

- `Group Name`: The name of the AeroPoint group,
- `AeroPoints`: The total number of AeroPoints in each group
- `Captures`: The total number of captures for each group.

The bounding box coordinates for London are:
North West / Top Left corner: 51.6919 (lat), -0.5104 (lon)
South East / Bottom Right corner: 51.2868 (lat), 0.3340 (lon)

This API can be used to convert British National Grid eastings and northings to latitudes and longitudes: https://www.getthedata.com/bng2latlong

To complete the challenge you will need to:

- Write a script called `enrich_data.py` to pull data from the API and enrich the data in the database with the latitudes and longitudes of the captures.
- Write a script called `generate_report.py` to run an SQL query to generate and save the report in CSV format.

You should think of these scripts as needing to be "production ready" and should be written in a way that they could be run as part of a scheduled job.

## What we’ll be looking for

- Your ability to talk us through your thinking and the decisions you are making.
- A well-structured solution that is easy to understand and maintain.
- Code that is clean, readable and well-documented.
- Handling of edge cases and errors.
