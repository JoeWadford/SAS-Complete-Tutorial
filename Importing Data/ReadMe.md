# SAS Complete Tutorial | Udemy | Importing Data

[Home Page](https://github.com/JoeWadford/SAS-Complete-Tutorial)

## Importing CSV Files

	data weightgain;
	infile "/home/u1421477/weightgain (2).csv" DSD MISSOVER Firstobs=2;
	input id source$ type$ weightg;
	run;

## Importing SPSS Files

	proc import datafile="/home/u1421477/p054 (2).sav" out=p054;
	proc contents data=p054;
	run;

## Importing Txt Files

	data salary;
	infile '/home/u1421477/salary (2).txt';
	input year salary;
	run;

## Importing XLSX Files

	proc import out=salesdata DATAFILE="/home/u1421477/Sample-Sales-Data (3).xlsx" DBMS=XLSX;
	/* if you have multiple sheet use: sheet="a";*/
	/* if you don't have sheet names use: getnames=no as getnames=yes is the default*/
	run;

	proc print data=salesdata; run;

## Save Datasets Permanently 

	libname mylib '/home/u1421477'; 

	data mylib.houseprice; 
	run;

[Home Page](https://github.com/JoeWadford/SAS-Complete-Tutorial)