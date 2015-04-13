<a id="top"></a>
# Building iOS Apps with JavaScript and React Native

*Quickly build reusable, modular native iOS applications*

Written and developed by [Matt Piccolella](mailto:matthew@adicu.com) and [ADI][adi].

Credit to [Use React Native][use-react], [Ray Wenderlich][wenderlich], [Facebook Developers][facebook-dev].

## Getting Started: FAQs

### What is React Native?
React Native is Facebook's solution to building native iOS and Android applications using JavaScript. It represents the first real attempt to bring web technologies to native mobile development. In the past, solutions like [PhoneGap][phone-gap] have used web-based solutions, which can be slow and unresponsive. With React Native's open source framework for building applications, you can build beautiful mobile applications.

### Why should I use it?
React Native is built on Facebook's belief that you should "build once, run everywhere." This means that, once you write your application using React Native, you will have both an iOS application and an Android application, which represents incredible time saving. 

In addition, React Native doesn't require to rebuild your application each time you make a change, meaning you can "refresh" the page just as you do in web development and see your changes.

Finally, JavaScript is a much more familiar and universal language than Objective-C. Now, you can harness the #skills you have from web programming and put them to use in creating awesome mobile applications, which are much more easily debuggable and stylable.

### What will this tutorial teach me?
This tutorial will teach you the basics of React Native. We will go through the basic concepts, ranging from React components, to Flexbox and styling, to running your application in XCode. It will NOT teach you all of the methods or possibilities of React Native. If you are interested in learning more in-depth material than this tutorial can offer, [examples][examples] are available, as well as all the [documentation][docs].

## Using this Document

This document contains a series of several sections, each of which explains a certain sector of our sample iOS application. In each section, we will add some code to our application. All of the code is available both in this document and in the GitHub repo available [here][github-link].

## Table of Contents

-   [Preface: Setting up your Computer](#setup)
-   [Project Description: GithubFinder](#github-finder)
-   [1.0 "Hello World" in React Native](#react)
    - [1.1 Creating a Project](#creating-proj)
    - [1.2 Using XCode](#using-xcode)
    - [1.3 Using the Simulator](#simulator)
    - [1.4 Project Structure](#project-structure)
-   [Additional Resources](#additionalresources)


------------------------------
<a id="setup"></a>
## Preface: Setting up your Computer
To use React Native, there are a few requirements that you will need:

    1. OS X - as we will be using XCode, your computer must be running Mac OS X.
    2. XCode - this is the application that you normally program iOS applications in. For React Native, we will merely run the application using XCode.
    3. Homebrew - the recommended package installer for Mac. We will use this to install a few pieces of software we will need.

To begin the process, please install XCode [here][xcode]. To install Homebrew, please run the following command in your Terminal:

```bash
$ ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

Once you have XCode and Homebrew installed, please run the following commands from your terminal:

```bash
$ brew install node
$ brew install --HEAD watchman
$ npm install -g react-native-cli
```

You may be wondering why we are installing Node, a web technology, when we are working on iOS applications. Node is used by React Native to run our application, which enables the refreshing we will see in a moment.

Once you have installed these, your computer is all setup to program in React Native!

<a id="github-finder"></a>
## Project Description: GithubFinder
In this tutorial, we will program a sample application that will allow us to search for projects on GitHub. This will allow to search for applications on GitHub so we can decide whether an application we want to find exists, or whether an application we want to make has been made yet.

Each step of our application will move us toward our final product, which will be our GithubFinder application.

<a id="react"></a>
## 1.0 "Hello World" in React Native
In this section, we will create our first basic "Hello World" app in React Native. This will show us how to start a project, how to use XCode, how to use the simulator, and what files are involved in our project.

<a id="creating-proj"></a>
### 1.1 Creating a Project
To create our project, we will use the React Native command-line-interface we installed before. To create our application, open your Terminal, navigate to a folder in which you want to keep your project, and type the following command:

```bash
$ react-native init GithubFinder
```

If it worked, you should see something like the following output in your Terminal:

```
Next steps:

   Open /Users/Matt/Desktop/GithubFinder/GithubFinder.xcodeproj in Xcode
   Hit Run button
```

That means we have successfully created our first iOS application using React Native! If you look at the files in our new project folder, you should see something like this:

```
GithubFinder.xcodeproj iOS                    index.ios.js           node_modules           package.json
```

In a later section, we will explain what each one of these files does, and which of them will be important to us.

<a id="using-xcode"></a>
### 1.2 Using XCode
Now, let's open our application. So, run XCode, and select:

```
File > Open
```

and from within the directory that was just created, select GithubFinder.xcodeproj. Once you have done this, press the Play button in the top left corner of the application, or simply type `Cmd-R`, to run your application. Once this happens, a new Terminal window should open with output similar to this:

```
 ===============================================================
 |  Running packager on port 8081.       
 |  Keep this packager running while developing on any JS         
 |  projects. Feel free to close this tab and run your own      
 |  packager instance if you prefer.                              
 |                                                              
 |     https://github.com/facebook/react-native                 
 |                                                              
 ===============================================================

Looking for JS files in
   /Users/Matt/Desktop/GithubFinder 
```

Don't exit out of this window, as it will package up your JavaScript code into your iOS application. You can minimize both XCode and the Terminal window that was just created; you don't need them anymore!

However, what you will need is the Simulator, which we will take about now.

<a id="simulator"></a>
### 1.3 Using the Simulator
We will use the Simulator to simulate a real iOS device. We do this because an iOS developer's license is required to run applications on a real device. The simulator looks like this:

![Simulator](https://dl.dropboxusercontent.com/s/6utgiyw4hoh5d6e/simulator.png)

For us, the simulator is quite simple. To refresh, we simply type `Cmd-R` to reload our application. Once we start to make changes to our application, you will see how nice this becomes.

<a id="project-structure"></a>
### 1.4 Project Structure
Now that we have our simulator running, let's go back to the structure of the project we created. We saw before that the files contained inside of our project include:

```
GithubFinder.xcodeproj iOS                    index.ios.js           node_modules           package.json
```

Let's look at each file:

  - GithubFinder.xcodeproj - contains details necessary to open our application in XCode. This is what you open when you open XCode.
  - iOS - the file that contains all of the iOS code that is generated by React Native. Important: **IGNORE THIS**, we don't need to worry about it.
  - node_modules - contains the modules necessary for Node. This is also unimportant to us
  - package.json - provides some details about our application

These four files are not relevant to us in our creating our application. In fact, there is only one file we need to care about, which is `index.ios.js`. This makes it super easy for us from a development perspective; in a single file, we can define styles, transitions, and behaviors of our application.

The code of our file looks as follows:

```javascript
/**
 * Sample React Native App
 * https://github.com/facebook/react-native
 */
'use strict';

var React = require('react-native');
var {
  AppRegistry,
  StyleSheet,
  Text,
  View,
} = React;

var GithubFinder = React.createClass({
  render: function() {
    return (
      <View style={styles.container}>
        <Text style={styles.welcome}>
          Welcome to React Native!
        </Text>
        <Text style={styles.instructions}>
          To get started, edit index.ios.js
        </Text>
        <Text style={styles.instructions}>
          Press Cmd+R to reload,{'\n'}
          Cmd+Control+Z for dev menu
        </Text>
      </View>
    );
  }
});

var styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
    backgroundColor: '#F5FCFF',
  },
  welcome: {
    fontSize: 20,
    textAlign: 'center',
    margin: 10,
  },
  instructions: {
    textAlign: 'center',
    color: '#333333',
    marginBottom: 5,
  },
});

AppRegistry.registerComponent('GithubFinder', () => GithubFinder);
```

The code, while it may look familiar in some aspects, has lots of concepts, which will represent most of our work here. The next section will attempt to explain each of the concepts present in this file.


___________

## Additional Resources

While React Native is still a very new technology, there are still lots of quality resources available to learn more about it. Below are some good places to start:

[React for the Web][react-web]

[Introduction of React Native][react-keynote]

[React Native Tutorial][react-tutorial]

[Ray Wenderlich][wenderlich]

[ADI Resources][learn]

[use-react]: http://www.reactnative.com/
[react-keynote]: https://code.facebook.com/videos/786462671439502/react-js-conf-2015-keynote-introducing-react-native-/
[phone-gap]: http://phonegap.com/
[facebook-dev]: https://facebook.github.io/react-native/
[react-web]: https://facebook.github.io/react/
[react-tutorial]: http://facebook.github.io/react-native/docs/tutorial.html#content
[wenderlich]: http://www.raywenderlich.com/99473/introducing-react-native-building-apps-javascript
[learn]: https://adicu.com/resources
[adi]: https://adicu.com
[examples]: https://github.com/facebook/react-native/tree/master/Examples
[docs]: http://facebook.github.io/react-native/docs/getting-started.html
[github-link]: https://github.com/mjp2220/react-native-talk 
[xcode]: https://developer.apple.com/xcode/downloads/


