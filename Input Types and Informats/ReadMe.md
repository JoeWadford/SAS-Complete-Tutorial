# SAS Complete Tutorial | Udemy | Input Types and Informats

[Home Page](https://github.com/JoeWadford/SAS-Complete-Tutorial)

## List Input

	/* just your standard input.  has its issues*/
	data sales1;
	input Name$ Sales_1-Sales_4;
	CARDS;
	Greg 10 2 40 0
	John 15 5 10 100
	Lisa 50 10 15 50
	Mark 20 0 5 20
	; run;	

## Column Input

	/* the lack of space between greg and 4 isn't an issue because we defined column Name*/
	data sales1;
	input Name$1-4 Sales_1-Sales_4 @5;
	CARDS;
	Greg10 2 40 0
	John 15 5 10 100
	Lisa 50 10 15 50
	Mark 20 0 5 20
	; run;

## Formatted Input and Informats

	/* review of length.  when all letters aren't showing up, this can be solved with a length statement*/
	data police1; 
	infile '/home/u1421477/londonoutcomes.csv' DSD MISSOVER FIRSTOBS=2;
	length CrimeID $25 ReportedF $25 FallsW $25 Longitude 4 Latitude 4 Location $25 LSOAC $25 LSOAN $25 OutcomeT $25;
	input CrimeID$ ReportedF$ FallsW$ Longitude Latitude Location$ LSOAC$ LSOAN$ OutcomeT$;
	run;

	/*Input BirthDate MMDDYY10.;*/

	data policeIssue; 
	infile '/home/u1421477/londonoutcomes.csv' DSD MISSOVER FIRSTOBS=2;
	input CrimeID$ ReportedF$ FallsW$ Longitude Latitude Location$ LSOAC$ LSOAN$ OutcomeT$;
	run;

	proc print data=police1 data=policeIssue; run;

	proc print data=policeIssue; run;

	/* informatting will be discussed in more detail in the next lecture.  use the following link for more info */
	[Proc Format](https://support.sas.com/content/dam/SAS/support/en/books/the-power-of-proc-format/59498-excerpt.pdf)

## User Defined Formats

	data disease;
	input diagcode$;
	datalines;
	001
	290
	800
	;
	run;

	proc print data=disease;
	run;

	proc format;
	value $codetwo
	'001' = 'Malaria'
	'290' = 'Social Anxiety Disorder'
	'800' = 'Leg Injury';
	run;

	proc print data=disease;
	format diagcode $codetwo.;
	run;

	data diseasereal;
	set disease;
	put
	diagdesc=put(diagcode,$codetwo.);
	run;

	proc print data=diseasereal;
	run;

[Home Page](https://github.com/JoeWadford/SAS-Complete-Tutorial)