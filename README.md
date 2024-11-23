# LearningDesignPatterns

# Observer Design Pattern

```
class Susbscribers{
public:
	Susbscribers(int userId)			{ this->userId = userId;}
	~Susbscribers() = default;

	void showMessage() 				{ std::cout << message_; }
	void setMessage(std::string message) 		{ message_ = message; showMessage(); }

private:
	int userId;
	std::string message_;
};

class  YTChannel{
public:

	YTChannel() = default;
	~ YTChannel() = default;

	YTChannel(const char* channelName)		{ name = channelName; }
	void addSubscribers(Susbscribers subscriber)	{ subsGroup.push_back(subscriber); }
	void sendNotification(const char* message)
	{

		std::string msg = message;
		for (auto& subs : subsGroup)
			subs.setMessage(msg);
	}

private:
	std::string name;
	std::vector<Susbscribers> subsGroup;
};



int main()
{
	YTChannel* RFM = new YTChannel(); //create a channel
	
	//Ask for subscribers

	Susbscribers subs1(1);
	RFM->addSubscribers(subs1);

	Susbscribers subs2(2);
	RFM->addSubscribers(subs2);

	Susbscribers subs3(3);
	RFM->addSubscribers(subs3);

	Susbscribers subs4(4);
	RFM->addSubscribers(subs4);

	Susbscribers subs5(5);
	RFM->addSubscribers(subs5);


	RFM->sendNotification("Welcome to the RML channel");
}
```
# Decorator Design Pattern
Example: Coffee Shop with Decorator Pattern
## Step 1: Define the Component Interface
First, we create an interface that defines the operations:

```
// Component interface  
public interface ICoffee  
{  
    string GetDescription();  
    double Cost();  
}
```
## Step 2: Implement the Concrete Component
Next, we have a concrete component that implements the interface:

```
// Concrete Component  
public class SimpleCoffee : ICoffee  
{  
    public string GetDescription()  
    {  
        return "Simple Coffee";  
    }  

    public double Cost()  
    {  
        return 5.0; // Cost of simple coffee  
    }  
}
```

## Step 3: Create the Decorator Base Class
Then, we create a base decorator class that implements the same interface and contains a reference to the component:

```
// Decorator Base Class  
public abstract class CoffeeDecorator : ICoffee  
{  
    protected ICoffee _coffee;  

    public CoffeeDecorator(ICoffee coffee)  
    {  
        _coffee = coffee;  
    }  

    public virtual string GetDescription()  
    {  
        return _coffee.GetDescription();  
    }  

    public virtual double Cost()  
    {  
        return _coffee.Cost();  
    }  
}
```

## Step 4: Implement Concrete Decorators
Now we can create concrete decorators that add additional behavior or responsibilities:

```
// Concrete Decorator for Milk  
public class MilkDecorator : CoffeeDecorator  
{  
    public MilkDecorator(ICoffee coffee) : base(coffee) {}  

    public override string GetDescription()  
    {  
        return _coffee.GetDescription() + ", Milk";  
    }  

    public override double Cost()  
    {  
        return _coffee.Cost() + 1.5; // Cost of milk  
    }  
}  

// Concrete Decorator for Sugar  
public class SugarDecorator : CoffeeDecorator  
{  
    public SugarDecorator(ICoffee coffee) : base(coffee) {}  

    public override string GetDescription()  
    {  
        return _coffee.GetDescription() + ", Sugar";  
    }  

    public override double Cost()  
    {  
        return _coffee.Cost() + 0.5; // Cost of sugar  
    }  
}
```

## Step 5: Use the Decorator Pattern
Finally, you can use these classes in your application to create orders with different combinations of decorators:

```
class Program  
{  
    static void Main(string[] args)  
    {  
        // Create a simple coffee  
        ICoffee myCoffee = new SimpleCoffee();  
        Console.WriteLine($"{myCoffee.GetDescription()} Cost: ${myCoffee.Cost()}");  

        // Add Milk  
        myCoffee = new MilkDecorator(myCoffee);  
        Console.WriteLine($"{myCoffee.GetDescription()} Cost: ${myCoffee.Cost()}");  

        // Add Sugar  
        myCoffee = new SugarDecorator(myCoffee);  
        Console.WriteLine($"{myCoffee.GetDescription()} Cost: ${myCoffee.Cost()}");  

        // Output  
        // Simple Coffee Cost: $5.0  
        // Simple Coffee, Milk Cost: $6.5  
        // Simple Coffee, Milk, Sugar Cost: $7.0  
    }  
}
```

## Explanation
- **ICoffee Interface**: This defines the common operations.
- **SimpleCoffee Class**: This is the basic coffee implementation.
- **CoffeeDecorator Class**: This is the abstract base class for decorators.
- **MilkDecorator and SugarDecorator**: These classes extend the decorator and provide additional functionalities (milk and sugar).
- **Main Method**: This demonstrates how to create a coffee order and decorate it with milk and sugar.
