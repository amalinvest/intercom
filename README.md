<p align="center"><br><img src="https://user-images.githubusercontent.com/236501/85893648-1c92e880-b7a8-11ea-926d-95355b8175c7.png" width="128" height="128" /></p>
<h3 align="center">Capacitor Intercom</h3>
<p align="center"><strong><code>@capacitor-community/intercom</code></strong></p>
<p align="center">
  Capacitor community plugin for enabling Intercom capabilities
</p>

<p align="center">
  <img src="https://img.shields.io/maintenance/yes/2022?style=flat-square" />
  <a href="https://www.npmjs.com/package/@capacitor-community/intercom"><img src="https://img.shields.io/npm/l/@capacitor-community/intercom?style=flat-square" /></a>
<br>
  <a href="https://www.npmjs.com/package/@capacitor-community/intercom"><img src="https://img.shields.io/npm/dw/@capacitor-community/intercom?style=flat-square" /></a>
  <a href="https://www.npmjs.com/package/@capacitor-community/intercom"><img src="https://img.shields.io/npm/v/@capacitor-community/intercom?style=flat-square" /></a>
  <!-- ALL-CONTRIBUTORS-BADGE:START - Do not remove or modify this section -->
<a href="#contributors"><img src="https://img.shields.io/badge/all%20contributors-9-orange?style=flat-square" /></a>
<!-- ALL-CONTRIBUTORS-BADGE:END -->
</p>

## Sponsors

<table>
  <tr>
    <td align="center">
      <a href="https://intenseloop.com">
      <img src="https://static.intenseloop.com/assets/logo-512x512.png" width="40" />
      </a>
    </td>
    <td>
      <a href="https://intenseloop.com">
      Intenseloop
      </a>
    </td>
  </tr>
</table>

## Maintainers

| Maintainer   | GitHub                                  | Social                                    |
| ------------ | --------------------------------------- | ----------------------------------------- |
| Stewan Silva | [stewones](https://github.com/stewones) | [@stewones](https://twitter.com/stewones) |

## Notice 🚀

We're starting fresh under an official org. If you were using the previous npm package `capacitor-intercom`, please update your package.json to `@capacitor-community/intercom`. Check out [changelog](/CHANGELOG.md) for more info.

## Installation

Using npm:
~~npm install @capacitor-community/intercom~~
```bash
npm install https://github.com/amalinvest/intercom --save
```

Using yarn:
~~yarn add @capacitor-community/intercom~~
```bash
yarn add https://github.com/amalinvest/intercom 
```

Sync native files:

```bash
npx cap sync
```

## API

- registerIdentifiedUser
- registerUnidentifiedUser
- updateUser
- logout
- logEvent
- displayMessenger
- displayMessageComposer
- displayHelpCenter
- hideMessenger
- displayLauncher
- hideLauncher
- displayInAppMessages
- hideInAppMessages
- displayCarousel
- setUserHash
- setBottomPadding

## Usage

```js
import { Intercom } from '@capacitor-community/intercom';
import { PushNotifications } from '@capacitor/push-notifications';

// Register for push notifications from Intercom
PushNotifications.register();

// Register an indetified user
Intercom.registerIdentifiedUser({ userId: 123456 });
Intercom.registerIdentifiedUser({ email: 'test@example.com' });
Intercom.registerIdentifiedUser({ userId: 123456, email: 'test@example.com' });

// Register a log event
Intercom.logEvent({ name: 'my-event', data: { pi: 3.14 } });

// Display the message composer
Intercom.displayMessageComposer({ message: 'Hello there!' });

// Identity Verification
// https://developers.intercom.com/installing-intercom/docs/ios-identity-verification
Intercom.setUserHash({ hmac: 'xyz' });
```

## iOS setup

- add intercom keys to capacitor's configuration file

```
{
 …
  "plugins": {
   "Intercom": {
      "iosApiKey": "ios_sdk-xxx",
      "iosAppId": "yyy"
    }
  }
…
}
```
- `npx cap run ios`
> Tip: every time you change a native code you may need to clean up the cache (Product > Clean build folder) and then run the app again.

## Android setup

1. Add intercom keys to capacitor's configuration file

```
{
 …
  "plugins": {
   "Intercom": {
      "androidApiKey": "android_sdk-xxx",
      "androidAppId": "yyy"
    }
  }
…
}
```

- `npx cap run android`

Now you should be set to go. Try to run your client using `ionic cap run android --livereload`.

> Tip: every time you change a native code you may need to clean up the cache (Build > Clean Project | Build > Rebuild Project) and then run the app again.

2. Add this dependecy to `android/app/build.gradle`
```gradle
dependencies {
     implementation 'com.google.firebase:firebase-messaging:20.2.+'
}
```

3. Create a new file `android/app/src/main/java/com/YOUR_APP/PushNotificationService.java` that extends `FirebaseMesssagingService` if you dont have one already.

  ```java
  package com.YOUR_APP;

  import com.google.firebase.messaging.FirebaseMessagingService;
  import com.google.firebase.messaging.RemoteMessage;
  import com.getcapacitor.community.intercom.IntercomPlugin;

  public class PushNotificationService extends FirebaseMessagingService {

   @Override
    public void onNewToken(String refreshedToken) {
      IntercomPlugin.sendTokenToIntercom(getApplication(), refreshedToken);
    }

   public void onMessageReceived(RemoteMessage remoteMessage) {
      if (IntercomPlugin.isIntercomPush(remoteMessage)) {
        IntercomPlugin.handleRemotePushMessage(getApplication(), remoteMessage);
     }
    }
  } 
```
4. Then add the following code to `android/app/src/main/AndroidManifest.xml`
 ```xml
       <service 
         android:name=".PushNotificationService"
         android:enabled="true"
         android:exported="true">
          <intent-filter>
             <action android:name="com.google.firebase.MESSAGING_EVENT" />
          </intent-filter>
       </service>
    </application>
</manifest>
  ```
## License

MIT

## Example

- https://github.com/capacitor-community/intercom/blob/master/example

## Contributors ✨

Thanks goes to these wonderful people ([emoji key](https://allcontributors.org/docs/en/emoji-key)):

<!-- ALL-CONTRIBUTORS-LIST:START - Do not remove or modify this section -->
<!-- prettier-ignore-start -->
<!-- markdownlint-disable -->
<table>
  <tr>
    <td align="center"><a href="https://twitter.com/stewones"><img src="https://avatars1.githubusercontent.com/u/719763?v=4?s=75" width="75px;" alt=""/><br /><sub><b>Stew</b></sub></a><br /><a href="https://github.com/capacitor-community/intercom/commits?author=stewones" title="Code">💻</a> <a href="https://github.com/capacitor-community/intercom/commits?author=stewones" title="Documentation">📖</a></td>
    <td align="center"><a href="https://davidseek.com/"><img src="https://avatars2.githubusercontent.com/u/17073950?v=4?s=75" width="75px;" alt=""/><br /><sub><b>David Seek</b></sub></a><br /><a href="https://github.com/capacitor-community/intercom/commits?author=davidseek" title="Code">💻</a></td>
    <td align="center"><a href="https://github.com/rnikitin"><img src="https://avatars3.githubusercontent.com/u/1829318?v=4?s=75" width="75px;" alt=""/><br /><sub><b>Roman Nikitin</b></sub></a><br /><a href="https://github.com/capacitor-community/intercom/commits?author=rnikitin" title="Code">💻</a></td>
    <td align="center"><a href="https://github.com/atomassoni"><img src="https://avatars1.githubusercontent.com/u/17362459?v=4?s=75" width="75px;" alt=""/><br /><sub><b>Anne Tomassoni</b></sub></a><br /><a href="https://github.com/capacitor-community/intercom/commits?author=atomassoni" title="Code">💻</a> <a href="https://github.com/capacitor-community/intercom/pulls?q=is%3Apr+reviewed-by%3Aatomassoni" title="Reviewed Pull Requests">👀</a></td>
    <td align="center"><a href="https://github.com/mmodzelewski"><img src="https://avatars2.githubusercontent.com/u/7762633?v=4?s=75" width="75px;" alt=""/><br /><sub><b>Maciej Modzelewski</b></sub></a><br /><a href="https://github.com/capacitor-community/intercom/commits?author=mmodzelewski" title="Code">💻</a></td>
    <td align="center"><a href="https://github.com/spaghettiguru"><img src="https://avatars.githubusercontent.com/u/5624009?v=4?s=75" width="75px;" alt=""/><br /><sub><b>Oleg Yuzvik</b></sub></a><br /><a href="#maintenance-spaghettiguru" title="Maintenance">🚧</a></td>
    <td align="center"><a href="https://github.com/gcorreaalves"><img src="https://avatars.githubusercontent.com/u/983426?v=4?s=75" width="75px;" alt=""/><br /><sub><b>Gustavo Corrêa Alves</b></sub></a><br /><a href="https://github.com/capacitor-community/intercom/commits?author=gcorreaalves" title="Documentation">📖</a></td>
  </tr>
  <tr>
    <td align="center"><a href="https://github.com/Jealvia"><img src="https://avatars.githubusercontent.com/u/28424830?v=4?s=75" width="75px;" alt=""/><br /><sub><b>Jealvia</b></sub></a><br /><a href="#maintenance-Jealvia" title="Maintenance">🚧</a></td>
    <td align="center"><a href="https://adamduren.com/"><img src="https://avatars.githubusercontent.com/u/581097?v=4?s=75" width="75px;" alt=""/><br /><sub><b>Adam Duren</b></sub></a><br /><a href="https://github.com/capacitor-community/intercom/commits?author=adamduren" title="Code">💻</a> <a href="#maintenance-adamduren" title="Maintenance">🚧</a></td>
  </tr>
</table>

<!-- markdownlint-restore -->
<!-- prettier-ignore-end -->

<!-- ALL-CONTRIBUTORS-LIST:END -->

This project follows the [all-contributors](https://github.com/all-contributors/all-contributors) specification. Contributions of any kind welcome!
