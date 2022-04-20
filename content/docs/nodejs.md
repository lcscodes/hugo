---
title: "Node.JS"
weight: 1
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: false
# bookSearchExclude: false
---

# Node.JS

## Pengantar Node.JS

### Node.JS

Node.js adalah runtime environment untuk JavaScript.

Dulu, javascript hanya bisa dieksekusi di browser dan hanya untuk frontend saja. Sekarang dengan Node.js, kita dapat menjalankan kode JavaScript di mana pun (frontend maupun backend), tidak hanya terbatas pada lingkungan browser saja.

### NPM

NPM adalah Node Package Manager. Digunakan untuk berbagi tool, menginstal modul, dan mengelola dependensi.

## Perintah Command Line

### Install Node.JS

Ubuntu

    sudo apt install nodejs

Cek Versi

    npm -v

### Install NPM

Ubuntu

    sudo apt install npm

Cek Versi

    node -v

### Initiate node.js file (Run Server Otomatis)

File yang dibuat harus di-inisiasi dulu oleh node.js sebelum action lain dijalankan.

    node app.js

## Membuat Server Node.JS

    const http = require('http');

    const hostname = 'sipkd.madiunkota.go.id';
    const port = 3000;

    const server = http.createServer((req, res) => {
        res.statusCode = 200;
        res.setHeader('Content-Type', 'text/plain');
        res.end('Hello World');
    });

    server.listen(port, hostname, () => {
        console.log(`Server running at http://${hostname}:${port}/`);
    });

Jalankan di terminal dengan perintah 'node app.js'

## Node.JS MySql

    npm install mysql

Membuat koneksi :

buatlah file koneksi.js

    var mysql = require('mysql');

    var con = mysql.createConnection({
    host: "localhost",
    user: "yourusername",
    password: "yourpassword"
    });

    con.connect(function(err) {
    if (err) throw err;
    console.log("Connected!");
    });

Jalankan di terminal dengan perintah 'node koneksi.js'

## Question & Answer

### NPM ERR: npm : Depends: node-gyp

Install manual package node.js yang kurang

    sudo apt-get install nodejs-dev node-gyp libssl1.0-dev
