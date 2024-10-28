using System;
using System.Collections.Generic;

namespace ProductComparison
{
    class Product
    {
        public string Name { get; set; }
        public decimal Price { get; set; }
        public string Description { get; set; }

        // Можно добавить больше свойств для сравнения:
        // public string Brand { get; set; }
        // public int Rating { get; set; } 
        // ...
    }

    class Program
    {
        static List<Product> products = new List<Product>();

        static void Main(string[] args)
        {
            Console.WriteLine("Добро пожаловать в систему сравнения продуктов!");

            while (true)
            {
                Console.WriteLine("\nВыберите действие:");
                Console.WriteLine("1. Добавить продукт");
                Console.WriteLine("2. Отобразить продукты");
                Console.WriteLine("3. Сравнить продукты");
                Console.WriteLine("4. Выход");

                int choice = GetChoice();

                switch (choice)
                {
                    case 1:
                        AddProduct();
                        break;
                    case 2:
                        DisplayProducts();
                        break;
                    case 3:
                        CompareProducts();
                        break;
                    case 4:
                        Console.WriteLine("До свидания!");
                        return;
                    default:
                        Console.WriteLine("Неверный выбор.");
                        break;
                }
            }
        }

        static int GetChoice()
        {
            // ... (Эта функция уже описана в предыдущем примере)
        }

        static void AddProduct()
        {
            Console.WriteLine("Введите название продукта:");
            string name = Console.ReadLine();

            Console.WriteLine("Введите цену продукта:");
            decimal price = GetDecimalInput();

            Console.WriteLine("Введите описание продукта:");
            string description = Console.ReadLine();

            products.Add(new Product { Name = name, Price = price, Description = description });
            Console.WriteLine("Продукт добавлен!");
        }

        static decimal GetDecimalInput()
        {
            // ... (Эта функция уже описана в предыдущем примере)
        }

        static void DisplayProducts()
        {
            if (products.Count == 0)
            {
                Console.WriteLine("Нет продуктов.");
            }
            else
            {
                Console.WriteLine("\nСписок продуктов:");
                for (int i = 0; i < products.Count; i++)
                {
                    Console.WriteLine($"{i + 1}. {products[i].Name} - {products[i].Price:C} - {products[i].Description}");
                }
            }
        }

        static void CompareProducts()
        {
            if (products.Count < 2)
            {
                Console.WriteLine("Необходимо добавить как минимум два продукта для сравнения.");
                return;
            }

            DisplayProducts();

            Console.WriteLine("Введите номера продуктов, которые вы хотите сравнить (например, 1,3):");
            string input = Console.ReadLine();

            string[] productNumbers = input.Split(',');
            if (productNumbers.Length != 2)
            {
                Console.WriteLine("Неверный ввод. Введите два номера продуктов.");
                return;
            }

            if (!int.TryParse(productNumbers[0], out int productIndex1) || !int.TryParse(productNumbers[1], out int productIndex2))
            {
                Console.WriteLine("Неверный ввод. Введите номера продуктов.");
                return;
            }

            if (productIndex1 < 1 || productIndex1 > products.Count || productIndex2 < 1 || productIndex2 > products.Count)
            {
                Console.WriteLine("Неверные номера продуктов.");
                return;
            }

            Product product1 = products[productIndex1 - 1];
            Product product2 = products[productIndex2 - 1];

            Console.WriteLine($"\nСравнение продуктов:");
            Console.WriteLine($"Название: {product1.Name} vs {product2.Name}");
            Console.WriteLine($"Цена: {product1.Price:C} vs {product2.Price:C}");
            Console.WriteLine($"Описание: {product1.Description} vs {product2.Description}");

            // Добавьте сюда сравнение других свойств, например, рейтинга, бренда и т.д.
        }
    }
}
