# HackMe1
Test your JavaScript knowledge and analytical skills.

![screenshot](https://github.com/lucianoaibar/HackMe1/blob/main/screenshot.png?raw=true)

## Goal
Analyze the algorithm to find the correct box-clicking order.\
Explain how it works and apply a new box-clicking order pattern.\
The source code is fully working. There is no need to fix it.\
Do not use brute force.

## Full source code
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Hack Me 1</title>
  <style>
    body { background-color: #000; color: #0F0; text-align: center; }
    div { display: inline-block; width: 50px; height: 50px; background-color: #888; margin-right: 5px;}
    .click { background-color: #FFF; }
  </style>
  <script>
    var $ = 1, _ = 'click';
  </script>
</head>
<body>
  <h2>Hack Me 1</h2>
  <h4>Click the squares in the correct order to unlock this challenge</h4>
  <h4>There is no need to modify this code. It is working properly.</h4>
  <h5>by Luciano Aibar lucianoaibar@gmail.com</h5>

  <script>
    (function(code) {
      'use strict';

      const DICTIONARY	= [
        0x01, 0x00, 0x05, 0x01, 0x00, 0x07, 0x01, 0x06, 0x08, 0x02, 0x00, 0x05, 0x01, 0x02, 0x01, 0x08,
        0x03, 0x02, 0x03, 0x07, 0x01, 0x09, 0x02, 0x09, 0x06, 0x01, 0x09, 0x09, 0x01, 0x06, 0x02, 0x01,
        0x00, 0x04, 0x06, 0x07, 0x07, 0x08, 0x01, 0x09, 0x07, 0x02, 0x00, 0x09 ];

      let x       = code;
      let y       = x;
      let max     = code * 10;
      let boxes   = [];
      let events  = [];
      let name;
      let result;

      {
        let code = 5;
        name = 'h' + code;
      }

      for(; y < max * max; y <<= code + code) {
        for(; x < max; x <<= code) {
          boxes.push( result = '' + y + x );
          document.body.innerHTML += '<div id="' + result + '"></div>'
        }
        document.body.innerHTML += '<br>';
        x = code;
      }

      document.body.addEventListener(_, function(e) {
        if(e.target.tagName == 'DIV') {
          e.target.classList.add(_);
          if(events.push(boxes.findIndex(x => x == e.target.id)) & code << 4) {

            x = code - 1;
            y = document.getElementsByTagName(name)[0].innerText;
            result = '';
            events.forEach(n => result += (boxes[n] & 0xFF) ^ y.charCodeAt(x++));

            if(result.length == DICTIONARY.length) {
              max = '';
              for(x = code - 1; x<DICTIONARY.length; x++) {
                max += String.fromCharCode(result.charCodeAt(x) ^ DICTIONARY[x]);
              }
              if(max == code) {
                alert('VICTORY !');
              }
            }
          }
        }
      });
    })($);
  </script>
</body>
</html>
```
