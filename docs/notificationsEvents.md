
# Handling Notification Events

## <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/f/fa/Apple_logo_black.svg/2000px-Apple_logo_black.svg.png" width=30/> iOS

When a push notification is received by the device, the application can be in one of the following states:

1. **Forground:** When the app is running and is used by the user right now; in this case, a `notificationReceivedForeground` event will be fired.
2. **Background:** When the app is running in a background state; in this case, a `notificationReceivedBackground` event will be fired.

Finally, when a notification is _opened_ by the device user (i.e. tapped-on), a `notificationOpened` event is fired.

Example:

```javascript
constructor() {
    this._boundOnNotificationReceivedForeground = this.onNotificationReceivedForeground.bind(this);
    this._boundOnNotificationReceivedBackground = this.onNotificationReceivedBackground.bind(this);
    this._boundOnNotificationOpened = this.onNotificationOpened.bind(this);
    
    NotificationsIOS.addEventListener('notificationReceivedForeground', this._boundOnNotificationReceivedForeground);
    NotificationsIOS.addEventListener('notificationReceivedBackground', this._boundOnNotificationReceivedBackground);
    NotificationsIOS.addEventListener('notificationOpened', this._boundOnNotificationOpened);
}

onNotificationReceivedForeground(notification) {
	console.log("Notification Received - Foreground", notification);
}

onNotificationReceivedBackground(notification) {
	console.log("Notification Received - Background", notification);
}

onNotificationOpened(notification) {
	console.log("Notification opened by device user", notification);
}

componentWillUnmount() {
	// Don't forget to remove the event listeners to prevent memory leaks!
	NotificationsIOS.removeEventListener('notificationReceivedForeground', this._boundOnNotificationReceivedForeground);
	NotificationsIOS.removeEventListener('notificationReceivedBackground', this._boundOnNotificationReceivedBackground);
	NotificationsIOS.removeEventListener('notificationOpened', this._boundOnNotificationOpened);
}
```

### Notification Object

When you receive a push notification, you'll get an instance of `IOSNotification` object, contains the following methods:

- **`getMessage()`**- returns the notification's main message string.
- **`getSound()`**- returns the sound string from the `aps` object.
- **`getBadgeCount()`**- returns the badge count number from the `aps` object.
- **`getCategory()`**- returns the category from the `aps` object (related to interactive notifications).
- **`getData()`**- returns the data payload (additional info) of the notification.
- **`getType()`**- returns `managed` for managed notifications, otherwise returns `regular`.

### Background Queue (Important - please read!)

When a push notification is opened but the app is not running, the application will be in a **cold launch** state, until the JS engine is up and ready to handle the notification.
The application will collect the events (notifications, actions, etc.) that happend during the cold launch for you. 

When your app is ready (most of the time it's after the call to `requestPermissions()`), just call to `NotificationsIOS.consumeBackgroundQueue();` in order to consume the background queue. For more info see `index.ios.js` in the example app.