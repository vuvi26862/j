using System;

namespace WaterBillingSystem
{
    internal class Program
    {
        static string NameCustoms()
        {
            Console.WriteLine("Enter your name:");
            string name = Console.ReadLine();
            return name;
        }

        static int TypeOfCustomer()
        {
            Console.WriteLine("Type of customer:\n\t1. Household customer\n\t2. Administrative agency, public services\n\t3. Production units\n\t4. Business services");
            Console.WriteLine("Enter your type (1-4):");
            int type = Convert.ToInt32(Console.ReadLine());
            while (type < 1 || type > 4)
            {
                Console.WriteLine("Please enter a number from 1-4");
                type = Convert.ToInt32(Console.ReadLine());
            }
            return type;
        }

        static double CalculateWaterConsumption()
        {
            Console.WriteLine("Enter quantity consumed last month:");
            double previousQuantity = Convert.ToDouble(Console.ReadLine());
            Console.WriteLine("Enter consumption numbers this month:");
            double currentQuantity = Convert.ToDouble(Console.ReadLine());

            if (previousQuantity > currentQuantity)
                Console.WriteLine("Error: Current quantity must be higher than previous quantity.");

            double consumption = currentQuantity - previousQuantity;
            Console.WriteLine("Cubic feet of water consumed:");
            Console.WriteLine(consumption);

            return consumption;
        }

        static double CalculatePrice()
        {
            int type = TypeOfCustomer();
            string typeOfCustomer;
            double price = default;
            double consumption = CalculateWaterConsumption();

            switch (type)
            {
                case 1:
                    typeOfCustomer = "Household customer";
                    if (consumption > 0 && consumption <= 10)
                    {
                        price = consumption * 5.973;
                        Console.WriteLine($"Water price for {typeOfCustomer} is: 5.973 VND/m3");
                    }
                    else if (consumption > 10 && consumption <= 20)
                    {
                        price = consumption * 7.052;
                        Console.WriteLine($"Water price for {typeOfCustomer} is: 7.052 VND/m3");
                    }
                    else if (consumption > 20 && consumption <= 30)
                    {
                        price = consumption * 8.699;
                        Console.WriteLine($"Water price for {typeOfCustomer} is: 8.699 VND/m3");
                    }
                    else if (consumption > 30)
                    {
                        price = consumption * 15.929;
                        Console.WriteLine($"Water price for {typeOfCustomer} is: 15.929 VND/m3");
                    }
                    break;
                case 2:
                    typeOfCustomer = "Administrative agency, public services";
                    price = consumption * 9.955;
                    Console.WriteLine($"Water price for {typeOfCustomer} is: 9.955 VND/m3");
                    break;
                case 3:
                    typeOfCustomer = "Production units";
                    price = consumption * 11.615;
                    Console.WriteLine($"Water price for {typeOfCustomer} is: 11.615 VND/m3");
                    break;
                case 4:
                    typeOfCustomer = "Business services";
                    price = consumption * 22.068;
                    Console.WriteLine($"Water price for {typeOfCustomer} is: 22.068 VND/m3");
                    break;
            }

            return price;
        }

        static double CalculateTotalBill()
        {
            double price = CalculatePrice();
            double tax = price * 0.1;
            double totalBill = price + tax;
            Console.WriteLine($"Your water bill is: {totalBill} VND");
            return totalBill;
        }

        static void Main(string[] args)
        {
            Console.WriteLine("Water Billing System");
            string customerName = NameCustoms();
            Console.WriteLine($"Customer: {customerName}");
            CalculateTotalBill();
            Console.ReadLine();
        }
    }
}
