import java.util.Scanner;

class Main {

    public static String calc(String input) {
        // Ожидаем формат входной строки: "a operator b"
        String[] parts = input.split(" "); // Добавлено объявление parts

        if (parts.length != 3) {
            throw new IllegalArgumentException("Ошибка: Введите выражение в формате 'a operator b'.");
        }

        // Парсинг чисел и операции
        try {
            int a = Integer.parseInt(parts[0]);
            char operator = parts[1].charAt(0);
            int b = Integer.parseInt(parts[2]);

            if (a < 1 || a > 10 || b < 1 || b > 10) {
                throw new IllegalArgumentException("Ошибка: Числа должны быть в диапазоне от 1 до 10.");
            }

            int result;

            switch (operator) {
                case '+':
                    result = a + b;
                    return String.valueOf(result);
                case '-':
                    result = a - b;
                    return String.valueOf(result);
                case '*':
                    result = a * b;
                    return String.valueOf(result);
                case '/':
                    if (b == 0) {
                        throw new IllegalArgumentException("Ошибка: Деление на ноль невозможно.");
                    }
                    result = a / b;
                    return String.valueOf(result);
                default:
                    throw new IllegalArgumentException("Ошибка: Неверная операция.");
            }
        } catch (NumberFormatException e) {
            throw new IllegalArgumentException("Ошибка: Ввод должен содержать целые числа.");
        }
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.println("Введите арифметическое выражение (например, '2 + 3'): ");

        String input = scanner.nextLine();

        try {
            String result = calc(input);
            System.out.println("Результат: " + result);
        } catch (IllegalArgumentException e) {
            System.out.println(e.getMessage());
        } finally {
            scanner.close();
        }
    }
}
