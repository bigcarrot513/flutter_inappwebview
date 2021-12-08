# Flutter InAppWebView Plugin v5.3.2 [![Share on Twitter](https://img.shields.io/twitter/url/http/shields.io.svg?style=social)](https://twitter.com/intent/tweet?text=Flutter%20InAppBrowser%20plugin!&url=https://github.com/pichillilorenzo/flutter_inappwebview&hashtags=flutter,flutterio,dart,dartlang,webview) [![Share on Facebook](https://img.shields.io/badge/share-facebook-blue.svg?longCache=true&style=flat&colorB=%234267b2)](https://www.facebook.com/sharer/sharer.php?u=https%3A//github.com/pichillilorenzo/flutter_inappwebview)

[![Pub](https://img.shields.io/pub/v/flutter_inappwebview.svg)](https://pub.dartlang.org/packages/flutter_inappwebview)
[![pub points](https://badges.bar/flutter_inappwebview/pub%20points)](https://pub.dev/packages/flutter_inappwebview/score)
[![popularity](https://badges.bar/flutter_inappwebview/popularity)](https://pub.dev/packages/flutter_inappwebview/score)
[![likes](https://badges.bar/flutter_inappwebview/likes)](https://pub.dev/packages/flutter_inappwebview/score)
[![Awesome Flutter](https://img.shields.io/badge/Awesome-Flutter-blue.svg?longCache=true&style=flat-square)](https://stackoverflow.com/questions/tagged/flutter-inappwebview)
[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](/LICENSE)

[![Donate to this project](https://img.shields.io/badge/support-donate-yellow.svg)](https://inappwebview.dev/donate/)
[![GitHub contributors](https://img.shields.io/github/contributors/pichillilorenzo/flutter_inappwebview)](https://github.com/pichillilorenzo/flutter_inappwebview/graphs/contributors)
[![GitHub forks](https://img.shields.io/github/forks/pichillilorenzo/flutter_inappwebview?style=social)](https://github.com/pichillilorenzo/flutter_inappwebview)
[![GitHub stars](https://img.shields.io/github/stars/pichillilorenzo/flutter_inappwebview?style=social)](https://github.com/pichillilorenzo/flutter_inappwebview)


![InAppWebView-logo](https://user-images.githubusercontent.com/5956938/110180687-8751f480-7e0a-11eb-89cc-d62f85c148cb.png)

A Flutter plugin that allows you to add an inline webview, to use an headless webview, and to open an in-app browser window.

## Articles/Resources

- [Official documentation: inappwebview.dev/docs](https://inappwebview.dev/docs/)
- Read the online [API Reference](https://pub.dartlang.org/documentation/flutter_inappwebview/latest/) to get the **full API documentation**.
- [Official blog: inappwebview.dev/blog](https://inappwebview.dev/blog/)
- Find open source projects on the [Official Showcase page: inappwebview.dev/showcase](https://inappwebview.dev/showcase/)
- Check the [example/integration_test/webview_flutter_test.dart](https://github.com/pichillilorenzo/flutter_inappwebview/blob/master/example/integration_test/webview_flutter_test.dart) file for other code examples
- [Flutter Browser App](https://github.com/pichillilorenzo/flutter_browser_app): A Full-Featured Mobile Browser App (such as the Google Chrome mobile browser) created using Flutter and the features offered by the flutter_inappwebview plugin

## Showcase - Who use it

Check the [Showcase](https://inappwebview.dev/showcase/) page to see an open list of Apps built with **Flutter** and **Flutter InAppWebView**.

#### Are you using the **Flutter InAppWebView** plugin and would you like to add your App there?

Send a submission request to the [Submit App](https://inappwebview.dev/submit-app/) page!

## Requirements

- Dart sdk: ">=2.12.0-0 <3.0.0"
- Flutter: ">=1.22.2"
- Android: `minSdkVersion 17` and add support for `androidx` (see [AndroidX Migration](https://flutter.dev/docs/development/androidx-migration) to migrate an existing app)
- iOS: `--ios-language swift`, Xcode version `>= 12`

## Installation

Add `flutter_inappwebview` as a [dependency in your pubspec.yaml file](https://flutter.io/using-packages/).

## Main Classes Overview

* [InAppWebView](https://inappwebview.dev/docs/in-app-webview/basic-usage/): Flutter Widget for adding an inline native WebView integrated into the flutter widget tree.
* [ContextMenu](https://inappwebview.dev/docs/context-menu/basic-usage/): This class represents the WebView context menu.
* [HeadlessInAppWebView](https://inappwebview.dev/docs/headless-in-app-webview/basic-usage/): Class that represents a WebView in headless mode. It can be used to run a WebView in background without attaching an InAppWebView to the widget tree.
* [InAppBrowser](https://inappwebview.dev/docs/in-app-browser/basic-usage/): In-App Browser using native WebView.
* [ChromeSafariBrowser](https://inappwebview.dev/docs/chrome-safari-browser/basic-usage/): In-App Browser using Chrome Custom Tabs on Android / SFSafariViewController on iOS.
* [InAppLocalhostServer](https://inappwebview.dev/docs/in-app-localhost-server/basic-usage/): This class allows you to create a simple server on http://localhost:[port]/. The default port value is 8080.
* [CookieManager](https://inappwebview.dev/docs/cookie-manager/basic-usage/): This class implements a singleton object (shared instance) which manages the cookies used by WebView instances.
* [HttpAuthCredentialDatabase](https://inappwebview.dev/docs/http-auth-credential-database/basic-usage/): This class implements a singleton object (shared instance) that manages the shared HTTP auth credentials cache.
* [WebStorageManager](https://inappwebview.dev/docs/web-storage-manager/basic-usage/): This class implements a singleton object (shared instance) which manages the web storage used by WebView instances.

## Support

Did you find this plugin useful? Please consider to [make a donation](https://inappwebview.dev/donate/) to help improve it!

## Edit guide for persistent http header

To add persistent http header, you should use shouldOverrideUrlLoading() method that flutter_inappwebview package provide.
they returns navigationAction as second parameter that contains request that are going to be proceeded.
In this case, it contains method, header, url and all other options but it doesn't included body of request.
This is what original package did in swift code.
Thus, you need to change it so that it returns body of request.
To do this, you need to change one file
`./ios/Classes/Types/URLRequest.swift`
add this line `"body": httpBody,` after line65
then it will looks like this.
```
    public func toMap () -> [String:Any?] {
        var iosAllowsConstrainedNetworkAccess: Bool? = nil
        var iosAllowsExpensiveNetworkAccess: Bool? = nil
        if #available(iOS 13.0, *) {
            iosAllowsConstrainedNetworkAccess = allowsConstrainedNetworkAccess
            iosAllowsExpensiveNetworkAccess = allowsExpensiveNetworkAccess
        }
        return [
            "url": url?.absoluteString,
            "method": httpMethod,
            "headers": allHTTPHeaderFields,
            "body": httpBody,
            "iosAllowsCellularAccess": allowsCellularAccess,
            "iosAllowsConstrainedNetworkAccess": iosAllowsConstrainedNetworkAccess,
            "iosAllowsExpensiveNetworkAccess": iosAllowsExpensiveNetworkAccess,
            "iosCachePolicy": cachePolicy.rawValue,
            "iosHttpShouldHandleCookies": httpShouldHandleCookies,
            "iosHttpShouldUsePipelining": httpShouldUsePipelining,
            "iosNetworkServiceType": networkServiceType.rawValue,
            "iosTimeoutInterval": timeoutInterval,
            "iosMainDocumentURL": mainDocumentURL?.absoluteString
        ]
    }
```
Then you can get body of request with `navigationAction.request.body`
And you can make same request with same params and can add custom headers to the request.
thats all.

### use this package in your flutter project
in pubspec.yaml file, add this under dependencies
``` 
flutter_inappwebview:
    git:
      url: https://github.com/galaxydeve/flutter_inappwebview.git
      ref: master 
```