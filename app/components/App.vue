<template>
  <Page>
    <ActionBar title="Welcome to NativeScript-Vue!" android:flat="true" />
    <TabView
      android:tabBackgroundColor="#53ba82"
      android:tabTextColor="#c4ffdf"
      android:selectedTabTextColor="#ffffff"
      androidSelectedTabHighlightColor="#ffffff"
    >
      <TabViewItem title="Tab 1">
        <GridLayout columns="*" rows="*">
          <Label class="message" :text="msg" col="0" row="0" />
        </GridLayout>
      </TabViewItem>
      <TabViewItem title="Tab 2">
        <GridLayout columns="*" rows="*">
          <Label class="message" text="Tab 2 Content" col="0" row="0" />
        </GridLayout>
      </TabViewItem>
      <TabViewItem title="Tab 3">
        <GridLayout columns="*" rows="*">
          <Label class="message" text="Tab 3 Content" col="0" row="0" />
        </GridLayout>
      </TabViewItem>
    </TabView>
  </Page>
</template>

<script >
import { messaging, Message } from "nativescript-plugin-firebase/messaging";
export default {
  data() {
    return {
      msg: "Hello World!"
    };
  },
  mounted() {
    messaging
      .registerForPushNotifications({
        onPushTokenReceivedCallback: token => {
          console.log("Firebase plugin received a push token: " + token);
        },

        onMessageReceivedCallback: message => {
          console.log("Push message received: " + message.title);
        },

        // Whether you want this plugin to automatically display the notifications or just notify the callback. Currently used on iOS only. Default true.
        showNotifications: true,

        // Whether you want this plugin to always handle the notifications when the app is in foreground. Currently used on iOS only. Default false.
        showNotificationsWhenInForeground: true
      })
      .then(() => console.log("Registered for push"));
  }
};
</script>

<style scoped>
ActionBar {
  background-color: #53ba82;
  color: #ffffff;
}

.message {
  vertical-align: center;
  text-align: center;
  font-size: 20;
  color: #333333;
}
</style>
