
## reporting-api
This proof of concept is to determine whether the Admin UI’s current charting capability is the most suitable environment to build the Publisher Analytics suite.

### Errors
When an error is encountered you will receive an HTTP status code along with a message and error code in the body of the response.

Status Code | error | error_description
------------ | ------------- | -------------
400 | Incorrect publisher parameter value | There is no such publisher
400 | Incorrect date format. It should be in YYYY-MM-DD format | Incorrectly formatted date
500 | An error occurred during a request. | Internal Server Error – There was a problem with the API host server. Try again later.



### Available Fields endpoint
<details open>
<summary>Available fields for the selected publisher in the selected date range.</summary>

```shell
GET /kpi/publisher-analytics-available-fields?publisher=<span style="color:blue">{publisher}</span>&start_date=<span style="color:blue">{start_date}</span>&end_date=<span style="color:blue">{end_date}</span>
```

</details>

<details closed>
<summary>URI Parameters</summary>

parameter | parameter_type | parameter_description
------------ | ------------- | -------------
publisher | **string** (required) | one of the available publishers: *{guardian, news-uk, telegraph, reach, the-stylist-group, ozone}*, ozone means selecting all available publishers
start_date | **string** (required) |  starting date in YYYY-MM-DD format
start_date | **string** (required) |  end date in YYYY-MM-DD format

</details>

<details closed>
<summary>Example</summary>

```shell
GET /kpi/publisher-analytics-available-fields?publisher=telegraph&start_date=2019-12-10&end_date=2019-12-11
```

```json
  {
      "device_type": [
          "Computer",
          "Mobile",
          "Tablet",
          "Game console",
          "Digital media receiver"
      ],
      "domain": [
          "telegraph.co.uk"
      ],
      "partner": [
          "appnexus",
          "openx",
          "beeswax",
          "rubicon",
          "pubmatic"
      ],
      "size": [
          "728x90",
          "300x250",
          "970x250",
          "320x50",
          "300x600",
          "300x50"
      ]
  }
```
</details>
