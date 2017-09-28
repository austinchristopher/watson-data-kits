---

copyright:
  years: 2017
lastupdated: "2017-09-15"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# Getting started tutorial
The {{site.data.keyword.IBM}} {{site.data.keyword.knowledgekits_full}} are the individual building blocks that can be used to build applications based on parsed and annotated content from the {{site.data.keyword.watsoncontent_short}} team.

The first kit that we have made available for you to start with is the Travel Knowledge Kit. This service provides information on points of interest and attractions based on location input. 

The following tutorial will help show how you can get started quickly with the service. The example below shows how to call the service's GET method on different endpoints with parameters of your choice.
{: shortdesc}


## Before you begin
{: #prereqs}
You'll need a [Bluemix account](https://console.ng.bluemix.net/registration/) and an instance of the {{site.data.keyword.knowledgekits_full_notm}} service.

1.  Go to the [Watson Content Knowledge Kits ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.stage1.bluemix.net/catalog/services/watson-content-knowledge-kits){: new_window} and either sign up for a free Bluemix account or log in.
1.  After you login in, click **Create** and you will be taken to the dashboard page for this service instance.


**Note**: The examples below use cURL to call methods of the HTTP interface. You can install the version of cURL for your operating system from [curl.haxx.se ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://curl.haxx.se/){: new_window}. You must install the version that supports the Secure Sockets Layer (SSL) protocol. Make sure to include the installed binary file on your `PATH` environment variable.


## Step 1: Request the default JSON response for any provided location.
{: #step-1}

1.  Find a pair of `latitude` and `longitude` coordinates (in Decimal Degrees) of any location you would like to test. Below are `latitude` and `longitude` values for San Francisco for your convenience. 

    ```javascript
    { 
        "latitude": 37.7792808,
        "longitude": -122.4192363
    }
    ```
    {: codeblock}

1.  Issue the following command to request the default JSON response. The  `Accept` header specifies acceptable meadia types for the response.
    -   Modify {latitude} and {longitude} to specify your desired inputs (you can use the values provided in step #1.1 above).
  
    ```bash
    curl -X GET \
    --header "Accept: application/json" \
    "http://173.193.106.27:31000/attractions?location={latitude},{longitude}"
    ```
    {: pre}

The service returns a JSON response that includes information about travel attractions found near the location input that was entered. Below is an example response using the San Francisco gps coordinates provided above:

```javascript
[
    {
    "address": {
        "address_string": "1073-1075 Howard St, San Francisco, CA 94103, USA",
        "street_number": "1073-1075",
        "county": "San Francisco County",
        "street": "Howard Street",
        "postcode": "94103",
        "city": "San Francisco",
        "country": "United States",
        "state": "California"
    },
    "categories": [
        "Museum"
    ],
    "description": "The San Francisco Museum of Modern Art ( SFMOMA ) is a modern art museum in San Francisco, California established in 1935 under director Grace L. McCann Morley as the San Francisco Museum of Art , the first museum on the West Coast devoted solely to 20th-century art. A gift of 36 artworks from Albert M. Bender, including The Flower Carrier, 1935, by Diego Rivera, established the nucleus of the permanent collection. Bender, a trustee of the museum, proceeded to donate more than 1,100 objects to the museum and endow its first purchase fund before his death in 1941. For its first sixty years, the museum occupied the upper floors of the War Memorial Veterans Building in the Civic Center. Under director Henry T. Hopkins (1974–1986) the museum added \"Modern\" to its title in 1975, and established an international reputation. In 1995 the museum moved to its current location at 151 Third Street, adjacent to Yerba Buena Gardens in the SOMA district. The museum has in its collection important works by Andy Warhol, Jackson Pollock, Richard Diebenkorn, Clyfford Still, Henri Matisse, Paul Klee, Marcel Duchamp and Ansel Adams, among others. The cinema series Art in Cinema was started at SFMOMA in 1946 by filmmaker Frank Stauffacher. Annually, the museum hosts more than twenty exhibitions and over three hundred educational programs. Also in 2009, the museum gained a custodial relationship for the important contemporary art collection of Doris and Donald Fisher of The Gap.",
    "distance_miles": 1.2,
    "id": "03637471-fe9b-485f-93ee-1d5f24c1bc88",
    "location": {
        "lat": 37.778416,
        "lng": -122.408833
     },
    "name": "Museum of Modern Art",
    "phone": "+1 415-357-4000",
    "rank": 197.497458497745,
    "url": "http://www.triposo.com/poi/T__e9fb9daa8ecb",
    "image_url": ""
    },
    . . .
]
```
{: codeblock}

## Step 2: Request a JSON response after finding and specifying a category.
{: #step-2}

1.  Issue the following command to request a JSON response of the available categories.

    ```bash
    curl -X GET \
    --header "Accept: application/json" \
    "http://173.193.106.27:31000/categories"
    ```
    {: pre}

      The service returns a JSON response that includes information about travel categories available and how frequently each appears in the database.

      ```javascript
      {
        "Museum": 53872,
        "Park": 34623,
        "Church": 25515,
        "Nature/Wildlife": 23060,
        "Mountain": 10209,
        "Bridge/Tunnel": 9421,
        "Memorial": 9343,
        "Fort": 6475,
        "Museum/Gallery": 6033,
        "Castle": 5963,
        "Library": 5877,
        "University": 5063,
        "Family": 4327,
        "Temple": 4287,
        "Lake": 3985,
        "Beach": 3760,
        "Market": 3297,
        "History Museum": 3286,
        "Square": 3130,
        "Religious": 3018,
        . . .
      }
      ```
      {: codeblock}

1.  From the JSON response above, select any category that you would like to use as a query parameter. Take note of this category so that you can use it for the next step.

1.  Issue the following command to request a JSON response of attractions near a location, filtered by a category of your choosing. 
    -   Replace {category_keyword} with the category you selected in step #2.2.
    -   Modify {latitude} and {longitude} to specify your desired inputs (you can use the values provided in step #1.1 above).

    ```bash
    curl -X GET \
    --header "Accept: application/json" \
    "http://173.193.106.27:31000/attractions?location={latitude},{longitude}&category_keyword={category_keyword}"
    ```
    {: pre}

  The service returns a JSON response that includes information about travel attractions found near the location input that was entered, filtered according to the category provided. Below is an example response using "memorial" as {category_keyword}.

      ```javascript
      [
       {
          "address:" {
              "address_string": "100 Larkin St, San Francisco, CA 94102, USA",
              "street_number": "100",
              "county": "San Francisco County",
              "street": "Larkin Street",
              "postcode": "94102",
              "city": "San Francisco",
              "country": "United States",
              "state": "California"
          },
          "categories": [
              "Statue"
          ],
          "description": "Double L Excentric Gyratory is a sculpture by American artist George Rickey. There are three editions. One is installed at the intersection of Larking and Fulton streets, outside the Main Library, in San Francisco's Civic Center, in the U.S. state of California. Another is part of the Auckland Art Gallery's International Art Collection. This stainless steel sculpture, dated 1985, measures 7163 x 3543 mm and was gifted by the Edmiston Trust.",
          "distance_miles": 0.1,
          "id": "e6c20243-344d-4ceb-b155-82767df62648",
          "location": {
              "lat": 37.7793110683296,
              "lng": -122.415905136432
          },
          "name": "Double L Excentric Gyratory",
          "phone": "",
          "rank": 199.638437974817,
          "url": "",
          "image_url: https://upload.wikimedia.org/wikipedia/commons/e/ed/Double_L_Excentric_Gyratory_by_George_Rickey%2C_San_Francisco_%282013%29_-_1.JPG",
          "grouping": "Monument"
       },
          . . .
      ]
      ```
      {: codeblock}

<!-- ## Next steps -->

<!-- -   Interact with the API in the [API explorer ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.stage1.bluemix.net/apidocs/1461-watson-content-travel-knowledge-kit){: new_window}. -->