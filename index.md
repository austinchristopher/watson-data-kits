---

copyright:
  years: 2017
lastupdated: "2017-10-20"

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
The {{site.data.keyword.watsondatakits_full}} are the individual building blocks that can be used to build applications based on parsed and annotated content from the {{site.data.keyword.watsoncontent_short}} team.

The first kit that we have made available for you to start with is the Data Kit for Travel Points of Interest (POI). This service provides information on points of interest and attractions based on location input. 

The following tutorial will help show how you can quickly get started with the service. The steps of the tutorial will walk through examples of endpoints that are exposed, how they can be called, which paramaters are acceptable, and what kinds of responses are expected.
{: shortdesc}


## Before you begin
{: #prereqs}

If you already know the credentials for your {{site.data.keyword.watsondatakits_short}} service instance, skip this step.
{: tip}

You'll need a [Bluemix account](https://console.ng.bluemix.net/registration/) and an instance of the {{site.data.keyword.watsondatakits_short}} service.

1. Go to the [Watson Data Kits ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.bluemix.net/catalog/services/watson-content-knowledge-kits){: new_window} and either sign up for a free Bluemix account or log in.
1. After you login in, click **Create** and you will be taken to the dashboard page for this service instance.
1. On the sidebar, navigate to **Service credentials** tab.
1. Use **New credential** button on this page to create credentials. In creating credentials you can use default settings or provide your own. Click **Add** to continue.
1. Once you have submitted the form for creating credentials, go to **View credentials** under the Actions column to view your credentials in JSON form.

1. Please note and store `apikey`, `instance_id`, and `url`. You will need `apikey` to request an Access Token for access to the API. You will need an `instance_id` and `url` to make API calls. 

Please note and store `apikey`, `instance_id`, and `url`.
{: tip}

**Note**:The examples in the bash codeblocks to follow use cURL to call methods of the HTTP interface. You can install the version of cURL for your operating system from [curl.haxx.se ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://curl.haxx.se/){: new_window}. You must install the version that supports the Secure Sockets Layer (SSL) protocol. Make sure to include the installed binary file on your `PATH` environment variable.


## Get access token
{: #get-access-token}
1. Issue the following command.
  -  Replace `{apikey}` with the API Key provided in **Service credentials**
  -  If you have not created **Service credentials**, see **Before you begin** section #3 to learn how.
 
  ```bash
  curl -X POST \
  -H "Content-Type: application/x-www-form-urlencoded" \
  -H "Accept: application/json" \
  -d "grant_type=urn:ibm:params:oauth:grant-type:apikey&apikey={apikey}" \
  "https://iam.stage1.bluemix.net/identity/token" \
  ```
  {: pre}

1. Save the `access_token`. To Authenticate any request, provide this `access token` in your request headers as a Bearer token.

Please note and store `access_token`.
{: tip}


## Step 1: Request the default JSON response for any provided location.
{: #step-1}

1.  Find a pair of `latitude` and `longitude` coordinates (in Decimal Degrees) of any location you would like to test. For convenience, here are `latitude` and `longitude` values for San Francisco: 

    ```javascript
    { 
        "latitude": 37.7792808,
        "longitude": -122.4192363
    }
    ```
    {: codeblock}

1.  Issue the following command to request the default JSON response. The  `Accept` header specifies acceptable meadia types for the response.
  -   Replace `{access_token}` with the access token you got from the **Get Access Token** section of this page.
  -   Replace `{url}` and `{instance_id}` with the url and instance id provided in **Service credentials** (See **Before you begin** section for more). 
  -   Modify `{latitude}` and `{longitude}` to specify your desired inputs (you can use the values provided in step #1.1).
  
  ```bash
  curl -X GET \
  -H "Authorization: Bearer {access_token}" \
  -H "Instance-ID: {instance_id}" \
  -H "Accept: application/json" \
  "{url}/travel/v1/attractions?location={latitude},{longitude}" \
  ```
  {: pre}

The service returns a JSON response that includes information about travel attractions found near the location input that was entered. The following is an example response using the San Francisco gps coordinates provided in step #1.1:

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

## Step 2: (Optional) Request a JSON response of available categories you may want to specify.
{: #step-2}

1.  Issue the following command to request a JSON response of the available categories. 

  **Note**: If you would not like to specify a category and only search attractions by name, you may skip this step and go directly to step #3.

  ```bash
  curl -X GET \
  -H "Authorization: Bearer {access_token}" \
  -H "Instance-ID: {instance_id}" \
  -H "Accept: application/json" \
  "{url}/travel/v1/categories"
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
    . . .
  }
  ```
  {: codeblock}


## Step 3: Request a JSON response for attractions with parameters of your choosing.
{: #step-3}


1.  From the JSON response in the last step, select any category that you would like to use as a query parameter. Take note of this category so that you can use it for the next step.

1.  Issue the following command to request a JSON response of attractions near a location, filtered by a category of your choosing. 
  -   Replace `{access_token}` with the access token you got from the **Get Access Token** section of this page.
  -   Replace `{url}` and `{instance_id}` with the url and instance id provided in **Service credentials** (See Before you begin** section for more). 
  -   Modify `{latitude}` and `{longitude}` to specify your desired inputs (you can use the values provided in step #1.1).
  -   Replace `{attraction}` with any word you would like to filter attractions by their names with.
  -   Optional: Replace `{category}` with a category you selected in step #2.2.

  ```bash
  curl -X GET \
  -H "Authorization: Bearer {access_token}" \
  -H "Instance-ID: {instance_id}" \
  -H "Accept: application/json" \
  "{url}/travel/v1/attractions?location={latitude},{longitude}&attraction={attraction}&category={category}"
  ```
  {: pre}

  The service returns a JSON response that includes information about travel attractions found near the location input that was entered, filtered according to the category provided. The following is an example response using "national" as `{attraction}` and "park" as `{category}`.

      ```javascript
      [
        {
          "address": {
              "address_string": "Landmark Building E, San Francisco, CA 94109, USA",
              "county": "San Francisco County",
              "postcode": "94109",
              "city": "San Francisco",
              "country": "United States",
              "state": "California"
          },
          "categories": [
              "Park"
          ],
          "description": "The park consists of a visitor center, Hyde St Pier and the fleet of historic ships moored there, the Maritime Museum, Aquatic Park, and the Municipal Pier.",
          "distance_miles": 2.2,
          "id": "e9549ff6-46e6-4cf1-a1fe-9a48ff61a6f2",
          "location": {
              "lat": 37.806643,
              "lng": -122.430359
          },
          "name": "San Francisco Maritime National Historical Park",
          "phone": "+1 415-447-5000",
          "rank": 295.457781839106,
          "url": "http://www.triposo.com/poi/T__c43b2521d3d8",
          "image_url": ""
        },
        {
          "address": {
              "address_string": "Rodeo Valley Trail, Sausalito, CA 94965, USA",
              "county": "Marin County",
              "street": "Rodeo Valley Trail",
              "postcode": "94965",
              "city": "Sausalito",
              "country": "United States",
              "state": "California"
          },
          "categories": [
              "Park"
          ],
          "description": "It's no mystery why this is one of the Bay Area's most popular hiking and cycling destinations. As the trails wind beside the Pacific Ocean and San Francisco Bay and through the Marin Headlands, they afford stunning views of the sea, the Golden Gate Bridge and the city of San Francisco. ",
          "distance_miles": 6.1,
          "id": "900edc61-ea22-483e-82a3-6f5d774ce0dc",
          "location": {
              "lat": 37.837174,
              "lng": -122.51009
          },
          "name": "Golden Gate National Recreation Area",
          "phone": "415-561-4700",
          "rank": 287.602532640087,
          "url": "https://www.lonelyplanet.com/a/poi-sig/1371762/361864",
          "image_url": ""
        },
          . . .
      ]
      ```
      {: codeblock}


<!-- ## Next steps -->

<!-- -   Interact with the API in the [API explorer ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.bluemix.net/apidocs/....................){: new_window}. -->
