# SpreadsheetConverter nodejs mongodb form controller

[![N|Solid](http://www.spreadsheetconverter.com/wp-content/uploads/2013/08/logo.png)](http://www.spreadsheetconverter.com)

mongomodulecontroller is a helper module for SpreadsheetConverter nodejs calculator app to connect with your [mongodb](https://www.mongodb.com/). With a small code manpulation at your node calculator app you will easy connect your form to your mongodb.

### Installation

mongomodulecontroller requires [mongoose.js](http://mongoosejs.com/) to run.

Install the dependencies, mongoose.js in your app.

```sh
$ cd <your application folder>
$ npm install mongoose --save
```
### Usage

Include mongomodulecontroller.js in your node application folder.
Now you need to edit app.js to handle the form save post request from browser. Open app.js in your editor  and paste this snipplet code 
```sh
var _db = require('./mongomodalcontroller.js');
app.post('/postform',function(req,res,next){
    var _form = req.body;
    _db.saveform(_form,function (err,msg) {
        if(!err){
            res.status('422').send(msg);
        }
    });
});
```
just above the 
```sh
//---------start server-------
http.createServer(app).listen(config.port||3000);
```
after that app.js may look like this 
```sh
'use strict'

var express = require('express'),
    bodyParser = require('body-parser'),
    http = require('http'),
    path = require('path'),
    fs = require('fs');

...

app.post('/calc', function (req, res) { //calculator REST api
    var co = req.body;
    res.send(calc.calculate(co));
});

var _db = require('./mongomodalcontroller.js');
app.post('/postform',function(req,res,next){
    var _form = req.body;
    _db.saveform(_form,function (err,msg) {
        if(!err){
            res.status('422').send(msg);
        }
    });
});
//---------start server-------
http.createServer(app).listen(config.port||3000);
```

That's it, you are done with server part.
Now come to the final part to edit, yes you are right, Lets give the client side page a server address to post the form.
Go to views folder and open index.ejs in editor , now at html form tag change the default url : https://www.spreadsheetserver.com/server1/g/submit/submit.aspx to your node server. for testing at your local computer, edit as http://localhost:3000/postform
index.ejs may look similar to this 
```sh
<!DOCTYPE HTML>
<!-- saved from url=(0013)about:internet -->
<html>
...

        <form id='formc' name='formc' method='post' action='http://localhost:3000/postform' target='_top'>
		    <input type='hidden' id='xl_spreadsheet' name='xl_spreadsheet' value='testnodedb' />
            <input type='hidden' id='xl_client' name='xl_client' value='x8.4.6830.0' />
            ...
</html>            
```

You are done now, you have configure the SpreadsheetConverter nodejs calculator app to your mongodb database to persist your form.

start your node app. you are good to go!

