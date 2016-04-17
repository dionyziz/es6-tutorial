---
layout: module
---
# 3. Κάνοντας Destructuring

Η ECMAScript 6 δίνει μια νεα δυνατότητα που μας διευκολύνει στην δημιουργία αντικειμένων από μεταβλητές, αλλά και στην δημιουργία μεταβλητών από αντικείμενα ή πίνακες.

Σε αυτή την ενότητα, θα αλλάξεις την συνάρτηση calculateMonthlyPayment ώστε να επιστρέφει πολλές μεταβλητές: την μηνιαία πληρωμή, το μηνιαίο rate καθώς και άλλες παραμέτρους σχετικά με το δάνειο. Με την νέα σύνταξη της ECMAScript 6 για δημιουργία και destructuring αντικειμένων, αυτή η αλλαγή γίνεται εύκολα.

## Βήμα 1: Δημιουργώντας αντικείμενα από μεταβλητές

1. Άνοιξε το `js/main.js` στον editor σου. 

1. Άλλαξε το return της συνάρτησης ```calculateMonthlyPayment```:

    ```
    return {principal, years, rate, monthlyPayment, monthlyRate};
    ```

    Έτσι είναι ένας πιο σύντομος τρόπος αν γράφαμε το αντίστοιχο σε ECMAScript 5:

    ```
    return { principal: principal, 
             years: years, 
             rate: rate, 
             monthlyPayment: monthlyPayment, 
             monthlyRate: monthlyRate };
    ```
    
    
## Βήμα 2: Δημιουργώντας μεταβλητές από αντικείμενα κάνοντας Destructuring
    
1. Άνοιξε το  **index.html**. Πρόσθεσε το ```<h3>``` από κάτω έτσι ώστε να τυπώνεις το **monthly rate** κάτω από το **monthly payment**:

    ```
    <h2>Monthly Payment: <span id="monthlyPayment" class="currency"></span></h2>
    <h3>Monthly Rate: <span id="monthlyRate"></span></h3>
    ```

1. Άνοιξε το `main.js`. Στον click event handler του **calcBtn** , άλλαξε την κλήση στην ```calculateMonthlyPayment```:

    ```   
    let {monthlyPayment, monthlyRate} = calculateMonthlyPayment(principal, years, rate);
    ```

    Το οποίο είναι συντομογραφία του αντίστοιχου κώδικα σε ECMAScript 5:
    
    ```
    var mortgage = calculateMonthlyPayment(principal, years, rate);
    var monthlyPayment = mortgage.monthlyPayment;
    var monthlyRate = mortgage.monthlyRate;
    ```

1. Στην τελευταία γραμμή του event handler για το click στο **calcBtn**, πρόσθεσε τον ακόλουθο κώδικα ώστε να εμφανιστεί το μηνιαίο rate κάτω από την μηνιαία πληρωμή:

    ```
    document.getElementById("monthlyRate").innerHTML = (monthlyRate * 100).toFixed(2);
    ```

## Βήμα 3: Build & Run

1. Στο command line, τρέξε την ακόλουθη εντολή ώστε να ξαναγίνει build η εφαρμογή:

    ```
    npm run babel
    ```

1. Μπες από τον browser στο [http://localhost:8080](http://localhost:8080), και κάνε click στο κουμπί **Calculate**.

    ![](images/calc-rate.jpg)
    
    
## Επιπλέον Βιβλιογραφία

- [MDN: Destructuring assignment](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)
- [2ality: Destructuring and parameter handling in ECMAScript 6](http://www.2ality.com/2015/01/es6-destructuring.html)

<div class="row" style="margin-top:40px;">
<div class="col-sm-12">
<a href="ecmascript6-let.html" class="btn btn-default"><i class="glyphicon glyphicon-chevron-left"></i> Προηγούμενο</a>
<a href="ecmascript6-arrow-functions.html" class="btn btn-default pull-right">Επόμενο <i class="glyphicon glyphicon-chevron-right"></i></a>
</div>
</div>
