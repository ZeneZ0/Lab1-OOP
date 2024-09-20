# Lab1-OOP
import java.util.Arrays;


public class Main
{

    public static void main(String[] args)
    {
        // Исходный текст для анализа
        String text = "Это текст для анализа. Он содержит три предложения. " +
                "В первом предложении три слова, во втором - четыре. Привет.";

        // Числовой массив для удаления дубликатов
        int[] numbers = {1, 2, 3, 2, 4, 5, 5, 1};

        // 1. определение числа предложений в тексте
        int sentenceCount = countSentence(text);
        System.out.println("Число предложений в тексте: " + sentenceCount);

        // 2. Поиск самого часто встречающегося слова
        String mostFrequentWord = word(text);
        System.out.println("Самое часто встречающееся слово: " + mostFrequentWord);

        // 3. Определение числа слов, начинающихся с гласной/согласной
        int vowelCount = sentesVowel(text);
        int consonantCount = sentesConsonant(text);
        System.out.println("Число слов, начинающихся с гласной: " + vowelCount);
        System.out.println("Число слов, начинающихся с согласной: " + consonantCount);

        // 4.Удаление повторяющихся значений в массиве
        int[] uniqueNumbers = removeDuplicat(numbers);
        System.out.println("Массив без повторений:");
        for (int number : uniqueNumbers)
        {
            System.out.print(number + " ");
        }
        System.out.println();
    }

    // Метод для подсчета предложений в тексте
    private static int countSentence(String text)
    {
        int count = 1; // Начинаем с 1, т.к. первое предложение всегда есть
        for (int i = 0; i < text.length(); i++)
        {
            if (text.charAt(i) == '.' || text.charAt(i) == '!' || text.charAt(i) == '?')
            {
                count++;
            }
        }
        return count;
    }

    // Метод для поиска самого часто встречающегося слова
    private static String word(String text)
    {
        String[] words = text.toLowerCase().split("[\\s.,!?;:]+"); // Разделяем текст на слова и приводим к нижнему регистру, чтобы не учитывать разнрицу например между Hello и hello
        int[] wordCounts = new int[words.length]; // Массив для хранения количества вхождений каждого слова
        int maxCount = 0; // Максимальное количество вхождений
        int maxIndex = 0; // Индекс слова с максимальным количеством вхождений

        for (int i = 0; i < words.length; i++)
        {
            if (!words[i].isEmpty())
            { // Проверяем, что слово не пустое
                for (int j = 0; j < words.length; j++)
                {
                    if (words[i].equals(words[j]))
                    {
                        wordCounts[i]++;
                    }
                }
                if (wordCounts[i] > maxCount)
                {
                    maxCount = wordCounts[i];
                    maxIndex = i;
                }
            }
        }

        return words[maxIndex]; // Возвращаем слово с максимальным количеством вхождений
    }

    // Метод для подсчета слов, начинающихся с гласной
    private static int sentesVowel(String text)
    {
        String[] words = text.toLowerCase().split("[\\s.,!?;:]+"); // Разделяем текст на слова и приводим к нижнему регистру для разницы между А и а(чтобы не видеть её)
        int vowelCount = 0;

        for (int i = 0; i < words.length; i++)
        {
            if (!words[i].isEmpty() && isVowel(words[i].charAt(0)))
            { // Проверяем, что слово не пустое и первый символ - гласная
                vowelCount++; // Увеличиваем счетчик гласных слов
            }
        }

        return vowelCount;
    }

    // Метод для подсчета слов, начинающихся с согласной
    private static int sentesConsonant(String text)
    {
        String[] words = text.toLowerCase().split("[\\s.,!?;:]+"); // Разделяем текст на слова и приводим к нижнему регистру
        int consonantCount = 0;

        for (int i = 0; i < words.length; i++)
        {
            if (!words[i].isEmpty() && !isVowel(words[i].charAt(0)))
            { // Проверяем, что слово не пустое и первый символ - согласная
                consonantCount++; // Увеличиваем счетчик согласных слов
            }
        }

        return consonantCount;
    }

    // Метод для проверки, является ли символ гласной
    private static boolean isVowel(char ch)
    {
        return "АЕЁИОУЫЭЮЯаеёиоуыэюя".indexOf(ch) != -1; // Проверяем, есть ли символ в строке гласных
    }

    // Метод для удаления повторяющихся значений в массиве
    private static int[] removeDuplicat(int[] numbers)
    {
        int[] uniqueNumbers = new int[numbers.length]; // Создаем новый массив для уникальных значений соразмерный оригинальному массиву
        int count = 0; // Счетчик уникальных значений

        for (int i = 0; i < numbers.length; i++)
        {
            boolean isDuplicate = false; // Флаг, указывающий, является ли элемент дубликатом

            for (int j = 0; j < i; j++)
            {
                if (numbers[i] == numbers[j])
                { // Проверяем, есть ли такой элемент в массиве до текущего
                    isDuplicate = true;
                    break;
                }
            }

            if (!isDuplicate)
            { // Если элемент не дубликат, добавляем его в массив уникальных значений
                uniqueNumbers[count++] = numbers[i];
            }
        }

        return Arrays.copyOf(uniqueNumbers, count); // Возвращаем массив без повторений
    }
}
