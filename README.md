# LearningDesignPatterns

# Observer Design Patter

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
