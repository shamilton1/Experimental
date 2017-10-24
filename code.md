

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

## Images
**Important**: Images should always be inserted using a relative path.

Repositories requiring images should each have a separate and unique image folder.

Use the following construction to insert images:

```
![](/images/<image1.jpg>)
```
