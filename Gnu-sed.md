## GNU SED

Sed is a stream editor. Multiple files would be regarded as one stream.

```
Syntex:

    sed OPTION SCRIPT INPUTFILE...
```

By default, sed displays all lines of contents with the processed lines following the original lines separately from input to the standard output, except with the -d option to be modified or deleted.

```
sed -n 's/hello/world/' input.txt
                        < input.txt
                                    >output.txt
[echo 8 |] sed -n ...                                   


    options

	'[RANGE] [INSTRUCTION] [/PATTERN/] [REPLACEMENT/] [INSTRUCTION]'
	

RANGE

number(s) separated by `,` or `~`.
2	/* Pick the second line.
1,3	/* Pick the 1-3 lines.
1~3	/* Pick the first line and subsequent lines in multiples of 3.
        /regexp/		/* or even a regex matching.

INSTRUCTION

d		/* Delete.
c TEXT		/* Replace lines with TEXT. 
i TEXT		/* Insert.
a addition 	/* Append.

Note: c, i, a instructions are Gnu extension.
 with the first line as the start point.
/* Substitute the matching.
s/REGEXP/REPLACEMENT/[FLAGS]

p		/* Print.

q[number]	/* Terminate with a specified exit status number.


OPTIONS

-n,
--quiet,
--silent	/* Only display the processed line(s).

/* specify the expression, mutiple -e may be used. If only one, then it could be omitted.
-e SCRIPT
--expression=SCRIPT

-i[SUFFIX]
--in-place[=SUFFIX]	/* Edit files in-place. If provide a suffix, then produces a backfile.

-f SCRIPT-FILE
--file=SCRIPT-FILE

/* Print the input sed program in canonial form, and show how the comands were processed by it.
--debug

``` with the first line as the start point.
