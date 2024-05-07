using System;
using System.Collections.Generic;
using System.Text;
using System.Text.RegularExpressions;
using System.Xml.Linq;
using static ConsoleApp2.Program;

namespace ConsoleApp2
{
    internal partial class Program
    {
        static void Main(string[] args)
        {
            while (true)
            {
                Console.WriteLine("Введите первое слово:");
                string word1 = Console.ReadLine().ToLower(); 

                Console.WriteLine("Введите второе слово:");
                string word2 = Console.ReadLine().ToLower(); 

                var operations = CalculateMinimumOperations(word1, word2);
                Console.WriteLine($"Минимальное количество действий: {operations.Count}");
                Console.WriteLine("Последовательность действий:");

                foreach (var operation in operations)
                {
                    Console.WriteLine(operation);
                }
            }
        }
        static List<string> CalculateMinimumOperations(string word1, string word2)
        {
            // Инициализируем матрицу для хранения результатов
            int[,] dp = new int[word1.Length + 1, word2.Length + 1];
            List<string> operations = new List<string>();

            for (int i = 0; i <= word1.Length; i++)
            {
                for (int j = 0; j <= word2.Length; j++)
                {
                    if (i == 0)
                    {
                        dp[i, j] = j; 
                    }
                    else if (j == 0)
                    {
                        dp[i, j] = i; 
                    }
                    else if (word1[i - 1] == word2[j - 1])
                    {
                        dp[i, j] = dp[i - 1, j - 1]; 
                    }
                    else
                    {
                        dp[i, j] = 1 + Math.Min(dp[i - 1, j - 1], Math.Min(dp[i - 1, j], dp[i, j - 1]));
                    }
                }
            }
            int m = word1.Length, n = word2.Length;
            while (m > 0 || n > 0)
            {
                if (m > 0 && n > 0 && word1[m - 1] == word2[n - 1])
                {
                    m--;
                    n--;
                }
                else if (n > 0 && (m == 0 || dp[m, n] == dp[m, n - 1] + 1))
                {
                    // Если операция - добавление буквы
                    operations.Add($"Добавить '{word2[n - 1]}' в позицию {m + 1}");
                    n--;
                }
                else if (m > 0 && (n == 0 || dp[m, n] == dp[m - 1, n] + 1))
                {
                    // Если операция - удаление буквы
                    operations.Add($"Удалить '{word1[m - 1]}' в позиции {m}");
                    m--;
                }
                else if (m > 0 && n > 0 && dp[m, n] == dp[m - 1, n - 1] + 1)
                {
                    // Если операция - замена буквы
                    operations.Add($"Заменить '{word1[m - 1]}' на '{word2[n - 1]}' в позиции {m}");
                    m--;
                    n--;
                }
            }
            // Реверсируем список операций, чтобы они были в правильном порядке
            operations.Reverse();
            return operations;
        }
    }
}
