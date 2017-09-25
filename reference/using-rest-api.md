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

# Using the Travel Knowledge Kit REST API
{: #rest_api}
A [OpenAPI Specification 2.0 (formerly, Swagger 2.0)](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/2.0.md) compliant REST API is available and can be used to retrieve travel data. You can use the [API Documentation](https://dev-console.stage1.bluemix.net/apidocs/1444-watson-content-travel-knowledge-kit){:new_window} to test API operations and instantly view the results to help you build your applications faster.
{: shortdesc}


## Handling missing data fields in the API response
{: #handling_missing}

If data for any field is not available, it's value will be an empty string, ```""```. The REST API will return the appropriate fields available to all collections consistently, despite whether data for a field is missing or not.