# Commands for gcloud

## How to enable Google Cloud Platform
   - First we go to the Admin Console and go to apps and additional Google Services.
   - We select and enable the desired service "Google Cloud Platform" (be mindful of the OUs inheritance).
   - Click the Google Cloud Platform and tick the box to allow users to make projects in Google Cloud Platform.

## How to know which account is active and which project is active
   ```bash
   gcloud auth list && gcloud config configurations list && gcloud config get-value project
   ```

## How to which account is active
   ```bash
   gcloud auth list
   ```

## How to authenticate with Google Cloud CLI
   ```bash
   gcloud auth login
   ```

## How to inititialize, authorize, and configure the gcloud tool.
   ```bash
   gcloud init
   ```

## How to create a new project
   ```bash
   gcloud
   gcloud projects create PROJECT-ID --name="<PROJECT-NAME>"
   ```

## How to see the project name if a project is active (otherwise output = unset)
   ```bash
   gcloud config get-value project
   ```

## How to list all availables projects in current account
   ```bash
   gcloud projects list
   ```

## How to select a project
   ```bash
   gcloud config set project <PROJECT-ID>
   ```

## How to enable the Admin SDK API
   ```bash
   gcloud services enable admin.googleapis.com
   ```

## How to register the app using OAuth
   - After a project was created go into the Google Cloud Console, then go to APIs & Services and then to OAuth consent screen. Select Internal.
   - Give the app information.
   - In scopes just save and continue.
   - Now go to credentials and create an OAuth 2.0 Client IDs. This will grant you the config.json file.

## How to access the cheat sheet in the terminal
   ```bash
   gcloud cheat-sheet
   ```


## How to list the gcloud available configurations
   ```bash
   gcloud config configurations list
   ```

## How to change the configuration
   ```bash
   gcloud config configurations activate <CONFIG-NAME>
   ```

## How to display the version and installed components
   ```bash
   gcloud version
   ```

## How to install specific components
   ```bash
   gcloud components install
   ```
