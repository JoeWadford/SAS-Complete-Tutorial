# SAS Complete Tutorial | Udemy | Working with Data

[Home Page](https://github.com/JoeWadford/SAS-Complete-Tutorial)

## Dataset Options

	data salaryemp (keep=salary rename=salary=salaryemp); 
	infile '/home/u1421477/salary (2).txt';
	input year salary;
	run;

	proc print data=salaryemp(firstobs=3 obs=4);
	run;

## Delimiters

	/* delimiter = anything that separates values. DLM */

	/* in this example, assume delimiter is a period . */

	data salary;
	infile '/home/u1421477/salary (2).txt' DLM=".";
	input year salary;
	run;

## Instream

	/*instream = typing data right into coding area*/
 
	data beer;

	input brand$ origin $ price;
	/* CARDS = there are data lines following this statement*/
	cards;
	Budweiser USA 14.99
	Heineken NED 13.99
	Corona MEX 12.99
	SamAdams USA 14.79
	Guiness IRE 17.99
	;
	run;

	data beer1;
	input brands$ 1-9 origin$ 10-12 price 13-17;
	/* column definitions list the exact spaces used for each column*/
	cards;
	BudweiserUSA14.99
	Heineken NED13.99
	Corona   MEX12.99
	SamAdams USA14.79
	Guiness  IRE17.99
	;
	run;

	/* output data contains two tables now. You can see both by switching tables in the upper left hand corner*/

## Intro to Dates

	data dates;
	/* use date11. right after the column using a date*/
	input name$ bday date11.;
	CARDS;
	Eric 4 Mar 1985
	Doug 15 Feb 1976
	Sean 14 Jun 1975
	Lisa 5 Jan 1988
	; 
	run;

	proc print data=dates; 
	FORMAT bday date9.;
	run;

## Create New Variables

	data houseprice;
	infile '/home/u1421477/houseprice (2).txt';
	input Type$ Price TaxPercent;
	TaxValue= Round (Price * TaxPercent);
	run;

	/* using instream to create  new variable*/
	data houseprice1;
	input Type$ Price TaxPercent;
	TaxValue= Round (Price * TaxPercent);
	DATALINES;
	Single 300000 0.20
	Single 250000 0.25
	Duplex 175000 0.15
	run;

## More With Creating Variables

	data sales;
	input Name$ Sales_1-Sales_4;
	Total = sum (of Sales_1-Sales_4);
	CARDS;
	Greg 10 2 40 0
	John 15 5 10 100
	Lisa 50 10 15 50
	Mark 20 0 5 20
	;
	run;

## Filtering Observations

	data filter;
	/* this might not work in the future as houseprice is a temp dataset*/
	SET houseprice;
	IF price<200000; 
	run;

## If Then Conditional Logic

	data sales;
	input Name$ Sales_1-Sales_4;
	Total = sum (of Sales_1-Sales_4);
	Fired = '';
	/* IF Then*/
	If Name='Greg' AND Total=>52 Then
	Do; 
	Fired='N';
	Total=Total+10;
	End;
	datalines;
	Greg 10 2 40 0
	John 15 5 10 100
	Lisa 50 10 15 50
	Mark 20 0 5 20
	;
	run;

	proc print data=sales;
	run;


	data sales1;
	input Name$ Sales_1-Sales_4;
	Total = sum (of Sales_1-Sales_4);
	Fired = '';
	Performance='';
	/* IF Then*/
	If Total=<10 Then Performance='l';
	else if Total=<50 then Performance='a';
	else Performance='h';
	datalines;
	Greg 10 2 40 0
	John 15 5 10 100
	Lisa 50 10 15 50
	Mark 20 0 5 20
	;
	run;

	proc print data=sales1;
	run;

## Where Statements

	data sales;
	input Name$ Sales_1-Sales_4;
	Total = sum (of Sales_1-Sales_4);
	CARDS;
	Greg 10 2 40 0
	John 15 5 10 100
	Lisa 50 10 15 50
	Mark 20 0 5 20
	;
	run;


	/* where from sql*/
	proc sql;
	Select Total from sales
	where Total > 50;
	run;

	/* where as dataset option*/
	proc print data=sales(where=(total>50));
	run;

	/* where included in data and proc steps*/
	proc print data=sales;
	where total>50;
	run;

[Home Page](https://github.com/JoeWadford/SAS-Complete-Tutorial)