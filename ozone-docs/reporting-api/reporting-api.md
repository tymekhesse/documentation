
## reporting-api
### publisher analytics
This proof of concept is to determine whether the Admin UI’s current charting capability is the most suitable environment to build the Publisher Analytics suite.


#### Available Fields endpoint

```shell
    GET /kpi/publisher-analytics-available-fields?publisher={publisher}&start_date={start_date}&end_date={end_date}
```

<details/>
<summary/>Details</summary>
Endpoint returns a json object containing arrays of available device_type, demoin, partner, size for a given publisher for a given time interval.

```shell
{
  "device_type": [],
  "domain": [],
  "partner": [],
  "size": []
}
```
</details>

<details/>
<summary/>URI Parameters</summary>

    parameter | parameter_type | parameter_description
    ------------ | ------------- | -------------
    publisher | **string** (required) | one of the available publishers: *guardian, news-uk, telegraph, reach, the-stylist-group, ozone*, ozone means selecting all available publishers
    start_date | **string** (required) |  starting date in YYYY-MM-DD format
    end_date | **string** (required) |  end date in YYYY-MM-DD format

</details>


<details/>
<summary/>Example request</summary>

```shell
GET /kpi/publisher-analytics-available-fields?publisher=telegraph&start_date=2019-12-10&end_date=2019-12-11

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


#### Benchmark endpoint

```shell
    GET /kpi/publisher-analytics-benchmark?start_date={start_date}&end_date={end_date}&publisher={publisher}
```

<details/>
<summary/>Details</summary>
Endpoint returns a json table containing the following tables: partners, revenue, benchmark for a given publisher for a given time period.

  1. "revenue" column is meant to show the % of revenue given ad partner constitutes for the chosen publisher
  2. "benchmark" column shows the % of revenue given ad partner constitutes across all publishers

```shell
[
    [
        "partner_1",
        revenue,
        benchmark
    ],
    [
        "partner_2",
        revenue,
        benchmark
    ],
    [
        "partner_3",
        revenue,
        benchmark
    ]
]
```
</details>

<details/>
<summary/>URI Parameters</summary>

    parameter | parameter_type | parameter_description
    ------------ | ------------- | -------------
    publisher | **string** (required) | one of the available publishers: *guardian, news-uk, telegraph, reach, the-stylist-group, ozone*, ozone means selecting all available publishers
    start_date | **string** (required) |  starting date in YYYY-MM-DD format
    end_date | **string** (required) |  end date in YYYY-MM-DD format

</details>


<details/>
<summary/>Example request</summary>

```shell
GET /kpi/publisher-analytics-benchmark?start_date=2019-11-16&end_date=2019-11-17&publisher=telegraph

[
    [
        "appnexus",
        49.439131586213506,
        46.868344046578706
    ],
    [
        "beeswax",
        40.6894085110077,
        11.770534879906727
    ],
    [
        "openx",
        8.616146929082245,
        18.2159087671419
    ],
    [
        "rubicon",
        1.2553129736965587,
        4.978539603600537
    ]
]
```

</details>

#### Publisher analytics results endpoint

  ```shell
      GET /kpi/publisher-analytics?start_date={start_date}&end_date={end_date}&publisher={publisher}&{domain, size, device_type}&domain_list={domain_1, domain_2}&size_list={size_1, size_2}&device_list={device_1, device_2}&publisher_list={publisher_1, publisher_2}
  ```

<details/>
<summary/>Details</summary>
Endpoint returns a json table containing tables containing date, partner, domain, size, device_type, revenue for a given publisher for a given time interval based on selected filters

```shell
[
    [
        date,
        partner,
        domain,
        size,
        device,
        revenue
    ],
    ...
]
```
</details>

<details/>
<summary/>URI Parameters</summary>

    parameter | parameter_type | parameter_description
    ------------ | ------------- | -------------
    publisher | **string** (required) | one of the available publishers: *guardian, news-uk, telegraph, reach, the-stylist-group, ozone*, ozone means selecting all available publishers
    start_date | **string** (required) |  starting date in YYYY-MM-DD format
    end_date | **string** (required) |  end date in YYYY-MM-DD format
    domain, size, device_type | **string** (optional) |  used to specify additional fields
    domain_list, size_list, device_list, publisher_list | **string** (optional) | used to specify additional filters, names specified in the database, for example: "Guardian", "300x250"  

</details>


<details/>
<summary/>Example request</summary>

```shell
GET /kpi/publisher-analytics?start_date=2019-11-16&end_date=2019-11-17&publisher=ozone&device_type=Computer&publisher_list=Guardian,Telegraph

[
    [
        "2019-11-17",
        "pubmatic",
        "Computer",
        509.6204058589993
    ],
    [
        "2019-11-17",
        "pubmatic",
        "Digital media receiver",
        0.07737414499999999
    ],
    [
        "2019-11-17",
        "pubmatic",
        "Game console",
        0.4653749760000001
    ],
    [
        "2019-11-17",
        "pubmatic",
        "Mobile",
        2042.1119873690018
    ],
    [
        "2019-11-17",
        "pubmatic",
        "Tablet",
        352.32040177699974
    ],
    [
        "2019-11-17",
        "pubmatic",
        "Unknown",
        0.030084411
    ],
    [
        "2019-11-17",
        "rubicon",
        "Computer",
        164.47206542200007
    ],
    [
        "2019-11-17",
        "rubicon",
        "Digital media receiver",
        0.018821839000000003
    ],
    [
        "2019-11-17",
        "rubicon",
        "Game console",
        0.035865981
    ],
    [
        "2019-11-17",
        "rubicon",
        "Mobile",
        1236.6861955310017
    ],
    [
        "2019-11-17",
        "rubicon",
        "Tablet",
        77.79448947999998
    ],
...
]
```

</details>

#### Errors
When an error is encountered you will receive an HTTP status code along with a message and error code in the body of the response.

<details/>
<summary/>Error codes</summary>

Status Code | error | error_description
------------ | ------------- | -------------
400 | Incorrect publisher parameter value | There is no such publisher
400 | Incorrect date format. It should be in YYYY-MM-DD format | Incorrectly formatted date
500 | An error occurred during a request. | Internal Server Error – There was a problem with the API host server. Try again later.

</details>
