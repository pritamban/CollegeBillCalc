#include <iostream>
#include <string>
using namespace std;

void mainBanner();
void residencyStatusMenu(string name);
void housingPreferenceMenu(string name);
double getIntInRange(int, int);

int main() {
	system("color e1");
	system("title constant variables, cin functions+methods, if and if ... else, logical operators, conditional operator      by P.Ban");
	
	int roomDiscount, tuitionBill, roomCharge, totalBill, i;

	string name;
	double housingPreferenceChoice, residencyStatusChoice;

	const int
		IN_STATE_TUITION = 3000,
		OUT_OF_STATE_TUITION = 5000,
		INTERNATIONAL_TUITION = 6700,
		PRIVATE_ROOM_CHARGE = 8000,
		DISCOUNT_PER_ROOMMATE = 1000;

	mainBanner();
	getline(cin, name);

	residencyStatusMenu(name);
	residencyStatusChoice = getIntInRange(1, 3);
	switch (static_cast<int>(residencyStatusChoice)) {
	case 1:
		tuitionBill = IN_STATE_TUITION;
	case 2:
		tuitionBill = OUT_OF_STATE_TUITION;
	case 3:
		tuitionBill = INTERNATIONAL_TUITION;
	}

	housingPreferenceMenu(name);
	housingPreferenceChoice = getIntInRange(1, 5);

	if (housingPreferenceChoice < 5) {
		if (housingPreferenceChoice == 1)
			roomDiscount = 0;
		else
			roomDiscount = DISCOUNT_PER_ROOMMATE * (housingPreferenceChoice - 1);

		roomCharge = PRIVATE_ROOM_CHARGE - roomDiscount;
	}
	else
		roomCharge = 0;

	if (housingPreferenceChoice != 5) {
		cout << "\n  Your room discount is $ " << roomDiscount << " because you have " << housingPreferenceChoice - 1 << " roomate" << (housingPreferenceChoice !=2 ? "s." : ".");
	}

	totalBill += roomCharge;

	cout << "\n\n         ******************************************\n\n"
		"  Your bill is $ " << tuitionBill << " for tuition and $ " << roomCharge << " for room charge.\n"
		"  the total amount you owe is $ " << totalBill << ".\n\n";

	system("pause");
	return 0;
}

void mainBanner() {
	cout << "\n"
		<< "\t\t                    College Bill Calculator                          \n"
		<< "\t\t       not as easy as it looks - the devil is in the details!        \n"
		<< "\t\t               make sure you test EVERY possible input               \n"
		<< "\t\t                compensate for user's 'extra' input                  \n"
		<< "\t\t  make sure you follow all the learning outcomes of the previous labs\n"
		<< "\t\t                           by P. Ban                             \n\n\n";

	cout << "Hints:\n"
		<< "  to reduce typing time you can copy and paste my prompts from the exe    \n"
		<< "  You need to use the WYSIWYG approach in many places!                  \n\n";

	cout << "You MUST have and appropriatelly use the following as const variables:   \n"
		<< "  in state tuition      $ 3,000                                           \n"
		<< "  out of state tuition  $ 5,000                                           \n"
		<< "  international tuition $ 6,700                                           \n"
		<< "  private room charge   $ 8,000                                           \n"
		<< "  discount per roomate  $ 1,000                                         \n\n";

	cout << "To make sure you practice more Learning outcomes make sure that          \n"
		<< "  For checking the residency valididy do NOT use < or <= or >=            \n"
		<< "  For checking the housing preference valididy do NOT use !=            \n\n";

	cout << "Please enter your full name: ";
}

void residencyStatusMenu(string name) {
	cout << "\nWhat is your residency status \" " << name << "\"?\n"
		<< "  Residency status choices :\n"
		<< "    1]  in state            \n"
		<< "    2]  out of state        \n"
		<< "    3]  international       \n"
		<< "  Enter your choice[1, 2 or 3]: ";
}

void housingPreferenceMenu(string name) {
	cout << "\nWhat is your housing preference \"" << name << "\"?\n"
		"  Housing choices :     \n"
		"    1]  single room dorm\n"
		"    2]  double room dorm\n"
		"    3]  triple room dorm\n"
		"    4]  quad room dorm  \n"
		"    5]  live off campus \n"
		"  Enter your choice[1 to 5]: ";
}

double getIntInRange(int y, int z) {
	double x;
	cin >> x;
	cin.ignore(1000, '\n');

	while ((x < y || x > z || (x - static_cast<int>(x) != 0))) {
		cout << "\n   xxx   You entered an illegal residency choice.    xxx\n";

		if (x < y || x > z ) {
			cout << "     Valid residency status choices must be between " << y << " and " << z << ".\n";
		}

		if (x - static_cast<int>(x) != 0) {
			cout << "     Residency status MUST be an integer.\n";
		}
		cout << "\n     Please enter a valid residency status: ";
		system("color c7");
		cin >> x;
		cin.ignore(10000, '\n');
	}

	system("color e1");
	return x;
}