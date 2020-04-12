# Dictionary Concatinator - A simple tool for concatenating dictionaries.
This program takes contents of specifically `'.txt'` dictionary files, and removes duplicates from the output.<br>

Text files are read using `utf_8` file encoding, with `errors='ignore'` on UTF-8 Decoding errors.<br>

An install script is not necessary as it is interpreted with bash, but may be placed in a place like `~/.local/bin` for ease of use.

## Example ending output
```
... more output above ...
Sun Apr 12 14:34:14 2020 Processing 67081369 words...
Sun Apr 12 14:34:47 2020 Processed 16113959 unique words...
Sun Apr 12 14:34:49 2020 Wrote 16113959 unique words to the-final-test.txt...
```

## Usage and help banner
```
usage: dictconcat [-h] [-f <include_file>] [-d <search_directory>] [-a]
                  <dictionary_path>

positional arguments:
  <dictionary_path>

optional arguments:
  -h, --help            show this help message and exit
  -f <include_file>     File read into <dictionary_path>
  -d <search_directory>
                        Directory to search. Default depth is infinite
  -a, --append          Append results to <dictionary_path>, if -a is not
                        specified <dictionary_path> will be truncated.
```
## Usage examples
**Help**
```bash
# Displays help
$ dictconcat -h 
```
**Fresh dictionary from a directory**
```bash
# Creates dictionary_file.txt if it does not exist 
# If dictionary_file.txt does exist, it is truncated
$ dictconcat -d /path/to/dictionaries/dir/ dictionary_file.txt
```
**Append to dictionary with a directory**
```bash
# Appends contents of -d to dictionary_file.txt
$ dictconcat -d /path/to/dictionaries/dir -a dictionary_file.txt
```
**Append a file to a dictionary**
```bash
# Append dictionary_file.txt to accumulating_dictionary_file.txt
$ dictconcat -f dictionary_file.txt -a accumulating_dictionary_file.txt
```
**Append directory files and another file to a directory**
```bash
# Append contents from -d and -f to dictionary_file.txt
$ dictconcat -d /path/to/dictionaries/dir/ -f this-file-too.txt -a dictionary_file.txt
```


## How the files are read
Ideally, the selected dictionary word will be the furthest to the end of the line. So if the text says `"the quick brown fox"` the selected word will be `"fox"`<br>

**Indexed file**
```bash
# abc, abc1, abcd1... will be chosen
    0   abc 
    1   abc1
    2   abcd
    3   abcd1
    ...
```
**Plain dictionary file**
```bash
# abc, abc1, abcd1... will be chosen
abc
abc1
abcd
abcd1
```
