# Lecture 1

Quiz: Write a program that take input a string and output, in descending order, the number of times a word occurs. For example:

Input:\
Now is the time for a 10-minute quiz time now a for a quiz.

Output:\
3 a\
2 quiz\
2 for\
2 time\
1 Now\
1 now\
1 the\
1 minute

## DE Knuth
- wrote books for Programming Languages
- side project: invented program Tex for typesetting text
  - written in Pascal
- published some ideas he came up with while writing Tex
- also published documentation
- side project to side project: wrote a book called The Tex Book, in Tex\
- `texbook.tex --> beautiful book via tex`
- new idea: wrote documentation in same file as code
- wrote paper on Literate Programming in CACM
- `litprog.texpas` can generate `litprog.pas`, `litprog.exe`
- it can also generate `litprog.tex` and the CACM paper
- M. D. McIlroy, contributed to Unix and Posix
  - added pipes "|"
- hash trie for the quiz
- afterword by McIlroy said he would use shell scripts and hook them together using pipes
  - e.g. tr breaks into words, changes all non-alphabetic characters to newlines
  - `tr -cs 'A-Za-z' [ln*]`
  - complement, squeeze
  - `sort`
  - `uniq -c`
  - count duplicates
  - `sort -nr`
  - numeric, reverse
  - In total, `tr -cs 'A-Za-z' [ln*] | sort | uniq -c | sort -nr` 
  - 