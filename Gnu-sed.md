## GNU SED

Sed is a stream editor. By default, multiple files would be regarded as one stream, unless specify it explicitly by '-s' option to treat them separately. Data based on lines and matched areas which have been selected by commands, instructions or regular expressions would be called RANGE or ADDRESS. Then they could be manipulated by commands, instructions or regular expressions following RANGE. Those commands, instruction or regular expressions sets could be separated by ';', '\n' or '-e' options.  It's a good idea to examine those sets with '--debug' option.

```
Syntex:

    sed OPTION SCRIPT INPUTFILE...
```

By default, sed will displays all lines from input with the specified lines following the original lines repectively to the standard output, except with the -d option to be modified or deleted.

```
 
sed -n 's/hello/world/' input.txt
                        < input.txt
                                    >output.txt
sed -n ...                                   

SCRIPT: '[RANGE] [INSTRUCTION] [/PATTERN/] [REPLACEMENT/] [INSTRUCTION]'
	
SCRIPT: 'scripts ; scripts' == -e 'scripts' -e 'scripts'
        -e 'scripts' -f script-file
```

RANGE

```
number(s) separated by `,` or `~`.
2	/* Pick the second line.
1,3	/* Pick the 1-3 lines.
1~2	/* Pick the first line and subsequent lines in increment of 2.
0~2	/* Pick even-numbered lines.
1~2!	/* Same as above. `!` char means reversing the selection.

/regexp		/* or even a regexp matching.
```

INSTRUCTION

```
d		/* Delete.
c TEXT		/* Replace lines with TEXT. 
i TEXT		/* Insert.
a TEXT	 	/* Append.

Note: c, i, a instructions are Gnu extension.

p		/* Print.

q[number]	/* Terminate with a specified exit status number.

/* Substitute the matching, by default only the first.
s/REGEXP/REPLACEMENT/[FLAGS]

FLAGES:

g		/* Apply to all matches on a line.
Number		/* Only apply to the Numberth match.
I		/* Match in case-insensitive.
```

OPTIONS

```
-n,
--quiet,
--silent	/* Only display the processed line(s).

/* specify the expression, mutiple -e may be used. If only one, then it could be omitted.
-e SCRIPT
--expression=SCRIPT

-i[SUFFIX]
--in-place[=SUFFIX]	/* Edit files in-place. If provide a suffix, then produces a backup file.

-f SCRIPT-FILE
--file=SCRIPT-FILE	/* read SCRIPT from file.

/* Print the input sed program in canonial form, and show how the comands were processed by it.
--debug

``` 

EXAMPLES


```
/* Delete the second imput line.
$ seq 3 | sed 2d
1
3

/* Print the 2nd line.
$ seq 3 | sed 2p
1
2
2
3

/* Print only the 2nd line.
$ seq 3 | sed -n 2p
2

/* Replace the 2nd line.
$ seq 3 | sed '2c here!'
1
here!
3

/* Append TEXT after a line.
$ seq 3 | sed '2a here!'
1
2
here!
3

/* Different form from above.
$ seq 3 | sed '2a\
here!' 
1
2
here!
3

/* Same as appending but in different way.
$ seq 3 | sed '2s/2/&\nhere!/'
1
2
here!
3

Note: match 2nd line; & char means the original. 

/* Same as above, just show another structure.
$ seq 3 | sed '/2/s/2/&\nhere!/'

/* Different methods, g means substitute all matches in a line.
$ seq 3 | paste -d, - <(seq 3) | sed -n -e '1s/1/2/p' -e '3s/3/1/gp'
$ seq 3 | paste -d, - <(seq 3) | sed -n '1s/1/2/p ; 3s/3/1/gp'
$ seq 3 | paste -d, - <(seq 3) | sed -n '1s/1/2/p\
3s/3/1/gp'
2,1
1,1

```
