---
version: v0.31.0
category: API
title: 'Screen Ko'
source_url: 'https://github.com/atom/electron/blob/master/docs/api/screen-ko.md'
---

﻿# screen

`screen` 모듈은 화면 크기, 디스플레이, 커서 위치 등등의 다양한 정보를 가져옵니다.
이 모듈은 `app` 모듈의 `ready` 이벤트가 발생하기 전까지 사용할 수 없습니다.

`screen`은 [EventEmitter](http://nodejs.org/api/events.html#events_class_events_eventemitter)를 상속 받았습니다.

한가지 주의할 점은 랜더러 / DevTools에선 이 모듈의 이름인 `screen`은 이미 DOM 속성에 `window.screen`로 존재 하므로 `screen = require('screen')`를
사용할 수 없습니다. 밑의 예제와 같이 `atomScreen`등의 이름으로 변수 이름을 대체하여 사용해야 합니다.

다음 예제는 화면 전체를 채우는 윈도우 창을 생성합니다:

```javascript
var app = require('app');
var BrowserWindow = require('browser-window');

var mainWindow;

app.on('ready', function() {
  var atomScreen = require('screen');
  var size = atomScreen.getPrimaryDisplay().workAreaSize;
  mainWindow = new BrowserWindow({ width: size.width, height: size.height });
});
```

다음 예제는 확장 디스플레이에 윈도우를 생성합니다:

```javascript
var app = require('app');
var BrowserWindow = require('browser-window');

var mainWindow;

app.on('ready', function() {
  var atomScreen = require('screen');
  var displays = atomScreen.getAllDisplays();
  var externalDisplay = null;
  for (var i in displays) {
    if (displays[i].bounds.x > 0 || displays[i].bounds.y > 0) {
      externalDisplay = displays[i];
      break;
    }
  }

  if (externalDisplay) {
    mainWindow = new BrowserWindow({
      x: externalDisplay.bounds.x + 50,
      y: externalDisplay.bounds.y + 50,
    });
  }
});
```

## Event: display-added

* `event` Event
* `newDisplay` Object

새로운 디스플레이가 추가되면 발생하는 이벤트입니다.

## Event: display-removed

* `event` Event
* `oldDisplay` Object

기존의 디스플레이가 제거되면 발생하는 이벤트입니다.

## Event: display-metrics-changed

* `event` Event
* `display` Object
* `changedMetrics` Array

`display`의 하나 또는 다수의 매트릭스가 변경될 때 발생하는 이벤트입니다.
`changedMetrics`는 변경에 대한 정보를 담은 문자열의 배열입니다.
`bounds`, `workArea`, `scaleFactor`, `rotation`등이 변경될 수 있습니다.

## screen.getCursorScreenPoint()

현재 마우스 포인터의 절대 위치를 반환합니다.

## screen.getPrimaryDisplay()

기본 디스플레이를 반환합니다.

## screen.getAllDisplays()

사용 가능한 모든 디스플레이를 배열로 반환합니다.

## screen.getDisplayNearestPoint(point)

* `point` Object
  * `x` Integer
  * `y` Integer

지정한 좌표에 가까운 디스플레이를 반환합니다.

## screen.getDisplayMatching(rect)

* `rect` Object
  * `x` Integer
  * `y` Integer
  * `width` Integer
  * `height` Integer

지정한 범위에 가장 가깝게 교차한 디스플레이를 반환합니다.
