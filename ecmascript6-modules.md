---
layout: module
---
# 7. Χρησιμοποιώντας Modules

Σε αυτή την ενότητα θα δημιουργήσεις ένα module που κάνει διαθέσιμη την business λογική σχετική με το στεγαστικό δάνειο και θα κάνεις build την εφαρμογή σου μέσω του Webpack.

## Βήμα 1: Δημιούργησε το Module

1. Φτιάξε ένα νέο αρχείο με το όνομα `mortgage.js` στο φάκελο `js`. 
 
1. Αντίγραψε τις συναρτήσεις `calculateMonthlyPayment` και `calculateAmortization` από το `main.js` στο `mortgage.js`.
 
1. Πρόσθεσε την λέξη-κλειδί ```export``` μπροστά και από τις δύο συναρτήσεις για να τις κάνεις διαθέσιμες ως μέρος του δημόσιου API του module. Το `mortgage.js` θα μοιάζει κάπως έτσι: 

	```
	export let calculateMonthlyPayment = (principal, years, rate) => {
		let monthlyRate = 0;
		if (rate) {
			monthlyRate = rate / 100 / 12;
		}
		let monthlyPayment = principal * monthlyRate / (1 - (Math.pow(1/(1 + monthlyRate),
				years * 12)));
		return {principal, years, rate, monthlyPayment, monthlyRate};
	};
	
	export let calculateAmortization = (principal, years, rate) => {
		let {monthlyRate, monthlyPayment} = calculateMonthlyPayment(principal, years, rate);
		let balance = principal;
		let amortization = [];
		for (let y=0; y<years; y++) {
			let interestY = 0;  //Interest payment for year y
			let principalY = 0; //Principal payment for year y
			for (let m=0; m<12; m++) {
				let interestM = balance * monthlyRate;       //Interest payment for month m
				let principalM = monthlyPayment - interestM; //Principal payment for month m
				interestY = interestY + interestM;
				principalY = principalY + principalM;
				balance = balance - principalM;
			}
			amortization.push({principalY, interestY, balance});
		}
		return {monthlyPayment, monthlyRate, amortization};
	};
	```

## Βήμα 2: Χρησιμοποίησε το Module

1. Στο `main.js`, αφαίρεσε τις συναρτήσεις ```calculateMonthlyPayment``` και ```calculateAmortization```.

1. Πρόσθεσε την ακόλουθη εντολή ```import``` ως πρώτη γραμμή στο `main.js` ώστε να κάνεις import το mortgage module:

	```
	import * as mortgage from './mortgage';
	```
	
1. Στο click event handler του **calcBtn** άλλαξε την κλήση στη συνάρτηση ```calculateAmortization``` ως εξής: 	
	
	```
    let {monthlyPayment, monthlyRate, amortization} = 
    	mortgage.calculateAmortization(principal, years, rate);
	```

## Βήμα 3: Κάνε build και τρέξ' το

1. Στη γραμμή εντολών, γράψε την ακόλουθη εντολή για να ξανακάνεις build την εφαρμογή:

	```
    npm run webpack
	```

1.  Άνοιξε ένα browser, μπες στο [http://localhost:8080](http://localhost:8080) και κάνε κλικ στο κουμπί **Calculate**.	
	
	
## Επιπλέον βιβλιογραφία

- [MDN: import](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import)
- [MDN: export](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/export)
- [2ality: ECMAScript 6 modules: the final syntax](http://www.2ality.com/2014/09/es6-modules-final.html)

<div class="row" style="margin-top:40px;">
<div class="col-sm-12">
<a href="ecmascript6-setup-webpack.html" class="btn btn-default"><i class="glyphicon glyphicon-chevron-left"></i> Προηγούμενο</a>
<a href="ecmascript6-classes.html" class="btn btn-default pull-right">Επόμενο <i class="glyphicon glyphicon-chevron-right"></i></a>
</div>
</div>

