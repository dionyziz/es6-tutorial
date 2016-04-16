---
layout: module
---
# 9. Χρησιμοποιώντας Promises

Τα promises έχουν αντικαταστήσει τις συναρτήσεις callback όσο αφορά το προτεινόμενο στυλ προγραμματισμού για το χειρισμό ασύγχρονων κλήσεων. Ένα promise κρατά ένα αποτέλεσμα (ή ένα σφάλμα) το οποίο θα γίνει διαθέσιμο στο μέλλον (όταν η ασύγχρονη κλήση επιστρέψει). Τα promises ήταν διαθέσιμα στην JavaScript μέσω τρίων βιβλιοθηκών (για παράδειγμα [jQuery](https://api.jquery.com/promise/) και [q](https://github.com/kriskowal/q)). Η ECMAScript 6 προσθέτει built-in υποστήριξη για promises στη JavaScript. 
 
Σε αυτή την ενότητα δημιουργείς μία απλή εφαρμογή που ονομάζεται ratefinder η οποία επιστρέφει μία λίστα με διαθέσιμες προσφορές στεγαστικών δανείων. 

## Μέρος 1: Χρησιμοποίησε ένα Promise

Για να δείξουμε τη χρήση promises σε αυτό το παράδειγμα, θα χρησιμοποιήσουμε την νέα συνάρτηση ```fetch()```. Αυτή τη στιγμή η ```fetch()``` είναι διαθέσιμη στην τελευταία έκδοση των Chrome, Firefox, και Opera, αλλά όχι στους IE και Safari. Μπορείς να δεις τη διαθεσιμότητα της `fetch()` [εδώ](http://caniuse.com/#feat=fetch). Μπορείς να διαβάσεις περισσότερα για την `fetch()` [εδώ](http://jakearchibald.com/2015/thats-so-fetch/).

1. Φτιάξε ένα αρχείο με το όνομα `ratefinder.html` στο φάκελο `es6-tutorial`. Γράψε τον παρακάτω κώδικα στο αρχείο:

    ```
    <!DOCTYPE html>
    <html>
    <head>
    	<meta charset="utf-8">
    </head>
    <body>
    	<table id="rates"></table>
        <script src="build/ratefinder.bundle.js"></script>
    </body>
    </html>
    ```
 
1. Δημιούργησε ένα αρχείο `ratefinder.js` στο φάκελο `es6-tutorial/js`. Γράψε τον παρακάτω κώδικα στο αρχείο:

    ```
    let url = "rates.json";
    
    fetch(url)
        .then(response => response.json())
        .then(rates => {
          let html = '';
          rates.forEach(rate => html += `<tr><td>${rate.name}</td><td>${rate.years}</td><td>${rate.rate}%</td></tr>`);
          document.getElementById("rates").innerHTML = html;
        })
        .catch(e => console.log(e));
    ```
    
    > Για να απλοποιήσουμε τα πράγματα, αυτός ο κώδικας χρησιμοποιεί ένα στατικό αρχείο δεδομένων: rates.json. Η εφαρμογή θα δούλευε και με κάποιο URL που να δείχνει σε κάποια απομακρυσμένη υπηρεσία.

1. Άνοιξε το `webpack.config.js` στον editor σου. Στο `module.exports` άλλαξε τα στοιχεία των κλειδιών entry και output ως εξής:         

    ```
    entry: {
        app: './js/main.js',
        ratefinder: './js/ratefinder.js'
    },
    output: {
        path: path.resolve(__dirname, 'build'),
        filename: '[name].bundle.js'
    },
    ```                

    > Το script **webpack** τώρα θα κάνει compile δύο εφαρμογές: την **main.js** και την **ratefinder.js**. Θα δημιουργήσει δύο compiled αρχεία με βάση το όνομα entry: **app.bundle.js** και **ratefinder.bundle.js**.         
            
1. Στη γραμμή εντολών γράψε την παρακάτω εντολή για να ξανακάνεις build την εφαρμογή:

	```
    npm run webpack
	```

1. Άνοιξε ένα browser και μπες στο [http://localhost:8080/ratefinder.html](http://localhost:8080/ratefinder.html).
          

## Part 2: Δημιουργώντας ένα Promise

Συνήθως αυτό που έχεις να κάνεις είναι να χρησιμοποιείς promises που επιστρέφονται από built-in ή τρίτα API. Συχνά χρειάζεται επίσης να δημιουργήσεις τα δικά σου promises. Σε αυτή την ενότητα δημιουργείς ένα mock data service για να εξοικιωθείς με τη διαδικασία δημιουργίας promises της ECMAScript 6. Το mock data service χρησιμοποιεί ένα ασύγχρονο API ώστε να αντικαταστήσει μία πραγματικά ασύγχρονη υπηρεσία δεδομένων για δοκιμές ή άλλους σκοπούς.

1. Δημιούργησε ένα νέο αρχείο με το όνομα `rate-service-mock.js` στο φάκελο `js`. 

1. Στο rate-service-mock.js, όρισε μία μεταβλητή ```rates``` με κάποια παραδείγματα δεδομένων:
 
    ```
    let rates = [
        {
            "name": "30 years fixed",
            "rate": "13",
            "years": "30"
        },
        {
            "name": "20 years fixed",
            "rate": "2.8",
            "years": "20"
        }
    ];
    ```
 
1. Όρισε μία συνάρτηση ```findAll()``` ως εξής:

    ```
    export let findAll = () => new Promise((resolve, reject) => {
        if (rates) {
            resolve(rates);
        } else {
            reject("No rates");
        }
    });
    ```
    
1. Άνοιξε το `ratefinder.js`. Άλλαξε την υλοποίηση ως εξής:

    ```
    import * as service from './rate-service-mock';
    
    service.findAll()
        .then(rates => {
            let html = '';
            rates.forEach(rate => html += `<tr><td>${rate.name}</td><td>${rate.years}</td><td>${rate.rate}%</td></tr>`);
            document.getElementById("rates").innerHTML = html;
        })
        .catch(e => console.log(e));
    ```
    
1. Στη γραμμή εντολών γράψε την ακόλουθη εντολή για να ξανακάνεις build την εφαρμογή σου:

	```
    npm run webpack
	```

1. Άνοιξε ένα browser και μπες στο [http://localhost:8080/ratefinder.html](http://localhost:8080/ratefinder.html).
    

## Επιπλέον βιβλιογραφία

- [MDN: Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)
- [2ality: Promises](http://www.2ality.com/2014/09/es6-promises-foundations.html)
- [MDN: Fetch](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch)

<div class="row" style="margin-top:40px;">
<div class="col-sm-12">
<a href="ecmascript6-classes.html" class="btn btn-default"><i class="glyphicon glyphicon-chevron-left"></i> Προηγούμενο</a>
<a href="next.html" class="btn btn-default pull-right">Επόμενο <i class="glyphicon glyphicon-chevron-right"></i></a>
</div>
</div>
