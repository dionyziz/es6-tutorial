---
layout: module
---
# 5. Χρησιμοποιώντας Template Strings

Στην ECMAScript 6, τα template strings είναι μονής ή πολλαπλών γραμμών αλφαριθμητικά τα οποία ορίζονται χρησιμοποιώντας τον χαρακτήρα \` (back-tick). Επιτρέπουν επίσης embedded expressions: ```${ }```

Σε αυτή την ενότητα, θα χρησιμοποιήσουμε template strings για να φτιάξουμε τον πίνακα με τα στοιχεία της αποπληρωμής του δανείου.

## Βήματα
	 
1. Στο `index.html`, πρόσθεσε τον ακόλουθο HTML κώδικα κάτω από το ```<h3>``` (monthly rate):
 
    ```
    <table>
        <thead>
        <tr>
            <th>Year</th>
            <th class="principal">Principal</th>
            <th class="stretch"></th>
            <th class="interest">Interest</th>
            <th>Balance</th>
        </tr>
        </thead>
        <tbody id="amortization"></tbody>
    </table>
    ```
 
1. Στο `main.js`, πρόσθεσε τον ακόλουθο κώδικα στο τέλος του click event handler για το **calcBtn**:  	 

    ```
	let html = "";
	amortization.forEach((year, index) => html += `
		<tr>
			<td>${index + 1}</td>
			<td class="currency">${Math.round(year.principalY)}</td> 
			<td class="stretch">
				<div class="flex">
					<div class="bar principal" 
						 style="flex:${year.principalY};-webkit-flex:${year.principalY}">
					</div>
					<div class="bar interest" 
						 style="flex:${year.interestY};-webkit-flex:${year.interestY}">
					</div>
				</div>
			</td>
			<td class="currency left">${Math.round(year.interestY)}</td> 
			<td class="currency">${Math.round(year.balance)}</td>
		</tr>
	`);
	document.getElementById("amortization").innerHTML = html;
	```
	
1. Τρέξε την ακόλουθη εντολή στο command line για να ξανακάνεις build την εφαρμογή:
    
    ```
    npm run babel
    ```

1. Από τον browser μπες στο [http://localhost:8080](http://localhost:8080), και κάνε click στο κουμπί **Calculate**.

    ![](images/amortization-table.jpg)


## Επιπλέον Βιβλιογραφία:

- [MDN: Template strings](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/template_strings)
- [2ality: HTML templating with ES6 template strings](http://www.2ality.com/2015/01/template-strings-html.html)


<div class="row" style="margin-top:40px;">
<div class="col-sm-12">
<a href="ecmascript6-arrow-functions.html" class="btn btn-default"><i class="glyphicon glyphicon-chevron-left"></i> Προηγούμενο</a>
<a href="ecmascript6-setup-webpack.html" class="btn btn-default pull-right">Επόμενο <i class="glyphicon glyphicon-chevron-right"></i></a>
</div>
</div>

