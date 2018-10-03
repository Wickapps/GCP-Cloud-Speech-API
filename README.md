# Google Cloud Speech API examples

This project is covered in Chapter 3 of the [book](https://www.apress.com/us/book/9781484239506):

![](fig-cover-sm.jpg)

This repository is a clone of the
[Google Cloud Speech API](https://cloud.google.com/speech/). 

# Project References
Project Name: GCP Cloud Speech API

Source: Github Google Cloud Speech Platform

Type: Android Application

# Key File Summary
| File | Description
| :--- | : ---
| app->src->main->java->MainActivity.java | The main activity that checks for device permissions, launches the voice recorder and speech service, and sets up the main view. 
| app->src->main->java->SpeechService.java | Service for handling API access. This Android Service implements the interface to the GCP Cloud Speech API, including authentication and real-time streaming of spoken words.
| app->src->main->java->MessageDialogFragment.java | A simple Android Dialog class that the app uses to display messages to the user.
| app->src->main->java->VoiceRecorder.java | This class implements the Android AudioRecord class for voice recording.
| app->src->main->res->layout->main.xml | Main XML layout.
| app->src->main->res->raw->credential.json | JSON credential file created on the GCP Cloud API Center. Place the file into the res/raw folder.
| app->src->main->res->raw->audio.raw | A sample audio file stored into /res/raw folder that can be sent to the API for classification. The audio file is a recording of the spoken words "how old is the Brooklyn Bridge".
| app->src->main->AndroidManifest.xml | App manifest file. Define the activity and the service.

## Prerequisites

### Enable the Speech API

If you have not already done so,
[enable the Google Speech API for your project](https://cloud.google.com/speech/docs/getting-started). You
must be whitelisted to do this.

### Set Up to Authenticate With Your Project's Credentials

This Android app uses JSON credential file locally stored in the resources. ***You should not do
this in your production app.*** Instead, you should set up your own backend server that
authenticates app users. The server should delegate API calls from your client app. This way, you
can enforce usage quota per user. Alternatively, you should get the access token on the server side,
and supply client app with it. The access token will expire in a short while.

In this sample, we just put the Service Account in the client for ease of use. The app still gets
an access token using the service account credential, and use the token to call the API, so you can
see how to do so.

In order to try out this sample, visit the [Cloud Console](https://console.cloud.google.com/), and
navigate to:
`API Manager > Credentials > Create credentials > Service account key > New service account`.
Create a new service account, and download the JSON credentials file. Put the file in the app
resources as `app/src/main/res/raw/credential.json`.

Again, ***you should not do this in your production app.***

See the [Cloud Platform Auth Guide](https://cloud.google.com/docs/authentication#developer_workflow)
for more information.

### Test

Before running tests update the following environment variable with the service
account:

    GOOGLE_APPLICATION=service-account.json

This environment variable will be used to update the service account used here
`app/src/main/res/raw/credential.json`.

Run tests by using:

    gradle test

### Build signed release

*This step is optional.*

This sample uses ProGuard to decrease the number of methods generated by the gRPC library. It is
enabled by default for release build. If you want to build it, change the path, alias and passwords
of the keystore file specified in gradle.properties.
