# What is *gparm*?
*gparm* is a program for generating oodles of text-based input files for other
programs.  It facilitates development and management of parametric analyses.

The general use case is where you need to run a program---say, a simulation of
some kind---dozens, thousands, or even millions of times, using a variety of
inputs.

# Installing *gparm*

*gparm* is Perl script that comprises a single file.  Put it wherever you
want.  In Linux, it should probably go in a bin file somewhere (e.g.,
/usr/local/bin or ~me/bin).

# Running *gparm*

To do parametric analysis with *gparm*, create two files:  1) a template
file formatted in the proper syntax for your simulation program, but having
replaceable parameters in place of any real input values you want to vary,
and 2) a parameter file that holds all your input sets.  Then, combine the
two with *gparm*:

> `gparm -t my.template.file -p my.parmameter.file`

The parameter file is simply a CSV file holding a rectangular block of data,
one column per parameter, one row per run set.  The first row holds the
parameter names (as they're used in the template file).  E.g.,

> `ID, iterations, use_fastlib, start_value`  
> `1, 12, yes, 1`  
> `2, 12, yes, 10`  
> `3, 20, yes, 1`  
> `4, 20, yes, 10`  
> `5, 12, no, 1`  
> `6, 12, no, 10`  
> `7, 20, no, 1`  
> `8, 20, no, 10`  

In Linux it's easy to make a script file executable, so you generally only
have to name the file to run it, just like any other command, as long as
the script file is in a directory on your search path.  E.g.,

> `gparm -t myinput.tmpl -p myparameters.csv`

If you don't want to put it in a bin directory, just run it from wherever
you put it:

> `./gparm -t myinput.tmpl -p myparameters.csv`

> `/home/me/tools/gparm -t myinput.tmpl -p myparameters.csv`

In Windows, you'll have to name *gparm* as an argument to the *perl* command:

> `perl gparm -t myinput.tmpl -p myparameters.csv`
