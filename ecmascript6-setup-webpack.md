---
layout: module
---
# 6. Ρυθμίζοντας το Webpack

Τα modules υποστηρίζονταν στην JavaScript μέσω τρίτων βιβλιοθηκών. Η ECMAScript 6 προσθέτει native υποστήριξη για modules στη JavaScript. Όταν κάνεις compile μία modular ECMAScript 6 εφαρμογή σε ECMASCript 5, ο compiler επαφύεται σε τρίτες βιβλιοθήκες για να υλοποιήσει τα modules στην ECMAScript 5. Το [webpack](http://webpack.github.io/) και το [Browserify](http://browserify.org/) είναι δύο συνηθισμένες επιλογές, και το Babel τα υποστηρίζει και τα δύο (και άλλα). Σε αυτό το workshop χρησιμοποιούμε το Webpack.

Σε αυτή την ενότητα, προσθέτεις το Webpack στο περιβάλλον εργασίας σου.

## Βήμα 1: Ρύμιση του Webpack

1. Στη γραμμή εντολών, βεβαιώσου ότι είσαι στο φάκελο `es6-tutorial` και εγκατάστησε το **babel-loader** και το **webpack**:
   
   	```
   	npm install babel-loader webpack --save-dev
   	```

1. Άνοιξε το **package.json** στον editor σου και πρόσθεσε ένα **webpack** script (αμέσως μετά το **babel** script). Η ενότητα των scripts θα μοιάζει κάπως έτσι:

    ```
    "scripts": {
        "babel": "babel --presets es2015 js/main.js -o build/main.bundle.js",
	    "start": "http-server",
        "webpack": "webpack"
    },
    ```
    
1. Στο φάκελο `es6-tutorial`, φτιάξε ένα νέο αρχείο με το όνομα `webpack.config.js` που να μοιάζει ως εξής:
     
     ```
     var path = require('path');
     var webpack = require('webpack');
     
     module.exports = {
         entry: './js/main.js',
         output: {
             path: path.resolve(__dirname, 'build'),
             filename: 'main.bundle.js'
         },
         module: {
             loaders: [
                 {
                     test: /\.js$/,
                     loader: 'babel-loader',
                     query: {
                         presets: ['es2015']
                     }
                 }
             ]
         },
         stats: {
             colors: true
         },
         devtool: 'source-map'
     };
     ```

## Βήμα 2: Build χρησιμοποιώντας Webpack

1. Στη γραμμή εντολών, βεβαιώσου ότι είσαι στο φάκελο **es6-tutorial** και γράψε την ακόλουθη εντολή:
  
	```
    npm run webpack
	```
	
	> Το Webpack χρησιμοποιεί το Babel στο παρασκήνιο για να κάνει compile την εφαρμογή σου. Μπορείς να κάνεις build μία εφαρμογή χρησιμοποιώντας το Webpack ακόμη και αν αυτή η εφαρμογή δεν χρησιμοποιεί modules της ECMAScript 6. Με άλλα λόγια, το **babel** script στο package.json δεν χρειάζεται πλέον.

1. Άνοιξε ένα browser, μπες στο [http://localhost:8080](http://localhost:8080) και πάτησε το κουμπί **Calculate**.

## Επιπλέον βιβλιογραφία

- [Webpack documentation](http://webpack.github.io/docs/)

<div class="row" style="margin-top:40px;">
<div class="col-sm-12">
<a href="ecmascript6-template-strings.html" class="btn btn-default"><i class="glyphicon glyphicon-chevron-left"></i> Προηγούμενο</a>
<a href="ecmascript6-modules.html" class="btn btn-default pull-right">Επόμενο <i class="glyphicon glyphicon-chevron-right"></i></a>
</div>
</div>

