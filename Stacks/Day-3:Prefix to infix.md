# Prefix to infix :

## video-explanation:
https://www.youtube.com/watch?v=4pIc9UBHJtk (🕓 35:40) onwards

## Algorithm:
Read the Prefix expression in reverse order (from right to left)
If the symbol is an operand, then push it onto the Stack
If the symbol is an operator, then pop two operands from the Stack 
Create a string by concatenating the two operands and the operator between them. 
string = (operand1 + operator + operand2) 
And push the resultant string back to Stack
Repeat the above steps until the end of Prefix expression.
At the end stack will have only 1 string i.e resultant string
## JAVA CODE:
```
import java.util.Stack;

public class PrefixToInfix {

    // Method to check if a character is an operator
    private static boolean isOperator(char c) {
        return c == '+' || c == '-' || c == '*' || c == '/';
    }

    // Method to convert prefix to infix
    public static String convertPrefixToInfix(String prefix) {
        Stack<String> stack = new Stack<>();

        // Read the prefix expression in reverse order (right to left)
        for (int i = prefix.length() - 1; i >= 0; i--) {
            char symbol = prefix.charAt(i);

            // If the symbol is an operand, push it onto the stack
            if (Character.isLetterOrDigit(symbol)) {
                stack.push(String.valueOf(symbol));
            } 
            // If the symbol is an operator
            else if (isOperator(symbol)) {
                // Pop two operands from the stack
                String operand1 = stack.pop();
                String operand2 = stack.pop();

                // Create the infix string: (operand1 operator operand2)
                String infix = "(" + operand1 + symbol + operand2 + ")";

                // Push the resultant string back to the stack
                stack.push(infix);
            }
        }

        // The final infix expression is the only element in the stack
        return stack.pop();
    }

    public static void main(String[] args) {
        String prefix = "*+AB-CD";
        String infix = convertPrefixToInfix(prefix);
        System.out.println("Prefix: " + prefix);
        System.out.println("Infix: " + infix);
    }
}

```
Time Complexity: $$O(n)$$
Space Complexity: $$O(n^2)$$
