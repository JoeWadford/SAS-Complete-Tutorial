# SAS Complete Tutorial | Udemy | Visual Representation of Data

[Home Page](https://github.com/JoeWadford/SAS-Complete-Tutorial)

## Scatter Plot

	data housescatter;
	input Type$ Price TaxValue;
	CARDS;
	Single 300000 20000
	Single 250000 25000
	Duplex 175000 15000
	Duplex 150000 10000
	Single 400000 18000
	Single 450000 19000
	Duplex 210000 5000
	Duplex 200000 7000
	Single 700000 40000
	; 
	run;

	goptions ftext=arial;
	proc gplot data=housescatter;
	Title "Comparing Price and Tax by Home Type";
	format price dollar9.;
	symbol1 value=dot cv=blue;
	symbol2 value=square cv=red;
	plot price*TaxValue=type;
	run;

## Bar Graph

	data housescatter;
	input Type$ Price TaxValue;
	CARDS;
	Single 300000 20000
	Single 250000 25000
	Duplex 175000 15000
	Duplex 150000 10000
	Single 400000 18000
	Single 450000 19000
	Duplex 210000 5000
	Duplex 200000 7000
	Single 700000 40000
	; 
	run;

	goptions ftext=arial;
	proc gchart data=housescatter;
	Title "Comparing Price and Tax by Home Type";
	format price dollar9.;
	vbar price taxvalue / group=type;
	/* use hbar if you want the bars to be horizontal */
	pattern color = yellow;
	run;

[Home Page](https://github.com/JoeWadford/SAS-Complete-Tutorial)