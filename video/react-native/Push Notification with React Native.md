
[Push Notification with React Native](https://www.youtube.com/watch?v=XCk31D5vY0U&index=1&list=WL)

Why Push Notifications?
- Retention
- Engagement
- Get user's attention

Some numbers...

31.84% of all apps in Android
app store include push

But, 57.92% if installed apps include push

How does it work
1. identify the user
2. Trigger notification from server
3. Handle receiving notification

How to implement it with React Native

Easy way - Expo

How does it work 
- Save the user's Expo Push Token on your server
- Call Expo's Push API with the user's token
- Handle receiving and/or selecting the notification

Hard way - without Expo


Handling secure notifications
Your application server - Message ID -> Notification Server - Message ID -> Client App

Don't annoy your users

Make your notification useful
- Don't broadcast a notification
- Tailor a notification based on the user
- Also target based on geo and timezone so that it can be tailored accordingly

make the notification configuration so that user can only opt in on what they want

Very important: maintain quiet hours

With great power, comes great responsibility



