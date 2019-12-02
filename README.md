# react-native-autoheight-webview

An auto height webview for React Native, even auto width for inline html.

[![NPM Version](http://img.shields.io/npm/v/react-native-autoheight-webview.svg?style=flat-square)](https://www.npmjs.com/package/react-native-autoheight-webview)
[![NPM Downloads](https://img.shields.io/npm/dt/react-native-autoheight-webview.svg?style=flat-square)](https://www.npmjs.com/package/react-native-autoheight-webview)

## versioning

`npm install react-native-autoheight-webview --save` (rn >= 0.59, be capable of Hooks)

`npm install react-native-autoheight-webview@1.0.1 --save` (0.57 <= rn < 0.59)

Read [README_old](./README_old.md) for earlier version guide.

## usage

```javascript
import AutoHeightWebView from 'react-native-autoheight-webview'

import { Dimensions } from 'react-native'

<AutoHeightWebView
    // default by screen width,
    // if there are some text selection issues on iOS, the width should be reduced more than 15 and the marginTop should be added more than 35
    style={{ width: Dimensions.get('window').width - 15, marginTop: 35 }}
    customScript={`document.body.style.background = 'lightyellow';`}
    // add custom CSS to the page's <head>
    customStyle={`
      * {
        font-family: 'Times New Roman';
      }
      p {
        font-size: 16px;
      }
    `}
    // either height or width updated will trigger onSizeUpdated
    onSizeUpdated={({size => console.log(size.height)})},
    /*
    using local or remote files
    to add local files:
    add files to android/app/src/main/assets/ (depends on baseUrl) on android
    add files to web/ (depends on baseUrl) on iOS
    */
    files={[{
        href: 'cssfileaddress',
        type: 'text/css',
        rel: 'stylesheet'
    }]}
    // baseUrl now contained by source
    // 'web/' by default on iOS
    // 'file:///android_asset/web/' by default on Android
    // or uri
    source={{ html: `<p style="font-weight: 400;font-style: normal;font-size: 21px;line-height: 1.58;letter-spacing: -.003em;">Tags are great for describing the essence of your story in a single word or phrase, but stories are rarely about a single thing. <span style="background-color: transparent !important;background-image: linear-gradient(to bottom, rgba(146, 249, 190, 1), rgba(146, 249, 190, 1));">If I pen a story about moving across the country to start a new job in a car with my husband, two cats, a dog, and a tarantula, I wouldn’t only tag the piece with “moving”. I’d also use the tags “pets”, “marriage”, “career change”, and “travel tips”.</span></p>` }}
    // false by default on iOS & Android (different from react-native-webview which true by default on Android),
    // when scalesPageToFit was assigned to true, it will apply page scale to size directly instead of using viewport meta script 
    scalesPageToFit={true}
    // only works on iOS when scalesPageToFit was false,
    // in other conditions, you can use your own custom scripts to create viewport meta to disable zooming
    zoomable={false}
    /*
    other react-native-webview props
    */
  />
```

## showcase

![react-native-autoheight-webview iOS](https://media.giphy.com/media/tocJYDUGCgwac0kkyB/giphy.gif)&nbsp;
![react-native-autoheight-webview Android](https://media.giphy.com/media/9JyX1wZshYIxuPklHK/giphy.gif)

## demo

You may have to use yarn to install the dependencies of the demo and remove "demo/node_modules/react-native-autoheight-webview/demo" manually, cause of installing a local package with npm will create symlink, but there is no supporting of React Native to symlink (https://github.com/facebook/watchman/issues/105) and "yarn install" ignores "files" from local dependencies (https://github.com/yarnpkg/yarn/issues/2822).
For android, you may have to copy the "Users\UserName\.android\debug.keystore" to "demo/android/app/".
