![image](https://github.com/eslam-hegazy/ci_cd/assets/73136746/8d8d367f-ef3d-4bc8-865b-5ce0c46faacb)

## Streamlining Flutter App Deployment with Firebase Distribution and Fastlan
Continuous Integration (CI) and Continuous Deployment (CD) are pivotal in modern app development to ensure seamless and efficient workflows. Leveraging Firebase App Distribution and Fastlane, you can automate the build and deployment processes for your Flutter apps. This post will guide you through setting up CI/CD pipelines using Firebase App Distribution and Fastlane, integrating them with your Flutter project, and connecting to Firebase for a comprehensive deployment solution.

### Prerequisites
Before we dive into the setup, ensure you have the following:

1. A Flutter project.
2. Firebase CLI installed (npm install -g firebase-tools).
3. A Firebase project configured for your app.
4. Fastlane installed (gem install fastlane).
5. Deploy your app to Firebase App Distribution services using fastlane.

### 1- A Flutter project

Create a New Flutter Project
```dart
flutter create ci_cd
```
### 2- Firebase CLI installed (npm install -g firebase-tools)

Ensure you have Node.js and npm installed. Then, install the Firebase CLI globally using the following command:
```sh
npm install -g firebase-tools
```
### 3- A Firebase project configured for your app

- Create a Firebase Project: Go to the [Firebase Console](https://console.firebase.google.com/), create a new project or select an existing one.
- If you haven't already, [install the Firebase CLI](https://firebase.google.com/docs/cli#setup_update_cli).
- Log into Firebase using your Google account by running the following command:
```dart
firebase login
```
- Install the FlutterFire CLI by running the following command from any directory:
```dart
dart pub global activate flutterfire_cli
```
- Configure your apps to use Firebase
```dart
flutterfire configure
```
- flutter pub add firebase_core
```dart
flutter pub add firebase_core
```
Now you link with firebase

### 4- Fastlane installed (gem install fastlane)
To install and set up a Fastlane environment for your Flutter project

```sh
gem install fastlane
```

#### Setting up fastlane
Navigate your terminal to your project's directory and run
this route
```dart
cd android
fastlane init
```
You'll be asked to confirm that you're ready to begin, and then for a few pieces of information. To get started quickly:
1. Provide the package name for your application when asked (e.g. io.fabric.yourapp)
2. Press enter when asked for the path to your json secret file
3. Answer 'n' when asked if you plan on uploading info to Google Play via fastlane (we can set this up later)
That's it! fastlane will automatically generate a configuration for you based on the information provided.

![image](https://github.com/eslam-hegazy/ci_cd/assets/73136746/a3100959-ee5d-4e04-b0a6-cc501857d8c5)

#### 5- Deploy your app to Firebase App Distribution services using fastlane
- Ensure you enable Firebase App Distribution.

```sh
fastlane add_plugin firebase_app_distribution
```

![image](https://github.com/eslam-hegazy/ci_cd/assets/73136746/05e9b440-3f2a-409d-8ee9-fd2e07bfac2a)



- Open Fastfile
![image](https://github.com/eslam-hegazy/ci_cd/assets/73136746/0b3692f2-88d6-4cad-b98f-3c129a43b7f2)
- edit this file with this scription

```sh
default_platform(:android)

platform :android do
  desc "Runs all the tests"
  lane :firebase_distribution do
    sh "flutter clean"
    sh "flutter build apk"
    firebase_app_distribution(
    app: "1:861645517091:android:5cd5206ed9c67dae4b5c96",
    firebase_cli_token: "1//03C0gsxejj-LcCgYIARAAGAMSNwF-L9IrksgJySiFV2PAHZll8bXq4yBMPMma-k9nK4w97Grm4xar_bR-fNdGMFYs3bIiB2byNwk",
    android_artifact_type: "APK",
    android_artifact_path: "../build/app/outputs/flutter-apk/app-release.apk",
    testers: "eslamhegazy968@gmail.com",
    release_notes: "Testing something with GitHub Actions, trying to push directly from master branch",
 )
  end
end

```
1. firebase_distribution: You can replace this name with any another name.
2. app: You can get from your App ID in firebase project.
3. firebase_cli_token: can you get firebase_cli_token by this steps:
```sh
firebase login:ci
```
![image](https://github.com/eslam-hegazy/ci_cd/assets/73136746/945b0468-7a2d-4eea-b05b-3a98f0201d42)

firebase_distribution:- 1//03C0gsxejj-LcCgYIARAAGAMSNwF-L9IrksgJySiFV2PAHZll8bXq4yBMPMma-k9nK4w97Grm4xar_bR-fNdGMFYs3bIiB2byNwk

#### Then you can run this command to upload to firebase distribution
```sh
fastlane android firebase_distribution
```

![image](https://github.com/eslam-hegazy/ci_cd/assets/73136746/9fcc86f8-dc60-447a-a990-56b7b743d407)

![image](https://github.com/eslam-hegazy/ci_cd/assets/73136746/c3863169-9a7d-4835-9822-d0750648e4dc)


By following these steps, you've successfully set up a CI/CD pipeline using Firebase Distribution and Fastlane for your Flutter app. This setup ensures that every change you push to your repository can be automatically built, tested, and distributed to your testers, allowing for a more efficient and streamlined development process. Happy coding!

