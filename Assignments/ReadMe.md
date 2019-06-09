# SAS Complete Tutorial | Udemy | SAS Functions

[Home Page](https://github.com/JoeWadford/SAS-Complete-Tutorial)

## SAS Ninja Assignment 1

	data national;
	infile '/home/u1421477/MPI_national (1).csv' DSD MISSOVER FIRSTOBS=2; 
	length Country$42;
	input ISO$ Country$ MPI_Urban Headcount_Ratio_Urban Intensity_of_Deprivation_Urban MPI_Rural Headcount_Ratio_Rural Intensity_of_Deprivation_Rural;
	/* I should have considered editing the longer columns using abbreviations */
	MPI_diff = MPI_Urban - MPI_Rural;
	if Country='Nigeria' then 
	do;
	ISO = 'NGA';
	end;
	separator = ',';
	together = catx(separator, Country, ISO);
	drop separator;
	run;

	proc contents data=national;
	run;

	proc print data=national(where=(Intensity_of_Deprivation_Rural>=40.0));
	run;

	/* if you need to create a subsetted dataset with IDR >= 40 */
	data nationalIDR;
	set national;
	if Intensity_of_Deprivation_Rural>=40;
	run;

## SAS Ninja Assignment 2

	data assignment2solution;
	infile '/home/u1421477/Current_Employee_Names__Salaries__and_Position_Titles (2).csv' DSD MISSOVER Firstobs=2;
	length Name$35 JobTitles$60 Dep$20 FULLorPART$14 SALorHR$10 TypicalH 3 AnnualS$ 20 HourlyR$ 25;
	input Name$ JobTitles$ Dep$ FULLorPART$ SALorHR$ TypicalH AnnualS$ HourlyR$;
	annualSAL = input(compress(annuals,'$'), comma11.);
	hourlyRate = input(compress(hourlyr,'$'), comma9.);

	SALorHourly = coalesce(annualSAL,hourlyRate);
	run;

	proc contents data=assignment2solution; run;

	proc print data=assignment2solution(where=(hourlyRate > 50));
	var Name hourlyRate;
	format hourlyRate dollar11.2;
	run;

[Home Page](https://github.com/JoeWadford/SAS-Complete-Tutorial)