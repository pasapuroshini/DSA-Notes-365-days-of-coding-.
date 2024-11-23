# Postfix to Prefix  Conversion -Code in Java
## Video link:

Video Explanation:https://www.youtube.com/watch?v=4pIc9UBHJtk ( 39:58 sec onwards)

## Dry run:
<img width="492" alt="Screenshot 2024-11-23 at 12 12 11 PM" src="https://github.com/user-attachments/assets/c739e143-35c3-4e72-b96e-9e0da3624871">


## Example:

<img width="586" alt="Screenshot 2024-11-23 at 12 22 12 PM" src="https://github.com/user-attachments/assets/da73b459-81d9-4018-803e-6c1ec0b304a6">

## Algorithm:
1.Read the Postfix expression from left to right
2.If the symbol is an operand, then push it onto the Stack
3.If the symbol is an operator, then pop two operands from the Stack 
 Operand1= 1st popped 
 Operand2= 2nd popped
4.Create a string by concatenating the two operands and the operator before them. 
5.string = operator + operand2 + operand1 
6. push the resultant string back to Stack
7.Repeat the above steps until end of Postfix expression.

## JAVA CODE:
```
import java.util.Stack;

public class PostfixToPrefix {
    // Method to check if a character is an operator
    private static boolean isOperator(char c) {
        return c == '+' || c == '-' || c == '*' || c == '/';
    }

    // Method to convert postfix to prefix
    public static String convertPostfixToPrefix(String postfix) {
        Stack<String> stack = new Stack<>();

        // Read the postfix expression from left to right
        for (int i = 0; i < postfix.length(); i++) {
            char symbol = postfix.charAt(i);

            // If the symbol is an operand, push it onto the stack
            if (Character.isLetterOrDigit(symbol)) {
                stack.push(String.valueOf(symbol));
            } 
            // If the symbol is an operator
            else if (isOperator(symbol)) {
                // Pop two operands from the stack
                String operand1 = stack.pop();
                String operand2 = stack.pop();

                // Create the string for the prefix expression
                String prefix = symbol + operand2 + operand1;

                // Push the resultant string back to the stack
                stack.push(prefix);
            }
        }

        // The final prefix expression is the only element in the stack
        return stack.pop();
    }

    public static void main(String[] args) {
        String postfix = "AB+C*";
        String prefix = convertPostfixToPrefix(postfix);
        System.out.println("Postfix: " + postfix);
        System.out.println("Prefix: " + prefix);
    }
}
```
## Time and Space complexities
Time complexity : $$O(n)$$
Space complexity; $$O(n^2)$$ in worst case

