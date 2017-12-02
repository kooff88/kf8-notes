var express = require('express');
var path = require('path');
const proxy = require('http-proxy-middleware');

var app = express();
app.use(express.static(path.join(__dirname,'../../dist')));

const apiProxy = proxy('/api',{target: 'http://192.168.188.114:3111',changeOrigin:true});
const imgProxy = proxy('/img',{target: 'http://192.168.188.114:3114',changeOrigin:true});
app.use('/api/*',apiProxy);
app.use('/img/*',imgProxy);

app.listen(3000);