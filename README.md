![](/images/capture.PNG)



# Table of Contents

### [Prerequisites][]

### [Register space][]

### [APIs][]

### [Example use cases][]

### [Tutorials][]

# Overview

This GitHub repository is being developed for TDL as a feasbility study to demonstrate markdown content creation, editing and publication of typical Xdocumentation in the GitHub environment.

The following figure shows a high level system representation. Component level descriptions are given in subsequent sections.

![](/images/image1.jpg)

# Basic Markdown: Content editing

## Adding Text

Just type to add plain text.

You can add emphasis as follows:

&nbsp;&nbsp;&nbsp;&nbsp;Apply *Italics*, using single asterisks or underscores either side of the target text.

&nbsp;&nbsp;&nbsp;&nbsp;Apply **Bold**, using double asterisks or underscores either side of the target text.

&nbsp;&nbsp;&nbsp;&nbsp;Apply ~~Strikethrough~~ using two tildes (\~~) either side of the target text.

### Indented Text
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Indents ARE possible but not native - use normal HTML tagging for this. (multiple \&nbsp;&nbsp;)

## Sections
Sections are typically created by inserting headings.
Headings are predeced by '#' symbols and take the following form:

\# Is a H1

\## Is a H2

\### Is a H3

## Tables

### Basics

Use outer pipes (|'s) to separate columns.

Use dashes (-'s) to separate rows.

There must be at least three dashes separating each header cell from body content.

### Alignment

Control cell horizontal alignment using colons. For example, in the following table:

Column 1 is left aligned

Column 2 is centered

Column 3 is right aligned

|Column 1 | Column 2 |Column 3|
|:------|:------:|-----:|
|Cell 1 | Cell 2| Cell 3|
|Cell 1 | Cell 2| Cell 3|
|Cell 1 | Cell 2| Cell 3|
|Cell 1 | Cell 2| Cell 3|


## Lists
#### Numbered
Just type 1, 2, 3 etc for numbered lists:
1. Keys
2. Phone
3. Wallet

#### Bulleted
For bulleted lists, precede each item with a dash:
- Apples
- Pears
- Oranges

## Code

Inline \`code\` has \`back-ticks\` around it.

Inline `code` has `back-ticks` around it.

Similarly, code blocks use triple back-ticks (\```) at the beginning and end of code blocks (back-ticks must be on separate lines).
```
/* Fibonacci Series C language */
#include<stdio.h>
 
int main()
{
   int n, first = 0, second = 1, next, c;
 
   printf("Enter the number of terms\n");
   scanf("%d",&n);
 
   printf("First %d terms of Fibonacci series are :-\n",n);
 
   for ( c = 0 ; c < n ; c++ )
   {
      if ( c <= 1 )
         next = c;
      else
      {
         next = first + second;
         first = second;
         second = next;
      }
      printf("%d\n",next);
   }
 
   return 0;
}
```


Support and Feedback

[Click for file][]

[Click for file]:file_2.md

[Prerequisites]:prerequisites.md

[Register space]:registers.md

[APIs]:apis.md

[Example use cases]:examples.md

[Tutorials]:tutorials.md

