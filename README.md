# Mobile Web Specialist Certification Course
---
## _Three Stage Course Material Project - Restaurant Reviews_

## Stage 3

For stage 3, I have rewritten nearly everything from Stage 2 to create a single page web
application. I have also implemented HTTPS via Spdy and for the reviewers convenience,
the certificate is generated on the fly thanks to the 'pem' module. I also used Sass for the first time in a project and I'm now hooked. It was so much easier to manage the CSS.

So, to install, and run:

1. Clone this project from git.

```
    git clone https://github.com/steve-christensen/mws-restaurant-reviews.git
```

2. Install dependencies.
```
    npm install
```

3. Build the project
```
    npm build
```

4. Start the server (Option 1: HTTP2! very fast)
```
    npm start
```
  Open your browser to https://localhost:8002/
  You will probably get a security warning. Please opt to trust me and continue to the site.

5. Start the server (Option 2: python HTTP)
```
    npm start-python
```
Open your browser to http://localhost:8001/


### Requirements

#### Functionality

Criteria | Meets Specifications
---------|---------------------
User Interface | Users are able to mark a restaurant as a favorite, this toggle is visible in the application. A form is added to allow users to add their own reviews for a restaurant. Form submission works properly and adds a new review to the database.
Offline Use | The client application works offline. JSON responses are cached using the IndexedDB API. Any data previously accessed while connected is reachable while offline. User is able to add a review to a restaurant while offline and the review is sent to the server when connectivity is re-established.


#### Responsive Design and Accessibility

Criteria | Meets Specifications
---------|---------------------
Responsive Design | The application maintains a responsive design on mobile, tablet and desktop viewports. All new features are responsive, including the form to add a review and the control for marking a restaurant as a favorite.
Accessibility | The application retains accessibility features from the previous projects. Images have alternate text, the application uses appropriate focus management for navigation, and semantic elements and ARIA attributes are used correctly. Roles are correctly defined for all elements of the review form.


#### Performance

Criteria | Meets Specifications
---------|---------------------
Site Performance | Lighthouse targets for each category exceed: <br><br> Progressive Web App: >90 <br> Performance: >90 <br> Accessibility: >90


### Extras

In addition to the course requirements, I wanted to learn a few other things. I actually implemented these self-imposed requirements first.

Criteria | Motivation & Implementation
---------|---------------------
Single-Page App | Though we couldn't use a framework, from the beginning, I thought this app might be nice as a single page app. So, I created my own router and view modules,  modified index.html to use them, and eliminated restaurant.html.
Sass | I've wanted to learn Sass for a long time. We had a brief introduction to Sass in the course, but the only way to learn it and gain experience is to use it.
HTTP2 | In order to handle deep linking or direct entry of detail page URLs in the address bar, I needed my own server to route those links to index.html for routing, so I implemented it using HTTP2 which also required setting up SSL.
Heroku (maybe) | After deploying a simple app to Heroku in one of the lessons, it might be nice to deploy this app to Heroku when finished.

___

## Stage 2

### API server
The stage 2 code expects that the API server (https://github.com/udacity/mws-restaurant-stage-2) is running on local host port 1337. You'll need for fork and clone the project by executing the following sequence of commands:

  ```
  git clone https://github.com/udacity/mws-restaurant-stage-2.git
  ```

  ```
  npm install
  ```
After it is installed, you can start the API server with the following command:

  ```
  node server
  ```
### Installing Restaurant-Review Project

Clone this project:

  ```
  git clone https://github.com/steve-christensen/mws-restaurant-reviews.git
  ```

Install dependencies:

  ```
  npm install
  ```

### Building and serving the app

#### Python SimpleHTTPServer

To build and serve with Python SimpleHTTPServer, enter the following command:

  ```
  nmp start
  ```

By default, the application will be served at http://localhost:8000/

#### BrowserSync (development only)

The default gulp task will build everything and then launch the app with BrowserSync.
This negatively impacts performance, so it is only beneficial during development
and not when evaluating app performance. To start with browser-sync, execute the
default gulp task:

  ```
  gulp
  ```

This will serve the application at http://localhost:3000/

#### BYO Server

If you need to serve the application in another way, you'll need to build the app
first and then serve from the build directory (./build where '.' is the project
root). To build the directory, execute the 'buildAll' Gulp task:

  ```
  gulp buildAll
  ```

### Stage 2 Changes

  - Changed the directory structure to move code to 'src' directory and then build the code in the 'build' directory

  - Build the app with GulpJS
    - Added GulpJS to do the following:
      - Copy HTML and manifest files
      - Minify CSS
      - Build JS with browserify, babel, and uglify.
      - Replace the grunt task for responsive images with a gulp-responsive (which in turn uses the sharp node module) to build various sized images
      - Set watches for HTML, CSS, and JavaScript changes
      - Launch the browser with BrowserSync

  - dbhelper.js
    - Updated dbhelper.js to an ES6 module and replaced the callback functions to use promises instead. Also changed the DBHelper class to have attributes and make the fetch methods non-static. The new version will only call out to the API (or service worker) when the constructor loads. After that, it will serve the restaurant data from the class attributes.
    - Made some minor changes to service-worker.js.
    - Updated main.js and restaurant_info.js to use the new DBHelper class.

- Progressive Web App Changes
  - Added a manifest.json file
  - Added meta tag for theme-color in the HTML files
  - Added icon images
  - Added icon and manifest links in the HTML files

### Stage 1 Changes

 - Home page
    - Update to use flex boxes to allow the restaurant list to expand to multiple columns when space is available.

 - HTML
    - Placed 'City map' paragraph inside of the map container so that it would be read by screen readers, but not visible.
  - CSS
    - Made many minor adjustments to improve responsiveness.
    - Added break points to allow different formatting on detail page based upon screen width.
    - Added ability to include 1-5 unicode stars in place of the rating.

 - 2018-06-15
    - HTML
        - Added labels for filter controls
    - CSS
        - Adjusted background and foreground colors to allow appropriate contrast levels for accessibility
        - position filter control labels off offscreen
        - adjust height on filter control bar to enclose the controls and the 'filter output' heading.
        - replace #footer and #main with footer and main.
    - JavaScript
        - Added code to include alt attributes on images. Look for a property called 'image_desc'. If that property does not exist, use the restaurant name.

## Project Overview: Stage 1

For the **Restaurant Reviews** projects, you will incrementally convert a static webpage to a mobile-ready web application. In **Stage One**, you will take a static design that lacks accessibility and convert the design to be responsive on different sized displays and accessible for screen reader use. You will also add a service worker to begin the process of creating a seamless offline experience for your users.

### Specification

You have been provided the code for a restaurant reviews website. The code has a lot of issues. It’s barely usable on a desktop browser, much less a mobile device. It also doesn’t include any standard accessibility features, and it doesn’t work offline at all. Your job is to update the code to resolve these issues while still maintaining the included functionality.

### What do I do from here?

1. In this folder, start up a simple HTTP server to serve up the site files on your local computer. Python has some simple tools to do this, and you don't even need to know Python. For most people, it's already installed on your computer.

In a terminal, check the version of Python you have: `python -V`. If you have Python 2.x, spin up the server with `python -m SimpleHTTPServer 8000` (or some other port, if port 8000 is already in use.) For Python 3.x, you can use `python3 -m http.server 8000`. If you don't have Python installed, navigate to Python's [website](https://www.python.org/) to download and install the software.

2. With your server running, visit the site: `http://localhost:8000`, and look around for a bit to see what the current experience looks like.
3. Explore the provided code, and start making a plan to implement the required features in three areas: responsive design, accessibility and offline use.
4. Write code to implement the updates to get this site on its way to being a mobile-ready website.

## Leaflet.js and Mapbox:

This repository uses [leafletjs](https://leafletjs.com/) with [Mapbox](https://www.mapbox.com/). You need to replace `<your MAPBOX API KEY HERE>` with a token from [Mapbox](https://www.mapbox.com/). Mapbox is free to use, and does not require any payment information.

### Note about ES6

Most of the code in this project has been written to the ES6 JavaScript specification for compatibility with modern web browsers and future proofing JavaScript code. As much as possible, try to maintain use of ES6 in any additional JavaScript you write.
