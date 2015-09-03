angular-simple-logger (nemLogging.nemSimpleLogger)
==============
[![Dependencies](https://david-dm.org/nmccready/angular-simple-logger.png)](https://david-dm.org/nmccready/angular-simple-logger)&nbsp;
[![Dependencies](https://david-dm.org/nmccready/angular-simple-logger.png)](https://david-dm.org/nmccready/angular-simple-logger)&nbsp;
[![Build Status](https://travis-ci.org/nmccready/angular-simple-logger.png?branch=master)](https://travis-ci.org/nmccready/angular-simple-logger)


### Purpose:
To have simplified log levels where a supporting angular module's log levels are independent of the application.


### Basic use:

```js
angular.module('someApp', ['nemLogging'])
//note this can be any type of injectable angular dependency (factory, service.. etc)
.controller("someController", function ($scope, nemSimpleLogger) {
  nemSimpleLogger.doLog = true; //default is true
  nemSimpleLogger.currentLevel = nemSimpleLogger.LEVELS.debug;//defaults to error only
});  
```

### Create a Custom Independent Loggers
*(maybe 3 for one lib)*

```js
angular.module('someApp', ['nemLogging'])
//note this can be any type of injectable angular dependency (factory, service.. etc)
.service("apiLogger", function ($scope, nemSimpleLogger) {
  var logger = nemSimpleLogger.spawn();
  logger.currentLevel = logger.LEVELS.warn;
  return logger;
})
.service("businessLogicLogger", function ($scope, nemSimpleLogger) {
  var logger = nemSimpleLogger.spawn();
  logger.currentLevel = logger.LEVELS.error;
  return logger;
})
.service("terseLogger", function ($scope, nemSimpleLogger) {
  var logger = nemSimpleLogger.spawn();
  logger.currentLevel = logger.LEVELS.info;
  return logger;
});  
```

### API
Underneath it all it is still calling `$log` so calling the logger for logging itself is the same.

- LEVELS: available are `log, info, debug, warn, error`

- doLog (boolean) - deaults to true. If set to false all logging for that logger instance is disabled.

- currentLevel (number) - defaults to `error: 5` corresponds to the current log level provided by `LEVELS`.
