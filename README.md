# What is *gparm*?
*gparm* is a program for generating oodles of text-based input files for other
programs.  It facilitates development and management of parametric analyses.

The general use case is where you need to run a program---say, a simulation of
some kind---dozens, thousands, or even millions of times, using a variety of
inputs.

# Installing *gparm*

*gparm* is Perl script embodied in a single file.  Put it wherever you
want.  In Linux, it should probably go in a bin file somewhere (e.g.,
/usr/local/bin or $HOME/bin).

You will need a working Perl 5 interpreter on your machine, and may need to
add two modules that are sometimes not part of the base Perl installation:

* Text::Template
* Parallel::ForkManager

In Linux it's easy to make a script file executable, so you generally only
have to name the file to run it, just like any other command, as long as
the script file is in a directory on your search path.  E.g.,

> `gparm [arguments...]`

If you don't want to put it in a bin directory, just run it from wherever
you put it.  E.g.,

> `./gparm [arguments...]`

or

> `$HOME/tools/gparm [arguments...]`

In Windows, you'll have to name *gparm* as an argument to the *perl* command:

> `perl gparm [arguments...]`

# Using *gparm*

To do parametric analysis with *gparm*, create two files:  1) a template
file formatted in the proper syntax for your simulation program, but having
replaceable parameters in place of any real input values you want to vary,
and 2) a parameter file that holds all your input sets.  Then, combine the
two with *gparm*:

> `gparm -t my.template.file -p my.parmameter.file`

The template file is simply a text file in the format required by your software,
with specific inputs replaced by special tags using replaceable parameters.
For example (completely contrived):

> `set iterations       {$iterations}`  
> `set use_fast_library {$use_fastlib}`  
> `set initial_estimate {$start_value <= 0 ? 1.0 : $start_value}`  

The tags inside the curlies {} are simply snippets of Perl code that may contain
nothing more than the name of a scalar variable or may contain programmed logic
of arbitrary complexity.  The values in the variables get defined by the parameter file.

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

# Additional Capabilities

The *gparm* user manual covers many other topics and describes *gparm*'s capabilities
in detail:

* Changing snippet delimiters from {} to other characters
* Assigning default parameter values in templates
* Control over generated filenames
* Automatic compression of generated files
* Breaking up templates into multiple files
* Multiprocessing for speed on multicore computers
* Use of persistent storage to accommodate large datasets in templates
* Use of special (non-parameter) variables inside templates
* Availability of Perl functions in templates
* Error messages and debugging of templates
