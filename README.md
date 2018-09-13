# React Native Notifications [![Build Status](https://travis-ci.org/wix/react-native-notifications.svg)](https://travis-ci.org/wix/react-native-notifications)

Handle all the aspects of push notifications for your app, including remote and local notifications, interactive notifications, silent notifications, and more.

**All the native iOS notifications features are supported!** 

### iOS

<img src="https://s3.amazonaws.com/nrjio/interactive.gif" alt="Interactive notifications example" width=350/>

- Remote (push) notifications
- Local notifications
- Background/Managed notifications (notifications that can be cleared from the server, like Facebook messenger and Whatsapp web)
- PushKit API (for VoIP and other background messages)
- Interactive notifications (allows you to provide additional functionality to your users outside of your application such as action buttons)

# Table of Content

- [Installation and setup](./docs/installation.md) - Setting up the library in your app
- [Subscription](./docs/subscription.md) - Signing in to push notifications vendors (e.g. GCM)
- [Notification Events (notifications core)](./docs/notificationsEvents.md) - Handling push notification arrival, notification opening by users
- [Local notifications](./docs/localNotifications.md) - Manually triggering notifications (i.e. not via push)
- [Advanced iOS topics](./docs/advancedIos.md) - e.g. managed notifications, PushKit API, Notifications actions

# License
The MIT License.

See [LICENSE](LICENSE)
