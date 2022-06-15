
[Things You Didn't know You Can Do With React Native](https://www.youtube.com/watch?v=1InokWxYGnE&t=0s&list=WL&index=11)
- #### Non Standard Animations
- #### Physical Things
- #### Bridging taken to extreme

### Non Standard Animations
Why is Animation important?

Magic is both in the details and in the performance

Our regular solutions
- Animated
- LayoutAnimation
- react-native-animatable

What if we want to get more complex results?

react-native-lottie
- Renders native animations based on JSON exported from 
After Effects with BodyMovin plugin

What if we want to work with images content?
gl-react-native-v2
- gl-react wrapper for react-native. Write shaders in OpenGL GLSL language.

### Physical things
Merging digital and physical worlds
By letting device to be aware of physical context 
we change the way we interact with a user and ultimately the way we develop our apps

Geolocation is not enough.
Beacons for rescue.
- Tiny BLE transmitter, that transmits UUID and proximity over GAP protocol.

What we can do with React Native and Beacons?
- Indoor Navigation
- Proximity Marketing
- AutoMatic Check-in
- Contactless payment

By using physical context we try to predict user intent.

General guidelines for physical context aware apps
- Enable location services in our app.
- Start scanning for beacons
- Check closest beacons against server
- Execute custom logic based on closeset beacon.

react-native-beacon-manager

And what about smart homes?

react-native-ble-plx

### Bridging taken to extreme
- Don't be scared to bridge native modules.
That's the main recipe to create cool stuff.
- You were awesome!
