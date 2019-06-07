# SAS Complete Tutorial | Udemy | SAS Functions

[Home Page](https://github.com/JoeWadford/SAS-Complete-Tutorial)

## catx Functions

	data bringittogether;
		separator=',';
		first='   Larry';
		last='Larryson   ';
		result=catx(separator,first,last);
		/* gets rid of leading or trailing blanks.  also allows us to use a delimiter. concatenates char strings 
	   	the delimiter is always entered first.  catx(delimiter, var1, var2, varx)
	   	cat function brings together char strings but does not get rid of spaces */
	drop separator;
	run;

	proc print data=bringittogether;
	run;

## coalesce Function

	data coalesce;
	input home cell;
	numavailable=coalesce(home,cell);
	/* will return the first available phone number. e.g. if home is missing, coalesce will return the cell */
	datalines;
	.
	6448565
	;
	run;

	proc print data=coalesce;
	run;

## Compress Functions

	data compressed;
	input phonen$1-15;
	phone1 = compress(phonen);
	phone2 = compress(phonen, '(-)','s');
	datalines;
	(314)456-4768
	(314) 453-56 78
	;
	run;

	proc print data=compressed;
	run;

## Input and Put Functions

	/* going from character to numeric */
	data inputfunc;
	input sale$9.; 
	numsale=input(sale,comma9.);
	/* comma9. gets rid of the commas */
	datalines;
	6,515,353
	;
	run;

		proc print data=inputfunc;
		run;

		proc contents data=inputfunc;
		run;
	
	/* going from numeric to character */
	data inputfunc1;
	input sale1;
	charsale=put(sale1,7.);
	datalines;
	6515353
	;
	run;

		proc print data=inputfunc1;
		run;

		proc contents data=inputfunc1;
		run;

## Length Lengthn and Lengthc

	/* Length statement, and Length, Lengthn, and LengthC Functions */
	/* lengthn returns the length of a character string, excluding trailing blanks */
	/* lengthc returns the length including trailing blanks */

	Data lengthfunctions;
		one = 'ABC   ';
		two = ' '; /* character missing value */
		three = 'ABC   XYZ';
	
		length_one = length(one);
		/* length function does not include the trailing blanks */
	
		lengthn_one = lengthn(one);
		/* lengthn does not include the trailing blanks */
	
		lengthc_one = lengthc(one);
		/* lengthc includes everything including trailing blanks */
	
		length_two = length(two);
		/* length function does include the blanks as they are not trailing */
	
		lengthn_two = lengthn(two);
		/* lengthn does not count the blanks here */
	
		lengthc_two = lengthc(two);
	
		length_three = length(three);
		/* counts as nine (9) because the blanks are between two character strings so it MUST count the blanks */
	
		lengthn_three = lengthn(three);
		/* lengthn does count the blanks between character strings */
	
		lengthc_three = lengthc(three);
	run;

	proc print data = lengthfunctions;
		title 'Length(n)(c) Function Examples';
	run;

## RAND Functions

	data rand;
	call streaminit(12345);
	do i = 1 to 50;
		x = rand("Normal");
		output;
	end;
	run;

	proc sgplot data=rand;
	title "Random Values from N(0,1)";
	histogram x;
	run;

	proc freq data=rand;
	run;

## Scan Functions

	data bringittogether1;
		separator=',';
		first='   larry';
		last='larryson   ';
		result=catx(separator,PROPCASE(first),PROPCASE(last));
		scann = scan(result,1);
		/* please scan the result variable and return the first word */
	drop separator;
	run;

	proc print data=bringittogether1;
	run;

## substr Function

	data bringittogether1;
		separator=',';
		first='   larry';
		last='larryson   ';
		result=catx(separator,PROPCASE(first),PROPCASE(last));
		scann = scan(result,1);
		/* please scan the result variable and return the first word */
	drop separator;
	run;

	proc print data=bringittogether1;
	run;

## Trim Lecture

	data trimlecture;
		input firstname$ lastname$ age tscore;
		length name$20;
		name=trim(lastname)||', '||(firstname);
		/* trim removes trailing blanks */
		datalines;
	Alex Benson 27 45
	; 
	run;

	proc contents data=trimlecture;
	run;

	proc print data=trimlecture;
	run;

## Verify Function

	data errors valid;
	input id$ stage : $5.;
	if verify(stage,'abcd') then output errors;
	/* verify function returns the position of the first character in a string that is not in adny of several other strings
	verify(source, excerpt) */
	else output valid;
	cards;
	001 aabcdefg
	002 aabqc
	; 
	/* note that 001 did not read any characters after the fifth character because of input code $5. */
	run;

	proc print data=errors;
	title 'Errors';
	run;

	proc print data=valid;
	title 'Valid';
	run;

[Home Page](https://github.com/JoeWadford/SAS-Complete-Tutorial)