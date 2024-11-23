# Prefix to Postfix
## Video-Explanation:
https://www.youtube.com/watch?v=4pIc9UBHJtk

## Algorithm:
Read the Prefix expression in reverse order (from right to left)
If the symbol is an operand, then push it onto the Stack
If the symbol is an operator, then pop two operands from the Stack 
Create a string by concatenating the two operands and the operator after them. 
string = operand1 + operand2 + operator 
And push the resultant string back to Stack
Repeat the above steps until end of Prefix expression.

## Examples:
<img width="580" alt="Screenshot 2024-11-23 at 12 38 43 PM" src="https://github.com/user-attachments/assets/8fde56a4-f794-42a6-885b-c95e6bc0bc1f">

### JAVA CODE:
```
import java.util.Stack;

public class PrefixToPostfix {

    // Method to check if a character is an operator
    private static boolean isOperator(char c) {
        return c == '+' || c == '-' || c == '*' || c == '/';
    }

    // Method to convert prefix to postfix
    public static String convertPrefixToPostfix(String prefix) {
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

                // Create the postfix string: operand1 + operand2 + operator
                String postfix = operand1 + operand2 + symbol;

                // Push the resultant string back to the stack
                stack.push(postfix);
            }
        }

        // The final postfix expression is the only element in the stack
        return stack.pop();
    }

    public static void main(String[] args) {
        String prefix = "*+AB-CD";
        String postfix = convertPrefixToPostfix(prefix);
        System.out.println("Prefix: " + prefix);
        System.out.println("Postfix: " + postfix);
    }
}
```
Time-complexity: $$O(n)$$
Space Complexity : $$O(n^2)$$ WorstCase




```
