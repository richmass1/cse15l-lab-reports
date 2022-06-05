# Lab Report 5, Week 10

Note: I got a lot of command line practice doing this one, because for some mysterious reason neither Remote Explorer via VSCode nor RDP via MobaXterm were working. (I literally have never had any problems with either of these before)

## Two test files where there were differences
I found the differences using vimdiff.

### 201.md
[which can be found here](https://github.com/nidhidhamnani/markdown-parser/blob/main/test-files/201.md)

![image of difference](/images/201md.png)

My output on the left, the downloaded program's output on the right. Using [dingus](https://spec.commonmark.org/dingus/) I have determined that my output (no link) is the correct one.
Here's the screenshot from dingus:

![dingus](/images/201expected.png)

The problem is that the downloaded version of MarkdownParse does not check what's in between the link text/title and the link itself. If there's stuff there, then there shouldn't be a link.

![code screenshot vim](/images/201fix.png)

For this if statement, another condition should be added, that checks the difference between closeBracket and openParen.

### 489.md
[which can be found here](https://github.com/nidhidhamnani/markdown-parser/blob/main/test-files/489.md)

![image of difference](/images/489md.png)

My output on the left, the downloaded program's output on the right. According to dingus my code in the wrong this time; there should be no link:

![expected](/images/489expected.png)

The problem is that it's not checking whether there is a newline character in the supposed link. If there is a newline, it shouldn't be considered a link.

![code screenshot2](/images/489fix.png)

It could be inserted into one of these if statements as a condition. (Really though, this whole part should be rewritten.)
