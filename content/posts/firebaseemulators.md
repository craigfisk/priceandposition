---
title: "How to set up Firebase Emulators"
date: 2022-12-11T23:07:30-06:00
draft: false
tags: ["Firebase Emulators", "Google Firebase Emulators", "Emulators"]
author: "Craig Fisk"
# author: ["Me", "You"] # multiple authors
showToc: true
TocOpen: false
hidemeta: false
comments: false
description: "Google's Firebase Emulators promise to make development fast and cheap."
canonicalURL: "https://priceandposition.com/content/"
disableHLJS: true # to disable highlightjs
disableShare: false
disableHLJS: false
hideSummary: false
searchHidden: true
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
cover:
    image: "<image path/url>" # image path/url
    alt: "<alt text>" # alt text
    caption: "<text>" # display caption under cover
    relative: false # when using page bundles set this to true
    hidden: true # only hide on current single page
editPost:
    URL: "https://github.com/<path_to_repo>/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link


---

<!-- pexels-quang-nguyen-vinh-2166711.jpg Photo by Quang Nguyen Vinh from Pexels -->

{{< figure src="/image/pexels-quang-nguyen-vinh-2166711.jpg" caption="Using Firebase Emulators to mirror development on your local system: free, fast." >}}

**Firebase Emulators sound like a great idea**. Run an extract of your cloud environment on localhost, Avoid expensive accidents in the cloud. Be fast. The reality, hoever, is that there are a lot of little **problems** to deal with.

Let's assume you already have ***gcloud*** set up, and have a **Firebase project** named *dev-test* with authentication, a Firestore database, Storage, and security rules for both of the latter. 

1) **Install** the Emulators
```javascript
    cd <project_directory>
    gcloud auth login
    gcloud config set project PROJECT_ID
    firebase login
    firebase use dev-test   // "firebase use" to show the current project
    npm install -g firebase-tools 
    firebase init    
    // Use the defaults. If you need to start over; delete .firebaserc and firebase.json 
```

2) **Backup and download** the Firebase project ("dev-test" for this example) 
```javascript
    cd ~/Downloads    
    gcloud firestore export gs://<your_project>-dev-test.appspot.com/dev-test
    //?? vs.: console > Databases > Firestore > Import and Export > Export on <project> export entire database > chose destination > Export
    // Note: Kristofer Källsbo, "Export Firestore to dev environment" 
    // (https://hackviking.com/2021/10/20/export-firestore-to-dev-environment/) says to use gcloud 
    // instead of the console, which may add special characters that prevent downloading the data.
    gsutil ls -la gs://<your_project>-dev-test.appspot.com/
    // vs.: console > storage > cloud storage > browser
    gsutil -m cp -r gs://<your_project>-dev-test/dev-test/ .
    // Delete the old directory, if there is one, before downloading
```

3) **Modify app** to use Emulators **for *localhost***
```javascript
    if (location.hostname === "localhost") {
        auth.useEmulator("http://localhost:9100");
        db.useEmulator("localhost", 8080);     
        projectStorage.useEmulator("localhost", 9199);
    }
    // Example is for Firebase 8 in firebase.js
    // .vscode/launch.json should have a line:
        "url": "http://localhost:8081",
```

4) **Start** the Emulators using your **download**:
```javascript
    firebase emulators:start 
    --import /<your_path>/Downloads/dev-test 
    --export-on-exit
    // Populates from "dev-test" and saves any changes there on exit.
    // Argh! Be sure to use absolute path above to the download.
```

5) **Launch and run** the project in VS Code:
```javascript
    npm run serve   // ctrl-click to open app on http://localhost:8081
```
Wow, that was easy! ;) 


Notes:

In case of a **"port already in use"** error: 
```javascript
    lsof -i:<port> // like 8080
    // returns PID; if multiple PIDs, pick the first
    sudo kill PID
```
To see **project** information:
```javascript
    gcloud config list     
```
To run on local network, like to check out your **app over wifi on a phone**:
```javascript
    // Use *ifconfig* to get your network IP: 192.168.x.y
    http://192.168.x.y:8081/
```
To have correct **permissions** on your "bucket" for your backup, you may need to add your account as **"new principal"** with role of **"Storage Admin."** ERROR: PERMISSION_DENIED: Service account does not have access to Google Cloud Storage file. See https://cloud.google.com/datastore/docs/export-import-entities#permissions for a list of permissions needed. Error details: account does not have storage.buckets.get access to the Google Cloud Storage bucket.


When creating a bucket, **by default no security** settings are defined, so come back to this and define some security settings.

For more information, see **Jorge Vergara** (JS Mobile Dev), ["How to set up Firebase Emulator for local development."](https://jsmobiledev.com/article/firebase-emulator/) 
