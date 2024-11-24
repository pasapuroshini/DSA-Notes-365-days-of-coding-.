# Given an infix expression, Your task is to convert the given infix expression to a postfix expression.

Infix Expression: <operand><operator><operand>.

Postfix Expression: <operand><operand><operator>.

## Steps:

1.Initialize Stack and Result:

2.Use a Stack to store operators and parentheses.

3.Use a StringBuilder (result) to build the postfix expression.

4.Traverse the Infix Expression:
  If Operand:
    Append directly to result.
    (e.g., A, B, 1)
  If (:
    Push to the stack.
    (Marks the start of a subexpression.)


  If ):
    Pop and append operators from the stack until ( is encountered.
    Discard the (.

  If Operator (+, -, *, /, ^):

    Pop and append all operators from the stack with higher or equal precedence.
    Push the current operator onto the stack.
5.After Traversing:
   Pop and append all remaining operators in the stack to result.
  (Ensure no unmatched ( remains.)
6.Return the Postfix Expression:
7.The final result contains the postfix expression.


``` Java
import java.util.Stack;

class TUF {

  // A utility function to return
  // precedence of a given operator
  // Higher returned value means
  // higher precedence
  static int Prec(char ch) {
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
    return -1;
  }

  // The main method that converts
  // given infix expression
  // to postfix expression.
  static String infixToPostfix(String exp) {
    // initializing empty String for result
    String result = new String("");

    // initializing empty stack
    Stack < Character > stack = new Stack < > ();

    for (int i = 0; i < exp.length(); ++i) {
      char c = exp.charAt(i);

      // If the scanned character is an
      // operand, add it to output.
      if (Character.isLetterOrDigit(c))
        result += c;

      // If the scanned character is an '(',
      // push it to the stack.
      else if (c == '(')
        stack.push(c);

      // If the scanned character is an ')',
      // pop and output from the stack
      // until an '(' is encountered.
      else if (c == ')') {
        while (!stack.isEmpty() &&
          stack.peek() != '(')
          result += stack.pop();

        stack.pop();
      } else // an operator is encountered
      {
        while (!stack.isEmpty() && Prec(c) <=
          Prec(stack.peek())) {

          result += stack.pop();
        }
        stack.push(c);
      }

    }

    // pop all the operators from the stack
    while (!stack.isEmpty()) {
      if (stack.peek() == '(')
        return "Invalid Expression";
      result += stack.pop();
    }
    return result;
  }

  // Driver method
  public static void main(String[] args) {
    String exp = "(p+q)*(m-n)";
    System.out.println("Infix expression: " + exp);
    System.out.println("Prefix expression: " + infixToPostfix(exp));
  }
}
```
Time Complexity: O(N)

Space Complexity: O(N) for using the stack
