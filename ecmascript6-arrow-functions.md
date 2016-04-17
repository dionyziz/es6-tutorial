---
layout: module
---
# 4. Χρησιμοποιώντας Arrow Functions

Τα arrow functions στην ECMAScript 6 είναι μια συντομογραφία για τα functions της ECMAScript 5. Το περιεχόμενο του function μπορεί να είναι είτε block είτε κάποιο expression. Η τιμή του ```this``` μέσα στο function δεν αλλάζει: είναι ίδια με την τιμή του ```this``` έξω από το function. Δεν χρειαζόμαστε πλέον ```var self = this``` για να κρατάμε το scope.

Σε αυτή την ενότητα, θα προσθέσεις μια νέα συνάρτηση για να υπολογίσεις την αποπληρωμή του δανείου. Θα αλλάξεις επίσης τις παλιές σου συναρτήσεις ώστε να χρησιμοποιούν arrow functions.

## Βήματα

1. Άνοιξε το `js/main.js`. Αμέσως μετά από την συνάρτηση ```calculateMonthlyPayment```, πρόσθεσε μια συνάρτηση ```calculateAmortization```:

    ```
    let calculateAmortization = (principal, years, rate) => {
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
    
1. Άλλαξε τον ορισμό της συνάρτησης ```calculateMonthlyPayment```:
    
    ```
    let calculateMonthlyPayment = (principal, years, rate) => {
    ```
    
1. Επίσης τροποποίησε και τον ορισμό του click event handler για το κουμπί **calcBtn**:
  
    ```
    document.getElementById('calcBtn').addEventListener('click', () => {
    ```
    
1. Στον event handler του **calcBtn**, κάλεσε την συνάρτηση ```calculateAmortization``` αντί της ```calculateMonthlyPayment```:

    ```
	let {monthlyPayment, monthlyRate, amortization} = calculateAmortization(principal, years, rate);
	```
   
1. Στην τελευταία γραμμή του click event handler για το **calcBtn**, κάνε log τα δεδομένα της αποπληρωμής στο console (θα τα τυπώσουμε μέσα στην σελίδα σε επόμενη ενότητα): 

    ```
	amortization.forEach(month => console.log(month));
	```
	
	> Αυτό είναι παράδειγμα ενός arrow function που τρέχει μόνο κάποιο expression.

    Τελικά ο click event handler για το **calcBtn** πρέπει να μοιάζει κάπως έτσι:
    
    ```
    document.getElementById('calcBtn').addEventListener('click', () => {
    	let principal = document.getElementById("principal").value;
    	let years = document.getElementById("years").value;
    	let rate = document.getElementById("rate").value;
    	let {monthlyPayment, monthlyRate, amortization} = calculateAmortization(principal, years, rate);
    	document.getElementById("monthlyPayment").innerHTML = monthlyPayment.toFixed(2);
    	document.getElementById("monthlyRate").innerHTML = (monthlyRate * 100).toFixed(2);
    	amortization.forEach(month => console.log(month));
    });
    ```
    
1. Στο command line τρέξε αυτή την εντολή για να ξανακάνεις build την εφαρμογή:
    
    ```
    npm run babel
    ```

1. Από τον browser, μπες στο  [http://localhost:8080](http://localhost:8080), και κάνε click στο κουμπί **Calculate**. Άνοιθξε το developer console: θα πρέπει εκεί να δεις τυπωμένες τις τιμές της αποπληρωμής.

    ![](images/amortization-in-console.jpg)


## Επιπλέον Βιβλιογραφία

- [MDN: Arrow functions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions)
- [2ality: ECMAScript 6: arrow functions and method definitions](http://www.2ality.com/2012/04/arrow-functions.html)

<div class="row" style="margin-top:40px;">
<div class="col-sm-12">
<a href="ecmascript6-destructuring.html" class="btn btn-default"><i class="glyphicon glyphicon-chevron-left"></i> Προηγούμενο</a>
<a href="ecmascript6-template-strings.html" class="btn btn-default pull-right">Επόμενο <i class="glyphicon glyphicon-chevron-right"></i></a>
</div>
</div>

