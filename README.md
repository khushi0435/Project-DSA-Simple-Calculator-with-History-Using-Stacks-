#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#define MAX 100
typedef struct {
   char history[MAX][100];
   int top;
} Stack;
void push(Stack *s, char *entry) {
   if (s->top == MAX - 1) {
       printf("History stack is full!'n");
   } else {
       s->top++;
       strcpy(s->history[s->top], entry);
   }
}
void displayHistory(Stack *s) {
   if (s->top == -1) {
       printf("No calculation history.'n");
   } else {
       printf("'n--- Calculation History ---'n");
       for (int i = s->top; i >= 0; i--) {
           printf("%s'n", s->history[i]);
       }
   }
}
void clearHistory(Stack *s) {
   s->top = -1;
   printf("History cleared.'n");
}

int main() {
   Stack s;
   s.top = -1;

   int choice;
   float num1, num2, result;
   char op;
   char record[100];

   do {
       printf("'n--- Simple Calculator with History ---'n");
       printf("1. Perform Calculation'n");
       printf("2. View History'n");
       printf("3. Clear History'n");
       printf("4. Exit'n");
       printf("Enter your choice: ");
       scanf("%d", &choice);

       switch (choice) {
       case 1:
           printf("Enter first number: ");
           scanf("%f", &num1);
           printf("Enter operator (+, -, *, /): ");
           scanf(" %c", &op);
           printf("Enter second number: ");
           scanf("%f", &num2);

           switch (op) {
           case '+':
               result = num1 + num2;
               printf("Result: %.2f'n", result);
               break;
           case '-':
               result = num1 - num2;
               printf("Result: %.2f'n", result);
               break;
           case '*':
               result = num1 * num2;
               printf("Result: %.2f'n", result);
               break;
           case '/':
               if (num2 != 0) {
                   result = num1 / num2;
                   printf("Result: %.2f'n", result);
               } else {
                   printf("Error: Division by zero!'n");
                   continue;
               }
               break;
           default:
               printf("Invalid operator!'n");
               continue;
           }
           snprintf(record, sizeof(record), "%.2f %c %.2f = %.2f", num1, op, num2, result);
           push(&s, record);
           break;
       case 2:
           displayHistory(&s);
           break;
       case 3:
           clearHistory(&s);
           break;
       case 4:
           printf("Exiting calculator. Goodbye!'n");
           break;
       default:
           printf("Invalid choice!'n");
       }
   } while (choice != 4);
   return 0;
}
