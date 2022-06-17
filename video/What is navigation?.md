
What is navigation?

- Navigation is a broad term that covers topics related to how you move between screens in your app.
- Navigation state
  - Web navigation is oriented around URLs.
  - Apps use URLs* for navigating into an app but not within the app.
- Navigation views
  - UI that users use to understand and manipulate the state

Navigation APIs for React Native
- Many libraries out there to solve this problem.
- Can be classified into two distinct approaches
  1. Implement mostly in Javascript with React
  2. Implement mostly in native, exposing an interface to Javascript for existing native navigation APIs.

Navigators, routes, screen components
- A navigator is a React component that implements a navigation pattern
- Each navigator has one or more routes
- Each route must have a name and a screen component
  - The name is usually unique across the app
  - The screen component is a React component that is rendered when the route is active
  - The screen component can also be another navigator

Switch navigator
- Display one screen at a time
- When a screen becomes inactive it is unmounted
- The only action a user can take is to switch between routes

Stack navigator
- Display one screen at a time
- The state of inactive screens is maintained and they remain mounted
- Platform-specific layout, animations, and gestures

Composing navigators
- Use a navigator as a screen component to compose navigators
- You can navigate() to any route in the app from any other route
 -- navigation actions aren't local to a single navigator.

Composing navigators
```
const MyStackNavigator = createStackNavigator({
  "Home": HomeScreen,
  "Profile": ProfileScreen
});

const MySwitchNavigator = createSwitchNavigator({
  "Login": LoginScreen,
  "Main": MyStackNavigator
});
```

Extending navigators
- You can wrap a navigator component with another in order to change the presentation or extend functionality
- You need to expose the router static on the component that wraps the navigator, and thread through the navigation prop.
  - If you don't do both of these, there will be problems.

Extending navigators
```
const PlainSwitchNavigator = createSwitchNavigator({
  Home: HomeScreen,
  Profile: ProfileScreen
});

class CustomSwitchNavigator extends React.Component {
  static router = PlainSwitchNavigator.router;

  render() {
    const { navigate } = this.props.navigation;
    return (
    <View style={{ flex: 1 }}>
      <PlainSwitchNavigator navigation={this.props.navigation} />
      <View style={styles.tabBar}>
        <Button onPress={() => navigate("Home")} title="Home" />
        <Button onPress={() => navigate("Home")} title="Profile" />
      </View>
    </View>);
  }
}

const AppNavigator = createSwitchNavigator({
    Login: LoginScreen,
    Main: CustomSwitchNavigator
});

```

Creating a navigator
- Navigator tie together two pieces: routers and navigation views.
- Routers are reducers that take an action and the current state for the navigator, then return the next state for the navigator
- Navigation views are React components that take the navigation state for the navigator as a prop and render the appropriate UI.


