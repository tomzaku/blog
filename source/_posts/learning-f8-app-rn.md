---
title: Learning F8 App ReactNative by UML
thumbnail: /images/f8app_flow.png
tags: react native
---

Just for learning F8app(by facebook)


![Class Flow F8App](/images/f8app_flow.png)
## Describe
  F8 app is created by Facebook. It's a basic example for React-Native (use redux).
  You can check here: https://github.com/fbsamples/f8app/tree/master/js.
  This post required some knowledge about redux,react.
  This is a life circle in React. This is so important in React.

![Life Cycle React Native](https://cdn-images-1.medium.com/max/1600/0*VoYsN6eq7I_wjVV5.png)
  Each component in ReactNative will run above image.
  When state of a component change, the component will render again.

## Structure Directory
├── setup.js
├── F8App.js
├── F8Navigator.js
├── FacebookSDK.js
├── PushNotificationsController.js
├── actions
├── common
│      ├── BackButtonIcon.js
│      ├── Carousel.js
│      ├── F8Button.js
│      ├── F8Colors.js
│      ├── F8DrawerLayout.js
│      ├── F8Header.js
│      ├── F8PageControl.js
│      ├── F8SegmentedControl.js
│      ├── F8StyleSheet.js
│      └── img
│          ├── back.android.png
├── filter
│      ├── FilterScreen.js
│      ├── FriendsList.js
│      ├── Header.js
├── flow-lib.js
├── login
├── rating
├── reducers
│      ├── config.js
│      ├── createParseReducer.js
│      ├── filter.js
│      ├── friendsSchedules.js
│      ├── index.js
│      ├── maps.js
│      └── user.js
├── setup.js
├── store
│      ├── analytics.js
│      ├── array.js
│      ├── configureStore.js
│      ├── promise.js
│      └── track.js
└── tabs
       ├── F8TabsView.android.js
       ├── F8TabsView.ios.js
       ├── MenuItem.js
       ├── info
       ├── maps
       ├── notifications
       └── schedule

## Detail
  First, F8App will call setup.js(./js/setup.js)
### 1. Setup.js

  Call `configureStore` from store directory(./store/configureStore) to apply `redux`
  ```
  <Provider store={this.state.store}>
  store: configureStore(() => this.setState({isLoading: false})),
  ```
  While it waiting loading redux,it show the white screen
  ```
      if (this.state.isLoading) {
    return null;
  }
  ```
  If loading finished, it will call F8App(./js/F8App)
  ```
      <Provider store={this.state.store}>
        <F8App />
      </Provider>
  ```
### 2. F8App.js
##### componentDidMount
  1. Adding event checking App status (`foreground` in App ,`background` in another App or home Screen)
  ```
  AppState.addEventListener('change', this.handleAppStateChange);
  ```
  2. Load notification,map ... (download from the internet). You can check code in redux
  ```
  // TODO: Make this list smaller, we basically download the whole internet
  this.props.dispatch(loadNotifications());
  this.props.dispatch(loadMaps());
  this.props.dispatch(loadConfig());
  this.props.dispatch(loadSessions());
  this.props.dispatch(loadFriendsSchedules());
  this.props.dispatch(loadSurveys());
  ```

  3. Sync/Update code from server to user(Update code without download from AppStore/CH Play)
  ```
  CodePush.sync({installMode: CodePush.InstallMode.ON_NEXT_RESUME});
  ```
##### render
  4. Check isLogined (use `redux-persist` in redux for save the data in local)
  If it's not Login => Push Login Screen
  else => push Navigator
  ```
  if (!this.props.isLoggedIn) {
      return <LoginScreen />;
    }
    return (
      <View style={styles.container}>
        <StatusBar
          translucent={true}
          backgroundColor="rgba(0, 0, 0, 0.2)"
          barStyle="light-content"
         />
        <F8Navigator />
        <PushNotificationsController />
      </View>
    );
  ```
  Note: `StatusBar` => Work for Android.
  `PushNotificationsController` => Check and Push Notification is used `react-native-push-notification` library

### 3. F8Navigator.js
##### componentDidMount
  1. Listening Press Back Button on Android. Use `BackAndroid`
  ```
    componentDidMount: function() {
      BackAndroid.addEventListener('hardwareBackPress', this.handleBackButton);
    },
  ```
  2. use `Navigator` to change screen.
  ```
  <Navigator
      ref="navigator"
      style={styles.container}
      configureScene={(route) => {
        if (Platform.OS === 'android') {
          return Navigator.SceneConfigs.FloatFromBottomAndroid;
        }
        // TODO: Proper scene support
        if (route.shareSettings || route.friend) {
          return Navigator.SceneConfigs.FloatFromRight;
        } else {
          return Navigator.SceneConfigs.FloatFromBottom;
        }
      }}
      initialRoute={{}}
      renderScene={this.renderScene}
    />
  ```
    `renderScene` is like a router that switch scene.
    Default `F8TabsView.js`
  3. Remove event Listen Back Button
  ```
  componentWillUnmount: function() {
    BackAndroid.removeEventListener('hardwareBackPress', this.handleBackButton);
  },
  ```
  4. Note
  Context in React is like Global Variable. So you have consider when use it.
  It will take more memory and may be reduce performance.
  ```
  getChildContext() {
    return {
      addBackButtonListener: this.addBackButtonListener,
      removeBackButtonListener: this.removeBackButtonListener,
      };
    },
    ```
### 4. F8TabView.js (./js/tab/F8TabsView.android.js and F8TabView.ios.js)
Change Tab of DrawerLayout in Android or Tab of TabBar in IOS.
Explain why have F8TabsView.android.js and F8TabView.ios.js.
      1. When you run app on IOS RN(React Native) know call F8TabView.ios.js automatic. also when you run Android, it will call F8TabView.android.js
      2. F8TabView.android use Drawer Layout (`DrawerLayoutAndroid` package) in Android, F8TabView.ios use TabBar(`TabBarIOS` package) in IOS.
      So we should separate file for compatible with User Experience(UX).
F8TabView control tab by redux. So It can save the current tab even when you exit F8 App. (So interesting ,isn't it? :D)
Depend on tab selected, will call which Component(F8 NotificationsView, GerneralScheduleView, MyScheduleView, F8MapView)



......Continue......
