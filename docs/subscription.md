# Push Notifications Subscription

The typical flow for subscribing a device for receiving push notification in real time is to first register the device with APNS, then publish the received token to your own push management servers.

This section is about the first part of the flow.

## <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/f/fa/Apple_logo_black.svg/2000px-Apple_logo_black.svg.png" width=30/> iOS

In order to handle notifications, you must register the `remoteNotificationsRegistered` event beforehand.


In your React Native app:

```javascript
import NotificationsIOS from 'react-native-notifications';

class App extends Component {
	constructor() {
		NotificationsIOS.addEventListener('remoteNotificationsRegistered', this.onPushRegistered.bind(this));
		NotificationsIOS.addEventListener('remoteNotificationsRegistrationFailed', this.onPushRegistrationFailed.bind(this));
		NotificationsIOS.requestPermissions();
	}
	
	onPushRegistered(deviceToken) {
	    // TODO: Send the token to my server so it could send back push notifications...
		console.log("Device Token Received", deviceToken);
	}

	onPushRegistrationFailed(error) {
		// For example:
		//
		// error={
		//   domain: 'NSCocoaErroDomain',
		//   code: 3010,
		//   localizedDescription: 'remote notifications are not supported in the simulator'
		// }
		console.error(error);
	}
	
	componentWillUnmount() {
  		// prevent memory leaks!
  		NotificationsIOS.removeEventListener('remoteNotificationsRegistered', this.onPushRegistered.bind(this));
		NotificationsIOS.removeEventListener('remoteNotificationsRegistrationFailed', this.onPushRegistrationFailed.bind(this));
	}
}

```

When you have the device token, POST it to your server and register the device in your notifications provider (Amazon SNS, Azure, etc.).

You can check if the user granted permissions by calling `checkPermissions()`:

```javascript
NotificationsIOS.checkPermissions().then((currentPermissions) => {
    console.log('Badges enabled: ' + !!currentPermissions.badge);
    console.log('Sounds enabled: ' + !!currentPermissions.sound);
    console.log('Alerts enabled: ' + !!currentPermissions.alert);
});
```


