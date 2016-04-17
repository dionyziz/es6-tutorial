---
layout: module
---
# 2. Χρησιμοποιώντας ```let``` μεταβλητές

Η ECMAScript 6 εισάγει ένα νέο keyword για να ορίζεις μεταβλητές: ```let```. Η διαφορά του με το ```var``` το οποίο είναι function-scoped, είναι ότι το ```let``` ορίζει μεταβλητές οι οποίες είναι block scoped: υπάρχουν μόνο στο code block που ορίστικαν.

Σε αυτή την ενότητα, θα αλλάξουμε την εφαρμογή μας ώστε να χρησιμοποιεί ```let``` μεταβλητές.


## Βήματα 

1. Στον editor σου, άνοιξε το αρχείο `js/main.js` και κοίταξε την συνάρτηση ```calculateMonthlyPayment```:

	```
	var calculateMonthlyPayment = function(principal, years, rate) {
		if (rate) {
			var monthlyRate = rate / 100 / 12;
		}
		var monthlyPayment = principal * monthlyRate / 
		                     (1 - (Math.pow(1/(1 + monthlyRate), years * 12)));
		return monthlyPayment;
	};
	```

	Παρατήρησε ότι στην γραμμή 5, η μεταβλητή `monthlyRate` είναι διαθέσιμη ενώ ορίστικε μέσα στο `if` block. Αυτό συμβαίνει επειδή μεταβλητές ορισμένες με `var` είναι **function-scoped** και όχι **block-scoped**. Βέβαια αυτή είναι κακή πρακτική να ορίζουμε μεταβλητές, ωστόσο εμείς το κάνουμε εδω για να τονίσουμε την διαφορά των function-scoped από τις block-scoped μεταβλητές.

	> Για να διατηρήσουμε το παράδειγμα απλό, το validation των inputs είναι σκοπίμως ελλιπές.	

1. Αντικατάστησε στον κώδικα όλα τα ```var``` με ```let```. **Μην αλλάξεις κάτι άλλο ακόμα**. 

	> Το main.js τώρα περιέχει ECMAScript 6 κώδικα και πλέον δεν δουλεύει σε browsers που υποστηρίζουν μόνο ECMAScript 5.

1. Στο command line, εκτέλεσε την ακόλουθη εντολή ώστε να τρέξεις το **babel** script και να κάνεις compile το `main.js` σε ECMAScript 5:

	```
    npm run babel
	```

1. Μπες από τον browser στο [http://localhost:8080](http://localhost:8080), και κάνε click στο κουμπί **Calculate**: **δεν δουλεύει**. Αν ανοιξεις το developer console θα δεις αυτό το error:
	
	![](images/scope-error.jpg)
	
	
	Αυτό συμβαίνει επειδή αντίθετα από τις ```var``` μεταβλητές που είναι **function-scoped**,  οι ```let``` μεταβλητές είναι **block-scoped**: υπάρχουν μόνο στο block που ορίστικαν. 

1. Στο `main.js`, άλλαξε την ```calculateMonthlyPayment```:

    ```
    let calculateMonthlyPayment = function(principal, years, rate) {
        let monthlyRate = 0;
        if (rate) {
            monthlyRate = rate / 100 / 12;
        }
        let monthlyPayment = principal * monthlyRate / 
                             (1 - (Math.pow(1/(1 + monthlyRate), years * 12)));
        return monthlyPayment;
    };
    ```

1. Στο command line, τρέξε αυτή την εντολή για να ξανακάνεις build την εφαρμογή σου:

	```
    npm run babel
	```

1. Μπες από τον browser στο [http://localhost:8080](http://localhost:8080), και κάνε click στο κουμπί **Calculate**: τώρα πρέπει να δεις την μηνιαία πληρωμή.

	> Αν βλέπεις ακόμα τα errors, σιγουρέψου ότι έχεις καθαρίσει την cache του browser και κάνε refresh.


## Επιπλέον Βιβλιογραφία

- [MDN let variables](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let)


<div class="row" style="margin-top:40px;">
<div class="col-sm-12">
<a href="ecmascript6-setup-babel.html" class="btn btn-default"><i class="glyphicon glyphicon-chevron-left"></i> Προηγούμενο</a>
<a href="ecmascript6-destructuring.html" class="btn btn-default pull-right">Επόμενο <i class="glyphicon glyphicon-chevron-right"></i></a>
</div>
</div>
