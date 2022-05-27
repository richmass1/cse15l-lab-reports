# Lab Report 4 - Week 8

[My markdown-parse repository](https://github.com/richmass1/markdown-parser)

[The other group's repository](https://github.com/anhthony/markdown-parser)

## Expected Output
To get the expected results for the snippets, I used [this interactive markdown renderer](https://spec.commonmark.org/dingus/) from commonmark.org, lovingly called "dingus".

According to Dingus, snippet 1 should produce only 1 link: `` `google.com``

Snippet 2 should produce 3:

- `a.com`
- `a.com(())`
- `example.com`

And snippet 3 should produce 1: `https://sites.google.com/eng.ucsd.edu/cse-15l-spring-2022/schedule`.


## Test code

![tests for the snippets](/images/snippet-tests.png)

These are the tests that I added to MarkdownParseTest.java.

## Test results

### My implementation

![JUnit results](/images/testresult-ourgroup.png)

All three of the new tests failed, but the second one was only missing a single parenthesis, so it was pretty close. The expected output is circled in red and the actual output is circled in blue.

### The other group's implementation

![JUnit results 2](/images/testresult-theirgroup.png)

All three new tests failed. The expected output is circled in red and the actual output is circled in blue.

## Thoughts on fixing the code

### Snippet 1

There is a way to fix the code to correctly parse snippet 1: before searching through the markdown for an open bracket, search for a backtick. If one is found, go to the next backtick and restart the search. I'm pretty sure this would take up fewer than 10 lines, but I don't know whether it would work for all possible cases.

### Snippet 2

This would require adding more than 10 lines. The backslash part is easy -- just ignore a close bracket if it has a backslash in front of it -- but parsing parentheses and brackets to match up all pairs and find where the link is supposed to end would be a bit more difficult, and in total, I doubt this could be accompished in 10 lines.

### Snippet 3

This could be done pretty simply. Scan through the title text and the link itself, and if either contains a new line character, don't add it.

## The last part

My code did not work for any of the new tests. However, it _almost_ worked for snippet 2, because my lab partner had suggested the possibility of parentheses being in the links, and so I put in this:
```
if(markdown.indexOf("(", openParen + 1) != -1 && markdown.indexOf("(", openParen + 1) < closeParen) {
                closeParen = markdown.indexOf(")", closeParen + 1);
            }
```
But this only works for non-nested pairs of parentheses, so the test still failed.
