# Postfix to Infix:
## Steps:






<img width="635" alt="Screenshot 2024-11-20 at 7 15 00 PM" src="https://github.com/user-attachments/assets/11bf006b-0317-48ae-8ee8-94401b7aab02">















## Java Code:
```
import java.util.Stack;

class PostfixToInfix {

    // Function to check if a character is an operator
    static boolean isOperator(char ch) {
        return ch == '+' || ch == '-' || ch == '*' || ch == '/' || ch == '^';
    }

    // Function to convert postfix to infix
    static String postfixToInfix(String postfix) {
        Stack<String> stack = new Stack<>();

        // Traverse the postfix expression
        for (int i = 0; i < postfix.length(); i++) {
            char c = postfix.charAt(i);

            // If the character is an operand, push it onto the stack
            if (Character.isLetterOrDigit(c)) {
                stack.push(Character.toString(c));
            }
            // If the character is an operator, pop two operands from the stack
            else if (isOperator(c)) {
                String operand2 = stack.pop();
                String operand1 = stack.pop();

                // Form the infix expression with parentheses
                String infix = "(" + operand1 + c + operand2 + ")";
                stack.push(infix);
            }
        }

        // The final element in the stack is the resulting infix expression
        return stack.pop();
    }

    // Main method to test the conversion
    public static void main(String[] args) {
        String postfix = "AB+C*D-";
        System.out.println("Postfix Expression: " + postfix);
        String infix = postfixToInfix(postfix);
        System.out.println("Infix Expression: " + infix);
    }
}

```
