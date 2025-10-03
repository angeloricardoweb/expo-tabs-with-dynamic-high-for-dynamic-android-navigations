# Tab Navigation with Gesture

# Font
https://github.com/JairajJangle/react-native-navigation-mode

# Install
`npx expo install react-native-navigation-mode`

## app.json
```js
    "plugins": [
      "react-native-navigation-mode",
    ],
```

## Code

```js

import MaterialIcons from '@expo/vector-icons/MaterialIcons';
import { Tabs } from 'expo-router';
import React from 'react';

import { HapticTab } from '@/components/haptic-tab';
import ProfileTabIcon from '@/components/ProfileTabIcon';
import { IconSymbol } from '@/components/ui/icon-symbol';
import { Fonts } from '@/constants/fonts';
import { Colors } from '@/constants/theme';
import { Platform } from 'react-native';
import { useNavigationMode } from 'react-native-navigation-mode';

export default function TabLayout() {
  const { navigationMode } = useNavigationMode();

  const isAndroidAndGestureNavigation = Platform.OS === 'android' && navigationMode?.isGestureNavigation;
  const isIos = Platform.OS === 'ios';

  const tabBarHeight = isIos ? 8 : !isAndroidAndGestureNavigation ? Number(navigationMode?.navigationBarHeight) + 80 : 8;

  return (
    <Tabs
      screenOptions={{
        tabBarActiveTintColor: Colors.secondary,
        headerShown: false,
        tabBarButton: HapticTab,
        tabBarStyle: {
          height: tabBarHeight, // Tab bar height
          paddingTop: 8,
          backgroundColor: Colors.tint,
          paddingBottom: Platform.OS === 'ios' ? 8 : 40,
        },
        tabBarLabelStyle: {
          fontSize: 12,
          marginTop: 2,
          fontFamily: Fonts.bold,
        },
        tabBarIconStyle: {
          marginTop: 2,
        },
      }}>
      <Tabs.Screen
        name="index"
        options={{
          title: 'Home',
          tabBarIcon: ({ color }) => <IconSymbol size={28} name="house.fill" color={color} />,
          headerShown: false,
        }}
      />
      <Tabs.Screen
        name="profile"
        options={{
          title: 'Minha Conta',
          tabBarIcon: ({ color }) => <ProfileTabIcon size={28} color={color} />,
          headerShown: false,
        }}
      />
      <Tabs.Screen
        name="menu"
        options={{
          title: 'Menu',
          tabBarIcon: ({ color }) => <MaterialIcons color={color} size={28} name="menu" />,
          headerShown: false,
        }}
      />
    </Tabs>
  );
}

```