<img width="620" alt="Screenshot 2024-11-20 at 6 55 33 PM" src="https://github.com/user-attachments/assets/8c6f0728-daf1-4380-85d8-d0d7707ee5e1">
A slight difference in infixtopostfix !!!!:Remember
 ## original : infix to postfix
```
while (!stack.isEmpty() && getPrecedence(c) <= getPrecedence(stack.peek())) {
    result.append(stack.pop());
}
```
## infix to prefix (via postfix)
