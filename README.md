# wind_turbine_etl

## Getting Started

### Create Volume in your Databricks Workspace

The 'wind_turbine_etl' project uses data from the data folder, which it is assumed has been added to a volume named ```wind_farm``` in location  ```/Volumes/wind_farm/default/source_data/ ``` 

You will need to create the equivalent in your Databricks environment and upload the csv files in the data folder

### Install Databrick CLI and Create dev and prod profiles 

1. Install the Databricks CLI from https://docs.databricks.com/dev-tools/cli/databricks-cli.html

2. Authenticate to your Databricks workspace, if you have not done so already:
    ```
    $ databricks configure
    ```
3. Create dev and prod profiles 

### Deploy Bundle

1. To deploy a development copy of this project, type:
    ```
    $ databricks bundle deploy --target dev
    ```
    (Note that "dev" is the default target, so the `--target` parameter
    is optional here.)

    This deploys everything that's defined for this project.
    For example, the default template would deploy a job called
    `[dev yourname] wind_turbine_etl_job` to your workspace.
    You can find that job by opening your workpace and clicking on **Workflows**.

2. Similarly, to deploy a production copy, type:
   ```
   $ databricks bundle deploy --target prod
   ```

   Note that the default job from the template has a schedule that runs every day
   (defined in resources/wind_turbine_etl.job.yml). The schedule
   is paused when deploying in development mode (see
   https://docs.databricks.com/dev-tools/bundles/deployment-modes.html).

3. To run a job or pipeline, use the "run" command:
   ```
   $ databricks bundle run
   ```

4. Optionally, install developer tools such as the Databricks extension for Visual Studio Code from
   https://docs.databricks.com/dev-tools/vscode-ext.html. Or read the "getting started" documentation for
   **Databricks Connect** for instructions on running the included Python code from a different IDE.

5. For documentation on the Databricks asset bundles format used
   for this project, and for CI/CD configuration, see
   https://docs.databricks.com/dev-tools/bundles/index.html.


### The Notebooks and Jobs

Once deployed, you will have jobs named:

- wind_turbine_etl_pipeline: DLT Job for loading data from source. The data is pushed through bronze and silver layers with validation
- wind_turbine_etl_job: Standard Databricks job used to write data to gold layer

These jobs use the following Python notebooks respectively:
- load_data_dlt
- analyse_data_and_write_to_gold


