# simple-app-shell

Simple App Shell provides a simple and basic HTML, CSS and Javascript shell for [Progessive Web Apps (PWA)](https://developers.google.com/web/progressive-web-apps).
The main features are:

- Hash Navigation
- Serviceworker Caching
- Basic User Interface

## Hash Navigation
Simple App Shell uses a single page architecture. One single HTML page contains all content pages for your application. The different content pages are identified by div elements with a class and an id attribute (see code sample 1):

```
<div class="page" id="yourpageID">
```

You can show content pages by using internal hash links based on the page id.

E.g. ```<a href="#yourpageID">...``` will show your content page with the matching id and hide all other content pages. If you use a hash link without a matching page id the first page will be shown (page with id="appstart" in code sample 1).

With hash based navigation you can use back and forward buttons of your browser and the back button of your android device to navigate among the content pages although you only use one HTML page.

Important: You can set an individual page id but you may not change the class="page".

```
<body>
...
<div class="page" id="appstart">
	<div class="header">
	</div>
	<div class="content">
	</div>
</div>
<div class="page" id="yourpageID">
	<div class="header">
	</div>
	<div class="content">
	</div>
</div>
...
</body>
```
Code Sample 1: Single page architecture (index.htm)


## Serviceworker Caching
The serviceworker is responsible for caching your files. This means basic content of your web app can be available when your device is offline with no internet connection.

When loading the web app based on simple app shell a servicworker is registered using the file serviceworker.js (located in root directory). Code sample 2 shows the caching section in serviceworker.js. There are just two items you may edit:

```
var cacheName = 'simple_appshell_20_01_18_15_51';
```
Every time you change your web app and you want the serviceworker to update your files you have to change the chacheName!

```
var urlsToCache = [...];
```
A list with the files you want to cache. Add all files here you want to be available when offline (e.g. images, css, js).

Important: The serviceworker only works in a secure environment (https) or with localhost. The lifecycle of a serviceworker is rather complex. For more information see https://developers.google.com/web/fundamentals/primers/service-workers

For a working update process you may also have to switch off the browser cache for your pwa site (e.g. by using no-cache header statement in .htaccess, depends on your hosting environment).

```
//########################################
// serviceworker for Simple App Shell
// Version: 18.01.2020 15:51
//########################################

var cacheName = 'simple_appshell_20_01_18_15_51';
var urlsToCache = [
	'/',
	'/index.htm',
	'/apple-touch-icon.png',
	'/favicon.ico',
	'/icon_144.png',
	'/icon_192.png',
	'/icon_512.png',
	'/manifest.json'
];
...
```
Code Sample 2: Caching section in serviceworker.js


## Basic User Interface
Every content page contains a header and a content section (see code sample 1). The header section ```<div class="header">``` contains the page titles and the main navigation buttons. The content section ```<div class="content">``` may contain your content. The footer ```<p class="footer">Footer...``` is also included in the content section.

CSS and JS code is included in the index.htm header section. You may change the CCS and add JS code for your needs. You may also replace the icons files with your icons.

The basic template includes an info page that shows version and status info. Status messages and version info can be set in the top of the JS section. You may also use the info page for general, legal and license information.

The manifest.json holds basic information about your PWA. You may set at least the short-name and name for your web app. For more information see https://developers.google.com/web/fundamentals/web-app-manifest

## Samples
You can find samples based on Simple App Shell at: https://www.cjpj.de/webapps.htm

Samples in this repository are 
- https://github.com/cjpjwa/simple-tracer
- https://github.com/cjpjwa/schmerzlog 
