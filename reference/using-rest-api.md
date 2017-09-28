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

# Using the REST API's
{: #rest_api}

An [OpenAPI Specification 2.0 (formerly, Swagger 2.0)](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/2.0.md) compliant REST API will be made available on Beta release and can be used to retrieve relevant Knowledge Kit data. 
{: shortdesc}


## Handling missing data fields in the API response
{: #handling_missing}

If data for any field is not available, its value will be an empty string, ```""```. The REST API will return the appropriate fields available to all collections consistently, despite whether data for a field is missing or not.


## Handling errors
{: #handling_errors}

The following error codes are common to all endpoints:

|**Error** |**Description**                                    |
|----------|---------------------------------------------------|
|400       |Bad request. The request was not understood by the server due to malformed syntax. This error code is implemented for all APIs. API rejects the request if any invalid parameters are supplied.|
|401       |Unauthorized. The request requires authentication.|
|403       |Forbidden. The server understood the request but is refusing to fulfill it.|
|500       |Internal server error. The server encountered an unexpected condition that prevented it from fulfilling the request.|

*Table 1. Error response code*