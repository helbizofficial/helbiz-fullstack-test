### [Helbiz](https://helbiz.com) - Full-stack technical test
This test is part of our hiring process at Helbiz for the Full-Stack Software Engineer role. The goal is to understand your development skills, coding style, how creative you are, and time management. Because the role is full-stack, we're going to ask you to develop a full-stack solution

There are three stages to this test, and you shouldn’t spend more than 4-6 hours completing it.

Overview
------
We would like to see how you architect an application that pulls data from an outside API, formats it for a [graphql](https://graphql.org/) API endpoint, and displays the data using using React.

1. pull data from our open GBFS API for `/free_bike_status`
2. create an API using ([apollo-server-express](https://www.npmjs.com/package/apollo-server-express) or [apollo-server-lambda](https://www.npmjs.com/package/apollo-server-lambda)) that formats the data and exposes a query so we can query by `bike_id`
3. create a single page app using React that renders the data from your graphql endpoint, and allows the user to query the API to get the latest status of a vehicle with `bike_id`

Instructions
------

### 1. Query our GBFS API
To get a list of vehicles and their current status, make a GET request to this endpoint:

```
https://api.helbiz.com/admin/reporting/arlington/gbfs/free_bike_status.json
```

The response looks like:
```json
{
  "last_updated": 1603386427821,
  "ttl": 0,
  "data": {
    "bikes": [
      {
        "bike_id": "T6S1",
        "lat": 38.86484,
        "lon": -77.077003,
        "is_reserved": 0,
        "is_disabled": 0,
        "vehicle_type": "scooter"
      },
      {
        "bike_id": "P6Z2",
        "lat": 38.882187,
        "lon": -77.111713,
        "is_reserved": 0,
        "is_disabled": 0,
        "vehicle_type": "scooter"
      },
      ...
    ]
  }
}
```

### 2. Create a Graphql API
We want you to make a graphql API ([apollo-server-express](https://www.npmjs.com/package/apollo-server-express) or [apollo-server-lambda](https://www.npmjs.com/package/apollo-server-lambda)) that exposes this data via a query - if no parameters are included, your graphql endpoint should simply return the list of vehicles. If the parameter `bike_id` is included, your endpoint should only return the data for that vehicle.

**HINT**: read about graphql + apollo here: https://www.apollographql.com/docs/tutorial/introduction/

**HINT**: you should organize the vehicle data under a `VehicleStatus` type, and your query returns an array of these

**BONUS**: add some simple auth to your endpoint via a `Bearer` token

### 3. Create a React component
Create a single page app using React that renders the data from your graphql endpoint. It can be as simple as querying your graphql endpoint for all vehicle statuses on page load and rendering them using [Material UI Table component](https://material-ui.com/components/tables/).

In addition, create a search input allows the user to get most recent status of a vehicle with the given `bike_id`. This should query your API with the parameter for `bike_id` and render the updated vehicle status.


Get coding!
------

To start, fork this repository and submit a pull request with your finished app. We'll review and schedule a call so you can go over it with us. Be prepared to explain your code and any technical questions we may have.
