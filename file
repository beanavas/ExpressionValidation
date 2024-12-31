#include <stdio.h>
#include <stdlib.h>
#include <ctype.h> 
#include <stdlib.h>
#include <string.h>
#define SIZE 100


struct stack {

    char items[SIZE];
    int top;

};

// Operators come after the operand

void initialize(struct stack* stackPtr);
int empty(struct stack* stackPtr);
char push(struct stack* stackPtr, char value);
char pop(struct stack* stackPtr);
char peek(struct stack *s);
int isOperator(char ch);
int priority(char ch);
char *infixToPostfix(char infix[]);
int checkBalance(char exp[]);
int isMatchingPair(char open, char close);

int main() {

    char infix[SIZE];

    printf("\nEnter Expression:");
    fgets(infix, SIZE, stdin);
    //size_t length = strlen(infix);

    char *postfix = infixToPostfix(infix);

    printf("\nYour input expression:");
    printf("%s", infix);


    printf("\nChecking balance...");
    if(checkBalance(infix)){

        printf("\nVALID");
        printf("\nThe postfix is: ");
        printf("%s\n", postfix);

    }else{

        printf("\nINVALID for )!!!\n");
    }


    
return 0;

}

void initialize(struct stack* stackPtr) {

    stackPtr->top = -1;

}

int empty(struct stack* stackPtr) {

    return (stackPtr->top == -1);

}

char push(struct stack* stackPtr, char value) {

    // Add value to the top of the stack and adjust the value of the top.
    stackPtr->items[stackPtr->top+1] = value;
    (stackPtr->top)++;

return 1;

}

char pop(struct stack* stackPtr) {

    char retval;
    // Check the case that the stack is empty.
    if (empty(stackPtr)) return '\0';

    // Retrieve the item from the top of the stack, adjust the top and return
    // the item.
    retval = stackPtr->items[stackPtr->top];
    (stackPtr->top)--;

return retval;

}

char peek(struct stack *s){

    if(empty(s)) return '\0';

    return s->items[s->top];

}

int isOperator(char ch){

    return(ch =='+' || ch =='-' || ch == '*' || ch == '/' || ch == '^');

}

int priority(char ch){

    if(ch=='+' || ch=='-'){

        return 1; //low priority

    }else if(ch =='*' || ch == '/'){

        return 2; //mid priority

    }else if(ch =='^'){
        
        return 3;
    }

    return 0; //for non-operators
}

char *infixToPostfix(char infix[]){

    struct stack s;
    initialize(&s);
    char *postfix = malloc(sizeof(char)*SIZE);
    int j =0;


    //now we run through every character
    for(int i=0; i<strlen(infix); i++){

        char ch = infix[i];

        //if its a number, we add it to postfix!
        if(isdigit(ch)) {
            postfix[j++] = ch;


        //if its an operator, we push it to the stack    
        }else if(ch == '('){

            push(&s, ch);

        }else if(ch==')'){
        
            while(!empty(&s) && peek(&s) != '('){

                postfix[j++] = pop(&s);

            }

            pop(&s);

        }else if(isOperator(ch)){

            while(!empty(&s) && priority(peek(&s)) >= priority(ch)){
                postfix[j++] = pop(&s);

            }

            push(&s,ch);
        }

    }

    while(!empty(&s)){

        postfix[j++] = pop(&s);

    }

    postfix[j] = '\0';
    return postfix;


}

int checkBalance(char exp[]){

    struct stack s;
    initialize(&s);

    for(int i=0; i<strlen(exp); i++){
        char current = exp[i];

        if(current == '(' || current == '{' || current == '['){

            push(&s,current);

        }else if (current == ')' || current == '}' || current == ']'){

            if(empty(&s)) return 0; //inbalanced

            //checks if there is a matching pair coming up next, if not its unbalanced
            char top = pop(&s);
            if(!isMatchingPair(top, current)) return 0;

        }

    }

    if(!empty(&s)) return 0;

    return 1;
}

int isMatchingPair(char open, char close){
    return(
        (open =='(' && close==')') ||
        (open =='{' && close=='}') ||
        (open =='[' && close==']')
    );
}

