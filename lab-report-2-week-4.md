# Lab Report 2 (week 4 - 4/24/2022)

This lab report will contain 3 changes that were made to the code of MarkdownParser.java in order to fix various bugs.

## Bug fix 1

![Bug fix 1](/images/bugfix1.JPG)

[Link to the test file which caused the failure](https://github.com/nidhidhamnani/markdown-parser/blob/main/test-file7.md)

![The error](/images/bugfix1error.JPG)

(The problem was that the program would not finish executing, in case it is not clear from the screenshot.)

What was happening is that because the file contained no close bracket, closeBracket would be set to -1. Instead of quitting as it should, it entered an infinite loop. The loop was programmed to only quit when currentIndex became greater than the length of the file or when openBracket was -1, but since there was an open parenthesis at index 0 and an open bracket at index 1, neither of these conditions were met.

## Bug fix 2

![Bug fix 2](/images/bugfix2.JPG)

[Link to the test file which caused the failure](https://github.com/nidhidhamnani/markdown-parser/blob/main/test-file8.md)

![Error 2](/images/bugfix2error.JPG)

There was a line of code that checked the index before the open bracket to ensure that there was no exclamation mark. When the open bracket was at index 0 in test file 8, this triggered a StringIndexOutOfBounds exception.

## Bug fix 3

![Bug fix 3](/images/bugfix3.JPG)

[Link to the test file which caused the failure](https://github.com/nidhidhamnani/markdown-parser/blob/main/test-file5.md)

![error 3](/images/bugfix3error.JPG)

The code did not take into account the number of characters in between the close bracket and the open parenthesis. When there are a bunch of characters in between, the link is not supposed to be added. Because it didn't check, it added the link from test file 5 anyways.
