# SAS Complete Tutorial | Udemy | Arrays

[Home Page](https://github.com/JoeWadford/SAS-Complete-Tutorial)

## Arrays

	data sixvar;
	infile '/home/u1421477/6var (2).txt';
	input var_1 var_2 var_3 var_4 var_5 var_6;
	run;

	/* long way with if then statement.  you would have to repeat the below for each var*/
	data recode;
	set sixvar;
	if var_2<5 then var_2=.;
	run;

	proc print data=recode; run;

	/* easier way with ARRAYS */

	data recodeArray;
	set sixvar;
	array recodearr(6) var_1-var_6;
	do i=1 to 6;
	if recodearr(i) < 40 then recodearr(i)=.;
	end;
	run;

	proc print data=recodeArray; 
	var var_1-var_6;
	run;

	/* more easier ways with Arrays */

	data sixvar;
	infile '/home/u1421477/6var (2).txt';
	input var_1 var_2 var_3 var_4 var_5 var_6;
	run;

	data newvar;
	set sixvar;
	array ovar(6) var_1-var_6;
	array newtax(6) tax_1-tax_6;
	do i = 1 to 6; 
	newtax(i) = ovar(i) * 0.05 + ovar(i);
	end;
	run;

	proc print data=newvar; 
	var var_1-var_6 tax_1-tax_6;
	run;

[Home Page](https://github.com/JoeWadford/SAS-Complete-Tutorial)