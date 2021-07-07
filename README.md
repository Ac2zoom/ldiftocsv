## Converting LDIF/LDAP data into a CSV file

### LDIF to CSV

#### This fork specifically supports Python 2

I work with LDAP on a regularly basis. I frequently have to pull data using ldapsearch. While the data that ldapsearch 
spits out is a decent representation sometimes I want something a bit easier to work with.

The format I use most tends to be CSV. While the acronym stands for comma separated value the format may be used to 
describe data that is printed out line by line and separated by anything you can imagine.

The problem for me is finding a decent LDIF to CSV converter. The ones that I have tried tend to choke on any number of 
issues. Some of these include binary data or failing to normalize the multivalued attributes.

I finally got sick enough of these issues that I decided to write my own.

### Usage

Running "python LDIFtoCSV.py" should give you the usage text.
```
usage: LDIFtoCSV.py [options] 

-o <filename> : File to write output. By default this is set to sys.stdout
-l <filename> : File to write logging output. By default there is no logging.
-F <char> : Character to separate the fields by. By default this is a comma. i.e. -F","
-D <char> : Character to delimit the text value by. By default this is a double quote. i.e. -D"""
-M <num> : The maximum number of columns a multivalued attribute should take up (default: 5). This is common with the objectClass attribute where it can have over 20 values. Do you want to have 20 columns each with the same heading objectClass or do you want to limit it.
```

Here are some common command lines that I use (assuming you have a test.ldif):

Outputs the CSV straight to standard output:

```
python LDIFtoCSV.py test.ldif
```

Outputs CSV to standard output with semicolons as the delimiter:

```
python LDIFtoCSV.py -F";" test.ldif
```

Outputs CSV to standard output with pipes as the delimiter and text surrounded by carrots:

```
python LDIFtoCSV.py -F"|" -D"^" test.ldif
```
