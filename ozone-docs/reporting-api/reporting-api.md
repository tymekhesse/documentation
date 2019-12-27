


// colors
s { color: green }
em { color: blue }
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
publisher | **string** (required) | one of the available publishers: *{guardian, news-uk, telegraph, reach, the-stylist-group, ozone}*, ozone means selecting all available publishers.
start_date | **string** (required) |  starting date in YYYY-MM-DD format
start_date | **string** (required) |  end date in YYYY-MM-DD format

</details>

<details closed>
<summary>Example</summary>
That command will build docker image (only in first execution) and start docker container.

Documentation is available on [http://localhost:4567](http://localhost:4567) address.

### How to add new project docs
1. Clone this project (ozone-docs).
2. Add empty project.
    <details open>
    <summary>Run scripts/add-project.sh</summary>

    ```shell
    ./scripts/add-project.sh <PROJECT_NAME>
    ```
    </details>
3. Run ozone-docs and go to [http://localhost:4567](http://localhost:4567).
    <details open>
    <summary>Run scripts/run-dev.sh</summary>

    ```shell
    ./scripts/run-dev.sh
    ```
    </details>
4. Make modifications in documentation and move **source/includes/partials/generated/<PROJECT_NAME>** folder to **ozone-docs/** in modified project.

### How to edit project docs
1. Clone this project (ozone-docs).
2. Create alias for edit ozone-docs command.
    <details open>
    <summary>~/.bashrc</summary>

    ```shell
    alias edit-ozone-docs='/bin/bash <PATH TO ozone-docs>/scripts/run-dev.sh $(pwd)/ozone-docs'
    ```
    </details>
3. Reload *.bashrc* file, go into root of your project and start editing with *edit-ozone-docs* command.
    <details open>
    <summary>Reload and start editing ozone-docs</summary>

    ```shell
    source ~/.bashrc
    edit-ozone-docs
    ```
    </details>
4. Every modification made in project affects documentation and is visible on [http://localhost:4567](http://localhost:4567).
