import java.util.Scanner;
import java.util.regex.Matcher;
import java.util.regex.Pattern;

class Main {
public static String calc(String input) {
String regex = "^(\\d{1,2})\\s*([+\\-*/])\\s*(\\d{1,2})$";
Pattern pattern = Pattern.compile(regex);
Matcher matcher = pattern.matcher(input.trim());

if (!matcher.matches()) {
throw new IllegalArgumentException("" + "throws Exception");
}

int num1 = Integer.parseInt(matcher.group(1));
String operator = matcher.group(2);
int num2 = Integer.parseInt(matcher.group(3));

if (num1 < 1 || num1 > 10 || num2 < 1 || num2 > 10) {
throw new IllegalArgumentException("Numbers must be between 1 and 10");
}

int result;
switch (operator) {
case "+":
result = num1 + num2;
break;
case "-":
result = num1 - num2;
break;
case "*":
result = num1 * num2;
break;
case "/":
if (num2 == 0) {
throw new ArithmeticException("Division by zero is not allowed");
}
result = num1 / num2;
break;
default:
throw new IllegalArgumentException("Unsupported operator");
}

return String.valueOf(result);
}

public static void main(String[] args) {
Scanner scanner = new Scanner(System.in);
System.out.println("Введите выражение (например, 3 + 5):");
String input = scanner.nextLine();

try {
String result = calc(input);
System.out.println("Результат: " + result);
} catch (IllegalArgumentException | ArithmeticException e) {
System.err.println("Ошибка: " + e.getMessage());
}
}
}

