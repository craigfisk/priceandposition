---
title: "How to set up Firebase Emulators"
date: 2022-01-11T23:07:30-06:00
draft: true
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

Firebase Emulators sound like a great idea. Run a dump of your cloud environment on localhost; it should safely avoid accidental expensive mistakes and be fast. The reality is that it there are a lot of edge cases to get right.

We will assume you already are using *gcloud* and have a Firebase (Google Cloud) project with authentication, a Firestore database, GCP Cloud Storage, and security rules for both of these. 

A) Install the Emulators
```javascript
    cd <project_directory>
    npm install -g firebase-tools 
    firebase init    // Creates firebase.json and .firebaserc
```

B) Download a Cloud backup of the project (as "dev-test" for this example) 

C) Modify app to use Emulators if on localhost
```javascript
    if (location.hostname === "localhost") {
        auth.useEmulator("http://localhost:9100");
        db.useEmulator("localhost", 8080);    // was 8081, changed 2022-1-11  
        projectStorage.useEmulator("localhost", 9199);
    }
    // Example is for Firebase 8
```

D) Start the Emulators:
```javascript
    firebase emulators:start 
    --import /<your_path>/Downloads/dev-test 
    --export-on-exit
    // Populates from "dev-test" and saves any changes there on exit
```

In case of a "port already in use" error: 
```javascript
    lsof -i:<port> // like 8080
    // returns PID; if multiple PIDs, pick the first
    sudo kill PID
```

c) Install the Firebase Emulators

In profiles-app directory, 

npm install -g firebase-tools  // package.json shows 9.23.0.
    // Use "npm list -g | grep firebase-tools" 
firebase login      // log in with your Google Marmalade account
firebase use marmalade-dev-test  // Shouldn't be necessary, if already in ENV
2022-1-9: firebase use --> marmalade-dev // wrong project! So
firebase use marmalade-dev-test and firebase use now shows marmalade-dev-test

2022-1-9: How do I set the "default" project to be "marmalade-dev-test"?
Frank van Puffelen answer on Stackoverflow: https://stackoverflow.com/questions/52344461/how-can-i-reset-the-default-project-hosting-with-firebase
    firebase use --add    // shows the list and you can select marmalade-dev-test and set as "default" when asked "what alias do you want to use for this project".

--> error: firebase use must be run from a Firebase project directory.
// This could mean you need to run "firebase init" in the current directory. 

Problem: I made a mistake. How do I delete "firebase init" and start over?
Solution: delete .firebaserc and firebase.json in the directory

firebase init   
    // select just firestore, emulators and storage; not functions, yet.
    // "use an existing project" --> pick "marmalade-dev-test"
    // What file should be used for Firestore Rules? (firestore.rules [default])
    // What file should be used for Firestore indexes: (firestore.indexes.json [default])
    // Storage? storage.rules
    // port 9199 is the default port for the Storage emulator
    // asks a second time; select Firestore, Storage, and Emulators
    // Existing project? or Overwrite? // yes to everything and default names
    // ESLint? Y
    // Install dependencies now? Y
    // runs for 30 seconds
    // Emulators for setup
    // select auth, firestore; skip functions, storage
    // port for auth? (9099 [default])
    // port for firestore? (8080 [default])
    // enable the Emulator UI? Y
    // port for Emulator UI? used 4000
    // download now? y
// laptop 2021-11-25: downloads 1.13.1
--> writing configuration info to firebase.json and project info to .firebaserc


#5 Running the profiles-app under VS Code using the Emulators

1) cd to project directory, check the ports in firebase.json // created by firebase init
    firestore 8080
    auth       9099

2) 2022-1-11: commented this out:
also check .vscode/launch.json should have a config line:
                "url": "http://localhost:8081",

3) In the profiles app, change firebase.js to use Emulators if on localhost:
        if (location.hostname === "localhost") {
    // Firebase 8; this changes if Firebase 9:
            auth.useEmulator("http://localhost:9100");
            db.useEmulator("localhost", 8080);    // was 8081, changed 2022-1-11    
        }

4) Start Emulators:
firebase emulators:start 
--import /home/fisk/Downloads/marmalade-dev-test 
--export-on-exit

- In case of a "port already in use" error: - lsof -i:<port> // like 8080, >> sudo kill PID








=========================
#4 Backup and download the Firestore database to the Emulators


[TBD. The profiles-app can switch among multiple databases. How to do this on the Emulators?]

3) environment variables (which I set in ~/.bashrc): 
export GOOGLE_APPLICATION_CREDENTIALS="/home/fisk/Downloads/marmalade-dev-test-firebase-adminsdk-wj2ra-187bb08aee.json"    // updated 2022-1-3

For GOOGLE_APPLICATION_CREDENTIALS, go to console.firebase.google.com > marmalade-dev-test > Settings > Project Settings > Service Accounts tab > select "Node.js" and "Generate new private key" which is then downloaded to your system. 

export CLOUDSDK_CORE_PROJECT='marmalade-dev-test'
export GCLOUD_PROJECT="marmalade-dev-test"

Save and source ~/.bashrc

b) Backup and download from GCP:project

2021-12-31 Trials and tribulations.
Summary of what worked (may well be a step or two that is incorrect or missing):
"[laptop]" = repeated this step for the laptop, after doing all steps on desktop.

[laptop][desktop]- Changed .bashrc so that all GOOGLE environment variables referenced "marmalade-dev-test" instead of "marmalade-dev." (and did "source .bashrc" to make the changes effective now).

[laptop][desktop]- In .bashrc, also changed GOOGLE_APPLICATION_CREDENTIALS from "/home/fisk/Downloads/marmalade-dev-firebase-adminsdk-kpwut-23ddeca1c0.json"
to "/home/fisk/Downloads/marmalade-dev-test-firebase-adminsdk-wj2ra-187bb08aee.json" which is the service account credential for marmalade-dev-test

[laptop][desktop]- Made sure that Cloud Console or Firebase Console was on project "marmalade-dev-test." (See results of "gcloud config list" for project, account, regions, zone).
- Use bucket named "marmalade-dev-test.appspot.com"; not "marmalade-dev-test" 
- Added a bucket permission via Cloud Console as a "role" "craigfisk@marmalade.ai" as Storage Admin.

Backup:
cd ~/Downloads
- Use gcloud instead of gsutil
    gcloud firestore export gs://marmalade-dev-test.appspot.com/marmalade-dev-test
    // This exports the firestore database to a bucket
Error: INVALID_ARGUMENT: Path already exists: /marmalade-dev-test.appspot.com/marmalade-dev-test/marmalade-dev-test.overall_export_metadata
--> delete the old export "folder" first

Now the latest in ~/Downloads/marmalade-dev-test is:
    marmalade-dev-test.appspot.com/marmalade-dev-test
at Jan 3, 2022, 11:31:50 AM

List:
    gsutil ls -la gs://marmalade-dev-test.appspot.com/
// results include
     gs://marmalade-dev-test.appspot.com/marmalade-dev-test/

Download:
On local system, 
    cd ~/Downloads
Delete the old directory, if there is one, before downloading:
    sudo rm -r marmalade-dev-test
    gsutil -m cp -r gs://marmalade-dev-test.appspot.com/marmalade-dev-test/ .

2022-1-13 if you mistakenly delete all the Firestore data in the Emulators and need to download it again, you need to delete the existing ~/Downloads/marmalade-dev-test first, or else the database will be empty.

2022-1-4 Craig note: Maybe I mistakenly moved section "c)" with the "firebase init" information into the appendix? Perhaps I didn't notice on the laptop because I had previously installed firebase-tools and done firebase init. In any case, now moving it back here:

c) Install the Firebase Emulators

In profiles-app directory, 

npm install -g firebase-tools  // package.json shows 9.23.0.
    // Use "npm list -g | grep firebase-tools" 
firebase login      // log in with your Google Marmalade account
firebase use marmalade-dev-test  // Shouldn't be necessary, if already in ENV
2022-1-9: firebase use --> marmalade-dev // wrong project! So
firebase use marmalade-dev-test and firebase use now shows marmalade-dev-test

2022-1-9: How do I set the "default" project to be "marmalade-dev-test"?
Frank van Puffelen answer on Stackoverflow: https://stackoverflow.com/questions/52344461/how-can-i-reset-the-default-project-hosting-with-firebase
    firebase use --add    // shows the list and you can select marmalade-dev-test and set as "default" when asked "what alias do you want to use for this project".

--> error: firebase use must be run from a Firebase project directory.
// This could mean you need to run "firebase init" in the current directory. 

Problem: I made a mistake. How do I delete "firebase init" and start over?
Solution: delete .firebaserc and firebase.json in the directory

firebase init   
    // select just firestore, emulators and storage; not functions, yet.
    // "use an existing project" --> pick "marmalade-dev-test"
    // What file should be used for Firestore Rules? (firestore.rules [default])
    // What file should be used for Firestore indexes: (firestore.indexes.json [default])
    // Storage? storage.rules
    // port 9199 is the default port for the Storage emulator
    // now asks a second time and I select Firestore, Storage, and Emulators
    // Existing project? or Overwrite? // yes to everything and default names
    // ESLint? Y
    // Install dependencies now? Y
    // runs for 30 seconds
    // Emulators for setup
    // select auth, firestore; skip functions, storage
    // port for auth? (9099 [default])
    // port for firestore? (8080 [default])
    // enable the Emulator UI? Y
    // port for Emulator UI? used 4000
    // download now? y
// laptop 2021-11-25: downloads 1.13.1
--> writing configuration info to firebase.json and project info to .firebaserc


#5 Running the profiles-app under VS Code using the Emulators

1) cd to project directory, check the ports in firebase.json // created by firebase init
    firestore 8080
    auth       9099

2) 2022-1-11: commented this out:
also check .vscode/launch.json should have a config line:
                "url": "http://localhost:8081",

3) In the profiles app, change firebase.js to use Emulators if on localhost:
        if (location.hostname === "localhost") {
    // Firebase 8; this changes if Firebase 9:
            auth.useEmulator("http://localhost:9100");
            db.useEmulator("localhost", 8080);    // was 8081, changed 2022-1-11    
        }

4) Start Emulators:
firebase emulators:start 
--import /home/fisk/Downloads/marmalade-dev-test 
--export-on-exit

- In case of a "port already in use" error: - lsof -i:<port> // like 8080, >> sudo kill PID
- In case of logging in with a registered account and error: "A network error (such as timeout, interrupted connection or unreachable host) has occurred." --> emulators are running?
- In case of running emulators, starting the app in VS Code, logging in and having the app go to "Profiles" tab and show no profiles, probably means you need to refresh the page.

5) In VS Code new terminal
        npm run serve

ctrl-click to open app on Local: http://localhost:8081  

// 2022-1-11: commented out
2022-1-4: Set .vscode/launch.json "url" field to 8081 instead of 8080. 

Network://192.168.x.y:8081/ runs against the cloud data instead.
 
Notes:
- Everyone has the puppy photo. This will be fixed when photo_url uses Cloud Storage.
- Refresh? Register a new user and profiles tab doesn't refresh automatically. [2022-1-4: check // confirmed 2022-1-11: that this is not necessary if .vscode/launch.json sets url to 8081 instead of 8080 and just registered; if logging in a different, authenticated user, it needs to be refreshed. 2022-1-11: But what impact does that have on non-emulator operation?]
- Test 2022-1-11: Start the emulators, start and open the app, register a new user. Now open Emulators at port 4000 to confirm the user is in both the Firestore collection and the authenticated users list. 
- Changes to local emulator Firestore data are reflected immediately in the app, (2022-1-11: if you refresh the app)
