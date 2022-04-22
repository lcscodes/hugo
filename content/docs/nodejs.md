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

Node.js adalah runtime environment untuk JavaScript. Sama halnya dengan .NET ataupun JRE pada Java.

Dulu, javascript hanya bisa dieksekusi di browser dan hanya untuk frontend saja. Sekarang dengan Node.js, kita dapat menjalankan kode JavaScript di mana pun (frontend maupun backend), tidak hanya terbatas pada lingkungan browser saja.

### NPM

NPM adalah Node Package Manager. Digunakan untuk berbagi tool, menginstal modul, dan mengelola dependensi.

### Express

Express adalah framework aplikasi web Node.js. Bagus untuk membuat API karena minimal, cepat dan mudah.

## Perintah Command Line

### Install Node.JS

Ubuntu

    sudo apt install nodejs

Cek Versi

    npm -v

Membuat package.json

    npm init

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
        res.writeHead(200,{
            "Content-Type" : "text/html"
        });
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

## CRUD Node.JS, Express, Bootstrap & MySQL

1.  Siapkan (download) bootstrap & jquery

    https://getbootstrap.com/

    https://jquery.com/

2.  Siapkan database dan table mysql

    nama db: example
    nama table: user
    field: id, username, password

3.  Buat folder project

    nama folder: crud

4.  Buat package.json

    jalankan perintah command line berikut di dalam folder project.

        npm init

    Perintah diatas akan membuat sebuah file bernama package.json secara otomatis pada project Anda.

5.  Install dependencies

    Dependencies disini adalah fitur pendukung (seperti: framework, driver, middleware, template) yang harus disediakan untuk menyempurnakan alur aplikasi. Dependencies yang dibutuhkan adalah :

    1. Express (node.js web framework)
    2. MySQL (driver mysql untuk node.js)
    3. Body-parser (middleware untuk menjalankan post body request)
    4. Handlebars (template engine (seperti blade di laravel) )

    Instal dependencies yang dibutuhkan dengan mengetik perintah berikut.

        npm install --save express mysql body-parser hbs

    Perintah diatas akan menginstall semua dependencies yang kita butuhkan yaitu: express, mysql, body-parser, dan handlebars. Kita bisa pantau dependencies yang terinstall di dalam file package.json.

6.  Struktur Project

    Buat folder public dan views di dalam project folder crud.

    Buat folder css dan js di dalam folder public.

    Copy file-file bootstrap.css yang telah di download sebelumnya kedalam folder public/css/.

    Copy file-file bootstrap.js dan jquery pada folder public/js/.

7.  Index.js

    Buat file dengan nama index.js di dalam folder project crud. Ketikkan kode berikut.

        //use path module
        const path = require('path');
        //use express module
        const express = require('express');
        //use hbs view engine
        const hbs = require('hbs');
        //use bodyParser middleware
        const bodyParser = require('body-parser');
        //use mysql database
        const mysql = require('mysql');
        const app = express();

        //konfigurasi koneksi
        const conn = mysql.createConnection({
            host: 'localhost',
            user: 'root',
            password: '',
            database: 'example'
        });

        //connect ke database
        conn.connect((err) => {
            if (err) throw err;
            console.log('Mysql Connected...');
        });

        //set views file
        app.set('views', path.join(__dirname, 'views'));
        //set view engine
        app.set('view engine', 'hbs');
        app.use(bodyParser.json());
        app.use(bodyParser.urlencoded({ extended: false }));
        //set folder public sebagai static folder untuk static file
        app.use('/assets', express.static(__dirname + '/public'));

        //route untuk homepage
        app.get('/', (req, res) => {
            let sql = "SELECT * FROM user";
            let query = conn.query(sql, (err, results) => {
                if (err) throw err;
                res.render('user_view', {
                    results: results
                });
            });
        });

        //route untuk insert data
        app.post('/save', (req, res) => {
            let data = { username: req.body.username, password: req.body.password };
            let sql = "INSERT INTO user SET ?";
            let query = conn.query(sql, data, (err, results) => {
                if (err) throw err;
                res.redirect('/');
            });
        });

        //route untuk update data
        app.post('/update', (req, res) => {
            let sql = "UPDATE user SET username='" + req.body.username + "', password='" + req.body.password + "' WHERE id=" + req.body.id;
            let query = conn.query(sql, (err, results) => {
                if (err) throw err;
                res.redirect('/');
            });
        });

        //route untuk delete data
        app.post('/delete', (req, res) => {
            let sql = "DELETE FROM user WHERE id=" + req.body.id + "";
            let query = conn.query(sql, (err, results) => {
                if (err) throw err;
                res.redirect('/');
            });
        });

        //server listening
        app.listen(8000, () => {
            console.log('Server is running at port 8000');
        });

8.  View

    Buat file dengan nama user_view.hbs didalam folder views. Lalu ketikkan kode berikut.

        <html lang="en">

        <head>
            <meta charset="utf-8">
            <title>CRUD Node.js and Mysql</title>
            <link href="/assets/css/bootstrap.css" rel="stylesheet" type="text/css" />
        </head>

        <body>
            <div class="container">
                <h2>User List</h2>
                <button type="button" class="btn btn-success" data-bs-toggle="modal" data-bs-target="#myModalAdd">
                    Add New
                </button>
                <table class="table table-striped" id="mytable">
                    <thead>
                        <tr>
                            <th>ID</th>
                            <th>Username</th>
                            <th>Password</th>
                            <th>Action</th>
                        </tr>
                    </thead>
                    <tbody>
                        {{#each results}}
                        <tr>
                            <td>{{ id }}</td>
                            <td>{{ username }}</td>
                            <td>{{ password }}</td>
                            <td>
                                <a href="javascript:void(0);" class="btn btn-sm btn-info edit" data-id="{{ id }}"
                                    data-username="{{ username }}" data-password="{{ password }}">Edit</a>
                                <a href="javascript:void(0);" class="btn btn-sm btn-danger delete"
                                    data-id="{{ id }}">Delete</a>
                            </td>
                        </tr>
                        {{/each}}
                    </tbody>
                </table>
            </div>

            <!-- Modal Add Produk-->
            <div class="modal fade" id="myModalAdd" tabindex="-1" role="dialog" aria-labelledby="exampleModalLabel"
                aria-hidden="true">
                <form action="/save" method="post">
                    <div class="modal-dialog" role="document">
                        <div class="modal-content">
                            <div class="modal-header">
                                <h5 class="modal-title" id="exampleModalLabel">Add New User</h5>
                                <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
                            </div>
                            <div class="modal-body">
                                <div class="form-group">
                                    <input type="text" name="username" class="form-control" placeholder="Nama User"
                                        required>
                                </div>

                                <div class="form-group">
                                    <input type="text" name="password" class="form-control" placeholder="Password" required>
                                </div>
                            </div>
                            <div class="modal-footer">
                                <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
                                <button type="submit" class="btn btn-primary">Save</button>
                            </div>
                        </div>
                    </div>
                </form>
            </div>


            <!-- Modal Update Produk-->
            <form action="/update" method="post">
                <div class="modal fade" id="EditModal" tabindex="-1" role="dialog" aria-labelledby="exampleModalLabel"
                    aria-hidden="true">
                    <div class="modal-dialog" role="document">
                        <div class="modal-content">
                            <div class="modal-header">
                                <h5 class="modal-title" id="exampleModalLabel">Edit Product</h5>
                                <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
                            </div>
                            <div class="modal-body">
                                <div class="form-group">
                                    <input type="text" name="username" class="form-control username" placeholder="Nama User"
                                        required>
                                </div>

                                <div class="form-group">
                                    <input type="text" name="password" class="form-control password" placeholder="Password"
                                        required>
                                </div>
                            </div>
                            <div class="modal-footer">
                                <input type="hidden" name="id" class="id">
                                <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
                                <button type="submit" class="btn btn-primary">Update</button>
                            </div>
                        </div>
                    </div>
                </div>
            </form>

            <!-- Modal Delete Produk-->
            <form id="add-row-form" action="/delete" method="post">
                <div class="modal fade" id="DeleteModal" tabindex="-1" role="dialog" aria-labelledby="myModalLabel"
                    aria-hidden="true">
                    <div class="modal-dialog">
                        <div class="modal-content">
                            <div class="modal-header">
                                <h5 class="modal-title" id="myModalLabel">Delete User</h5>
                                <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
                            </div>
                            <div class="modal-body">
                                <strong>Anda yakin mau menghapus data ini?</strong>
                            </div>
                            <div class="modal-footer">
                                <input type="hidden" name="id" class="form-control id2" required>
                                <button type="button" class="btn btn-default" data-bs-dismiss="modal">Close</button>
                                <button type="submit" class="btn btn-success">Delete</button>
                            </div>
                        </div>
                    </div>
                </div>
            </form>

            <script src="/assets/js/jquery-3.6.0.js"></script>
            <script src="/assets/js/bootstrap.js"></script>
            <script>
                $(document).ready(function () {
                    //tampilkan data ke modal untuk edit
                    $('#mytable').on('click', '.edit', function () {
                        var id = $(this).data('id');
                        var username = $(this).data('username');
                        var password = $(this).data('password');
                        $('#EditModal').modal('show');
                        $('.username').val(username);
                        $('.password').val(password);
                        $('.id').val(id);
                    });
                    //tampilkan modal hapus record
                    $('#mytable').on('click', '.delete', function () {
                        var id = $(this).data('id');
                        $('#DeleteModal').modal('show');
                        $('.id2').val(id);
                    });

                });
            </script>
        </body>

    </html>

    9.  Testing

        Uji coba dengan perintah berikut.

            node index

## Question & Answer

### NPM ERR: npm : Depends: node-gyp

Install manual package node.js yang kurang

    sudo apt-get install nodejs-dev node-gyp libssl1.0-dev

## Referensi

ref: https://mfikri.com/artikel/crud-nodejs-mysql

ref: https://mfikri.com/artikel/tutorial-nodejs

ref: https://mfikri.com/artikel/tutorial-express-pemula

ref: https://mfikri.com/artikel/express-mysql-vue

ref: https://www.youtube.com/watch?v=es9_6RFR7wk
