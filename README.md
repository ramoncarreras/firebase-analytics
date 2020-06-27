# Capacitor Firebase Analytics Plugin

Capacitor community plugin for Firebase Analytics.

## Maintainers

| Maintainer     | GitHub                                                  | Social                                           | Sponsoring Company |
| -------------- | ------------------------------------------------------- | ------------------------------------------------ | ------------------ |
| Priyank Patel  | [priyankpat](https://github.com/priyankpat)             | [@priyankpat\_](https://twitter.com/priyankpat_) | Ionic              |
| Stewan Silva   | [stewwan](https://github.com/stewwan)                   | [@StewanSilva](https://twitter.com/StewanSilva)  | Ionic              |
| Daniel Pereira | [danielprrazevedo](https://github.com/danielprrazevedo) | [@DandanPrr](https://twitter.com/DandanPrr)      | Ionic              |

Maintenance Status: Actively Maintained

## Installation

Using npm:

```bash
npm install @capacitor-community/firebase-analytics
```

Using yarn:

```bash
yarn add @capacitor-community/firebase-analytics
```

Sync native files:

```bash
npx cap sync
```

On iOS, no further steps are needed.

On Android, register the plugin in your main activity:

```java
import com.getcapacitor.community.firebaseanalytics.FirebaseAnalytics;

public class MainActivity extends BridgeActivity {

  @Override
  public void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);

    // Initializes the Bridge
    this.init(
        savedInstanceState,
        new ArrayList<Class<? extends Plugin>>() {

          {
            // Additional plugins you've installed go here
            // Ex: add(TotallyAwesomePlugin.class);
            add(FirebaseAnalytics.class);
          }
        }
      );
  }
}
```

## Configuration

No configuration is required for this plugin.

## Examples

[Click here](https://github.com/priyankpat/capacitor-plugins-example/tree/firebase-analytics) for an example on how to implement this plugin.

You can also clone the repository:

```bash
git clone https://github.com/priyankpat/capacitor-plugins-example
git checkout -b firebase-analytics
```

## Supported methods

| Name             | Android | iOS | Web |
| :--------------- | :------ | :-- | :-- |
| setUserId        | ✅      | ✅  | ✅  |
| setUserProperty  | ✅      | ✅  | ✅  |
| getAppInstanceId | ✅      | ✅  | ❌  |
| setScreenName    | ✅      | ✅  | ❌  |
| reset            | ✅      | ✅  | ✅  |
| logEvent         | ✅      | ✅  | ✅  |
| enable           | ✅      | ✅  | ❌  |
| disable          | ✅      | ✅  | ❌  |

## Usage

```typescript
// Must import the package once to make sure the web support initializes
import "@capacitor/firebase-analytics";

import { Plugins } from "@capacitor/core";

const { FirebaseAnalytics } = Plugins;

/**
 * This method will allow you to set user id.
 * @param userId - unique identifier of a user
 * @returns void
 * https://firebase.google.com/docs/analytics/userid
 */
FirebaseAnalytics.setUserId({
  userId: "john_doe_123",
});

/**
 * This method will allow you to set user property.
 * @param userId - unique identifier of a user
 * @returns void
 * https://firebase.google.com/docs/analytics/user-properties
 */
FirebaseAnalytics.setUserProperty({
  name: "favorite_food",
  value: "pizza",
});

/**
 * This method will allow you to set user id.
 * @param none
 * @returns instanceId - individual instance id value
 * https://firebase.google.com/docs/analytics/user-properties
 */
FirebaseAnalytics.getAppInstanceId();

/**
 * This method will allow you to track screens.
 * @param screenName - name of the current screen to track
 *        nameOverride - name of the screen class to override
 * @returns instanceId - individual instance id value
 * https://firebase.google.com/docs/analytics/screenviews
 */
FirebaseAnalytics.setScreenName({
  screenName: "login",
  nameOverride: "LoginScreen",
});

/**
 * This method will clear all analytics data and reset the app instance id.
 * @param none
 * @returns void
 */
FirebaseAnalytics.reset();

/**
 * This method will log an app event.
 * @param name - name of the event to log
 *        params - key/value pairs of properties (25 maximum per event)
 * @returns void
 */
FirebaseAnalytics.logEvent({
  name: "select_content",
  params: {
    content_type: "image",
    content_id: "P12453",
    items: [{ name: "Kittens" }],
  },
});
```

## Setup

Navigate to the project settings page for your app on Firebase.

### iOS

Download the `GoogleService-Info.plist` file. In Xcode right-click on the yellow folder named "App" and select the `Add files to "App"`.

> Tip: if you drag and drop your file to this location, Xcode may not be able to find it.

### Android

Download the `google-services.json` file and copy it to `android/app/` directory of your capacitor project.

## iOS setup

- `ionic start my-cap-app --capacitor`
- `cd my-cap-app`
- `npm install --save @capacitor-community/analytics`
- `mkdir www && touch www/index.html`
- `sudo gem install cocoapods` (only once)
- `npx cap add ios`
- `npx cap sync ios` (every time you run `npm install`)
- `npx cap open ios`
- sign your app at xcode (general tab)
- add `GoogleService-Info.plist` to the app folder in xcode

### Enable debug view

1. In Xcode, select Product > Scheme > Edit scheme
2. Select Run from the left menu
3. Select the Arguments tab
4. In the Arguments Passed On Launch section, add `-FIRAnalyticsDebugEnabled`

> Tip: every time you change a native code you may need to clean up the cache (Product > Clean build folder) and then run the app again.

## Android setup

- `ionic start my-cap-app --capacitor`
- `cd my-cap-app`
- `npm install --save @capacitor-community/analytics`
- `mkdir www && touch www/index.html`
- `npx cap add android`
- `npx cap sync android` (every time you run `npm install`)
- `npx cap open android`
- add `google-services.json` to your `android/app` folder
- `[extra step]` in android case we need to tell Capacitor to initialise the plugin:

> on your `MainActivity.java` file add `import com.getcapacitor.community.firebaseanalytics.FirebaseAnalytics;` and then inside the init callback `add(AnalyticsPlugin.class);`

Now you should be set to go. Try to run your client using `ionic cap run android --livereload --address=0.0.0.0`.

> Tip: every time you change a native code you may need to clean up the cache (Build > Clean Project | Build > Rebuild Project) and then run the app again.

## Updating

For existing projects you can upgrade all capacitor related packages (including this plugin) with this single command

`npx npm-upgrade '*capacitor*' && npm install`

## Migration

If you were previously using the `capacitor-analytics` package from npm

1. rename dep in package.json from `capacitor-analytics` to `@capacitor-community/analytics`
2. on android's _MainActivity.java_ change the import path from `io.stewan.capacitor.analytics.AnalyticsPlugin;` to `com.getcapacitor.community.firebaseanalytics.FirebaseAnalytics;`
3. public api changes
   - `instance()` is now `getAppInstanceId()`
   - `setScreen()` is now `setScreenName()`
   - `setUserID()` is now `setUserId()`
   - `setUserProp()` us now `setUserProperty()`
