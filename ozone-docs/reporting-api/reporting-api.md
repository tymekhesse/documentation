## reporting-api
This proof of concept is to determine whether the Admin UI’s current charting capability is the most suitable environment to build the Publisher Analytics suite.

### Errors
When an error is encountered you will receive an HTTP status code along with a message and error code in the body of the response.

Status Code | error | error_description
------------ | ------------- | -------------
400 | Incorrect publisher parameter value | There is no such publisher
400 | Incorrect date format. It should be in YYYY-MM-DD format | Incorrectly formatted date
500 | An error occurred during a request. | Internal Server Error – There was a problem with the API host server. Try again later.



### available fields endpoint
<details open>
<summary>Execute scripts/run-dev.sh script</summary>

```shell
GET /kpi/publisher-analytics-available-fields?publisher=the-stylist-group&start_date={start_date}&end_date={end_date}
```
</details>

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