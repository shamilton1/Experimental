![](/images/x_banner.PNG)

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

### Syntax Highlighting

You can add an optional language identifier to enable syntax highlighting in your fenced code block.

For example, to syntax highlight the following as Ruby code:

```
require 'redcarpet'
markdown = Redcarpet.new("Hello World!")
puts markdown.to_html
```
Simply add 'Ruby' after the initial ```

\```ruby
require 'redcarpet'
markdown = Redcarpet.new("Hello World!")
puts markdown.to_html
```

