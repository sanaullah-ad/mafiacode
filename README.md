using System;
using System.Collections.Generic;

class Product
{
    public int Id { get; set; }
    public string Name { get; set; }
    public int Quantity { get; set; }
    public decimal Price { get; set; }

    public Product(int id, string name, int quantity, decimal price)
    {
        Id = id;
        Name = name;
        Quantity = quantity;
        Price = price;
    }

    public void DisplayProduct()
    {
        Console.WriteLine($"ID: {Id}, Name: {Name}, Quantity: {Quantity}, Price: {Price:C}");
    }
}

class Inventory
{
    private List<Product> products = new List<Product>();
    private int nextId = 1;

    public void AddProduct(string name, int quantity, decimal price)
    {
        Product product = new Product(nextId++, name, quantity, price);
        products.Add(product);
        Console.WriteLine($"Product '{name}' added successfully!");
    }

    public void DisplayInventory()
    {
        Console.WriteLine("\n--- Inventory ---");
        if (products.Count == 0)
        {
            Console.WriteLine("Inventory is empty.");
        }
        else
        {
            foreach (var product in products)
            {
                product.DisplayProduct();
            }
        }
        Console.WriteLine("-----------------\n");
    }

    public void UpdateStock(int id, int newQuantity)
    {
        Product product = products.Find(p => p.Id == id);
        if (product != null)
        {
            product.Quantity = newQuantity;
            Console.WriteLine($"Product '{product.Name}' updated with new quantity: {newQuantity}");
        }
        else
        {
            Console.WriteLine("Product not found!");
        }
    }

    public void RemoveProduct(int id)
    {
        Product product = products.Find(p => p.Id == id);
        if (product != null)
        {
            products.Remove(product);
            Console.WriteLine($"Product '{product.Name}' removed successfully.");
        }
        else
        {
            Console.WriteLine("Product not found!");
        }
    }
}

class Program
{
    static void Main(string[] args)
    {
        Inventory inventory = new Inventory();
        bool running = true;

        while (running)
        {
            Console.WriteLine("Inventory Management System");
            Console.WriteLine("1. Add Product");
            Console.WriteLine("2. View Inventory");
            Console.WriteLine("3. Update Product Quantity");
            Console.WriteLine("4. Remove Product");
            Console.WriteLine("5. Exit");
            Console.Write("Choose an option: ");
            string choice = Console.ReadLine();

            switch (choice)
            {
                case "1":
                    Console.Write("Enter product name: ");
                    string name = Console.ReadLine();
                    Console.Write("Enter quantity: ");
                    int quantity = int.Parse(Console.ReadLine());
                    Console.Write("Enter price: ");
                    decimal price = decimal.Parse(Console.ReadLine());
                    inventory.AddProduct(name, quantity, price);
                    break;
                case "2":
                    inventory.DisplayInventory();
                    break;
                case "3":
                    Console.Write("Enter product ID to update: ");
                    int idToUpdate = int.Parse(Console.ReadLine());
                    Console.Write("Enter new quantity: ");
                    int newQuantity = int.Parse(Console.ReadLine());
                    inventory.UpdateStock(idToUpdate, newQuantity);
                    break;
                case "4":
                    Console.Write("Enter product ID to remove: ");
                    int idToRemove = int.Parse(Console.ReadLine());
                    inventory.RemoveProduct(idToRemove);
                    break;
                case "5":
                    running = false;
                    Console.WriteLine("Exiting the system...");
                    break;
                default:
                    Console.WriteLine("Invalid option, please try again.");
                    break;
            }

            Console.WriteLine();
        }
    }
}
