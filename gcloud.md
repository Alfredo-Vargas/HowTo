# Commands for gcloud

## How to enable Google Cloud Platform
   - First we go to the Admin Console and go to apps and additional Google Services.
   - We select and enable the desired service "Google Cloud Platform" (be mindful of the OUs inheritance).
   - Click the Google Cloud Platform and tick the box to allow users to make projects in Google Cloud Platform.

## How to know which account is active and which project is active
   @code bash
   gcloud auth list && gcloud config configurations list && gcloud config get-value project
   @end

## How to which account is active
   @code powershell
   gcloud auth list
   @end

## How to authenticate with Google Cloud CLI
   @code powershell
   gcloud auth login
   @end

## How to inititialize, authorize, and configure the gcloud tool.
   @code powershell
   gcloud init
   @end

## How to create a new project
   @code bash
   gcloud
   gcloud projects create PROJECT-ID --name="<PROJECT-NAME>"
   @end

## How to see the project name if a project is active (otherwise output = unset)
   @code powershell
   gcloud config get-value project
   @end

## How to list all availables projects in current account
   @code powershell
   gcloud projects list
   @end

## How to select a project
   @code powershell
   gcloud config set project <PROJECT-ID>
   @end

## How to enable the Admin SDK API
   @code powershell
   gcloud services enable admin.googleapis.com
   @end

## How to register the app using OAuth
   - After a project was created go into the Google Cloud Console, then go to APIs & Services and then to OAuth consent screen. Select Internal.
   - Give the app information.
   - In scopes just save and continue.
   - Now go to credentials and create an OAuth 2.0 Client IDs. This will grant you the config.json file.

## How to access the cheat sheet in the terminal
   @code powershell
   gcloud cheat-sheet
   @end


## How to list the gcloud available configurations
   @code powershell
   gcloud config configurations list
   @end

## How to change the configuration
   @code powershell
   gcloud config configurations activate <CONFIG-NAME>
   @end

## How to display the version and installed components
   @code powershell
   gcloud version
   @end

## How to install specific components
   @code powershell
   gcloud components install
   @end
