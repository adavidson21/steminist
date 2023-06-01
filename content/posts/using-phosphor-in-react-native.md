---
title: "Using Phosphor Icons in React Native"
date: 2023-05-30T23:48:24-04:00
draft: false
tags: ["Phosphor Icons", "React Native", "webdev", "mobile", "open source"]
---

Hello all! Today, we're going to dive into the world of icons. Specifically, we're going to talk about how to use Phosphor Icons in a React Native project. Phosphor Icons provide a wide range of beautifully crafted icons that can add a touch of elegance to your app. 

We are going to be using [this Phosphor React Native](https://github.com/duongdev/phosphor-react-native) package. To note, as of this article being written, it seems that an "official" react native package may be [in the works](https://github.com/phosphor-icons/react-native). But, as its not completed as of May 2023, we will be continuing with the community supported package. 

So, let's get started!

## Step 1: Installing Phosphor into Your Project

First things first, we need to install Phosphor into our project. You can do this by running the following command in your terminal in your existing project:

```
yarn add phosphor-react-native
```

You can find more information about the package [here](https://github.com/duongdev/phosphor-react-native).

## Step 2: Choosing the Right Spot for Your Icon

Next, navigate to the file where you want to use the icon to prepare to import the icon(s) you would like to use. Unlike some other frameworks, it is best to import icons individually to maintain a smaller build size for your mobile app. 

## Step 3: Picking Your Icon

Now comes the fun part - choosing your icon! Head over to the Phosphor Icons [website](https://phosphoricons.com/), select the icon you want to use, and choose "React". 

**Note** - As of May 2023, the package used here does not support any icons that were released as a part of Phosphor's 2.0 release.

## Step 4: Importing and Using Your Icon

Once you've chosen your icon, you'll need to import it into your file. Here's an example of how to do this:

```
import { House } from "phosphor-react-native"
```

After importing, you can reference the icon in your project wherever you want to include it. Here's an example:

```
<House size={32} />
```

And voila! You've successfully added a Phosphor icon to your project. Here's an example of a baseline file format for using Phosphor icons in your navigation bar for your React Native app:

```typescript
import { House, ImageSquare, FolderUser, DotsThree, FilePlus } from "phosphor-react-native"

/* ... */

return (
<Tab.Navigator
  screenOptions={() => ({
    headerShown: false,
    tabBarStyle: {
      height: 90,
      paddingHorizontal: 5,
      paddingTop: 0,
      backgroundColor: "white",
      position: "absolute",
      borderTopWidth: 0,
    },
  })}
>
  <Tab.Screen
    name="Home"
    component={Screens.HomeScreen}
    options={{
      tabBarIcon: () => <House size={32} />,
      title: "Home",
    }}
  />
  <Tab.Screen
    name="Chart"
    component={Screens.ChartScreen}
    options={{
      tabBarIcon: () => <FolderUser size={32} />,
      title: "Chart",
    }}
  />
  <Tab.Screen
    name="Add"
    component={Screens.AddScreen}
    options={{
      tabBarIcon: () => <FilePlus size={32} />,
      title: "Add New",
    }}
  />
  <Tab.Screen
    name="Images"
    component={Screens.ImagesScreen}
    options={{
      tabBarIcon: () => <ImageSquare size={32} />,
      title: "Imaging",
    }}
  />
  <Tab.Screen
    name="More"
    component={Screens.MoreScreen}
    options={{
      tabBarIcon: () => <DotsThree size={32} />,
      title: "More",
    }}
  />
</Tab.Navigator>
)

```

And that's it! You've successfully added Phosphor icons to your React Native project. Happy coding!