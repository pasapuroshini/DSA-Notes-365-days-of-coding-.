
# Steps:


<img width="620" alt="Screenshot 2024-11-20 at 6 55 33 PM" src="https://github.com/user-attachments/assets/8c6f0728-daf1-4380-85d8-d0d7707ee5e1">




# A slight difference in infixtopostfix !!!!:Remember
 ## original : infix to postfix
```
while (!stack.isEmpty() && getPrecedence(c) <= getPrecedence(stack.peek())) {
    result.append(stack.pop());
}
```
## infix to prefix (via postfix)
```while (!stack.isEmpty() && 
      (getPrecedence(c) < getPrecedence(stack.peek()) || 
      (getPrecedence(c) == getPrecedence(stack.peek()) && c != '^'))) {
    result.append(stack.pop());
}
```
if the operator( not ^) has same precedence just push it into stack without popping out top.
if the operator is ^ , then push into stack with poppping out top from stack.

Java Code:
```
import java.util.Stack;

class InfixToPrefix {

    // A utility function to return precedence of a given operator
    static int getPrecedence(char ch) {
        switch (ch) {
            case '+':
            case '-':
                return 1;
            case '*':
            case '/':
                return 2;
            case '^':
                return 3;
        }
        return -1; // Invalid character
    }

    // A utility function to check if a character is an operator
    static boolean isOperator(char ch) {
        return ch == '+' || ch == '-' || ch == '*' || ch == '/' || ch == '^';
    }

    // Function to reverse a string and swap '(' with ')'
    static String reverse(String exp) {
        StringBuilder reversed = new StringBuilder();
        for (int i = exp.length() - 1; i >= 0; i--) {
            char ch = exp.charAt(i);
            if (ch == '(') {
                reversed.append(')');
            } else if (ch == ')') {
                reversed.append('(');
            } else {
                reversed.append(ch);
            }
        }
        return reversed.toString();
    }

    // Function to convert infix expression to prefix
    static String infixToPrefix(String infix) {
        // Step 1: Reverse the infix expression
        String reversedInfix = reverse(infix);

        // Step 2: Convert reversed infix to postfix
        String postfix = infixToPostfix(reversedInfix);

        // Step 3: Reverse the postfix expression to get prefix
        return reverse(postfix);
    }

    // Function to convert infix to postfix (used in prefix conversion)
    static String infixToPostfix(String infix) {
        StringBuilder result = new StringBuilder();
        Stack<Character> stack = new Stack<>();

        for (int i = 0; i < infix.length(); i++) {
            char c = infix.charAt(i);

            // If the character is an operand, add it to the result
            if (Character.isLetterOrDigit(c)) {
                result.append(c);
            }
            // If the character is '(', push it onto the stack
            else if (c == '(') {
                stack.push(c);
            }
            // If the character is ')', pop until '(' is encountered
            else if (c == ')') {
                while (!stack.isEmpty() && stack.peek() != '(') {
                    result.append(stack.pop());
                }
                stack.pop(); // Remove '(' from the stack
            }
            // If the character is an operator
            else if (isOperator(c)) {
                while (!stack.isEmpty() &&
                        (getPrecedence(c) < getPrecedence(stack.peek()) ||
                        (getPrecedence(c) == getPrecedence(stack.peek()) && c != '^'))) {
                    result.append(stack.pop());
                }
                stack.push(c);
            }
        }

        // Pop all remaining operators from the stack
        while (!stack.isEmpty()) {
            result.append(stack.pop());
        }
        return result.toString();
    }

    // Main method to test the conversion
    public static void main(String[] args) {
        String infix = "(A+B)*(C-D)";
        System.out.println("Infix Expression: " + infix);
        String prefix = infixToPrefix(infix);
        System.out.println("Prefix Expression: " + prefix);
    }
}

```
Output:

Infix expression: (p+q)*(c-d)
Prefix Expression: *+pq-cd

Time Complexity: O(N)

Space Complexity: O(N)
