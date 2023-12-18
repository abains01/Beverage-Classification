#include <iostream>
#include <vector>
#include <string>

// Base class
class Beverage {
protected:
    std::string name;
    std::string description;
    std::string servingSize;
    int calories;
    double price;

public:
    Beverage(const std::string& n, const std::string& desc, const std::string& size, int cal, double pr)
        : name(n), description(desc), servingSize(size), calories(cal), price(pr) {}

    virtual ~Beverage() {}

    // Getter methods
    std::string getName() const { return name; }
    std::string getDescription() const { return description; }
    std::string getServingSize() const { return servingSize; }
    int getCalories() const { return calories; }
    double getPrice() const { return price; }

    // Virtual toString method
    virtual std::string toString() const {
        return "Name: " + name + "\nDescription: " + description +
               "\nServing Size: " + servingSize + "\nCalories: " + std::to_string(calories) +
               "\nPrice: $" + std::to_string(price);
    }
};

// Derived class Coffee
class Coffee : public Beverage {
private:
    std::string hotOrCold;
    bool isCaffeinated;
    bool hasCreamer;
    bool hasSweetener;

public:
    Coffee(const std::string& n, const std::string& desc, const std::string& size, int cal, double pr,
           const std::string& temp, bool caffeinated, bool creamer, bool sweetener)
        : Beverage(n, desc, size, cal, pr), hotOrCold(temp), isCaffeinated(caffeinated),
          hasCreamer(creamer), hasSweetener(sweetener) {}

    // Override toString method
    std::string toString() const override {
        return Beverage::toString() + "\nHot/Cold: " + hotOrCold +
               "\nCaffeinated: " + (isCaffeinated ? "Yes" : "No") +
               "\nCreamer: " + (hasCreamer ? "Yes" : "No") +
               "\nSweetener: " + (hasSweetener ? "Yes" : "No");
    }
};

// Similarly, implement classes Tea, Soda, and EnergyDrink following the same structure.

int main() {
    // Create a vector to store beverages
    std::vector<Beverage*> beverages;

    // Sample user interaction to add a Coffee to the vector
    std::string coffeeName, coffeeDesc, coffeeSize, coffeeTemp;
    int coffeeCal;
    double coffeePrice;
    bool coffeeCaffeinated, coffeeCreamer, coffeeSweetener;

    std::cout << "Enter Coffee details:\n";
    std::cout << "Name: ";
    std::getline(std::cin, coffeeName);
    std::cout << "Description: ";
    std::getline(std::cin, coffeeDesc);
    std::cout << "Serving Size: ";
    std::getline(std::cin, coffeeSize);
    std::cout << "Calories: ";
    std::cin >> coffeeCal;
    std::cout << "Price: $";
    std::cin >> coffeePrice;
    std::cout << "Hot or Cold: ";
    std::cin.ignore(); // Clear the newline from the buffer
    std::getline(std::cin, coffeeTemp);
    std::cout << "Caffeinated (1 for Yes, 0 for No): ";
    std::cin >> coffeeCaffeinated;
    std::cout << "Creamer (1 for Yes, 0 for No): ";
    std::cin >> coffeeCreamer;
    std::cout << "Sweetener (1 for Yes, 0 for No): ";
    std::cin >> coffeeSweetener;

    // Create a Coffee object using the provided data
    Coffee* coffee = new Coffee(coffeeName, coffeeDesc, coffeeSize, coffeeCal,
                                coffeePrice, coffeeTemp, coffeeCaffeinated,
                                coffeeCreamer, coffeeSweetener);

    // Add the Coffee object to the vector
    beverages.push_back(coffee);

    // Display the list of beverages
    std::cout << "\nList of Beverages:\n";
    for (const auto& beverage : beverages) {
        std::cout << beverage->toString() << "\n\n";
    }

    // Clean up dynamically allocated memory
    for (const auto& beverage : beverages) {
        delete beverage;
    }

    return 0;
}
