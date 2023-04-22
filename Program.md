# CS210_Project3

#include <iostream>
#include <fstream>
#include <string>
#include <map>
using namespace std;

int main() {
	// creates map and opens files
	map <string, int> Item_Frequency;
	std::ifstream input_file("CS210_Project_Three_Input_File.txt");
	std::ofstream output_file("Frequency.txt");

	// adds 1 when an item shows up on the list (frequency)
	string item;
	while (input_file >> item) {
		++Item_Frequency[item];
	}

	// prints the output onto the frequency.txt file
	for (auto i : Item_Frequency) {
		output_file << i.first << " " << i.second << endl;
	}

	bool run_menu = true;
	bool correct_input;
	int user_input;
	string grocery_item;

	// menu loop
	do {

		cout << endl;
		cout << "********************************************************" << endl;
		cout << "*            Please Select A Menu Option               *" << endl;
		cout << "********************************************************" << endl;
		cout << "*  1. Print item frequency                             *" << endl;
		cout << "*  2. Print all items and the frequency                *" << endl;
		cout << "*  3. Print histogram                                  *" << endl;
		cout << "*  4. Exit Program                                     *" << endl;
		cout << "********************************************************" << endl;
		cout << endl;

		try {
			std::cin >> user_input;
			cout << endl;

			// if user enters wrong input
			while (std::cin.fail()) {
				std::cin.clear();
				std::cin.ignore(256, '\n');
				cout << "Please enter a valid input." << endl;
				std::cin >> user_input;
				cout << endl;
			}
			if (user_input > 0 && user_input < 5) {
				correct_input = true;
			}
			else {
				throw (user_input);
			}
		}
		catch (...) {
			cout << "Please enter a valid input." << endl;
		}
		// if user selects option 1 on menu
		if (user_input == 1) {
			cout << "*****************************************************************" << endl;
			cout << "* Please enter the item you would like to see the frequency of: *" << endl;
			cout << "*****************************************************************" << endl;
			cout << endl;
			std::cin >> grocery_item;

			// If user enters item that is not in the files
			if (Item_Frequency.find(grocery_item) == Item_Frequency.end()) {
				cout << "Sorry this item is not in our files." << endl;
			}
			// If user enters item that is in files
			else {
				cout << grocery_item << " were sold " << Item_Frequency[grocery_item] << " times." << endl;
			}
		}

		// if user selects option 2 on menu
		else if (user_input == 2) {
			cout << endl;
			cout << "********************************************************" << endl;
			cout << "*            Items sold and amount sold                *" << endl;
			cout << "********************************************************" << endl;
			cout << endl;

			for (auto i : Item_Frequency) {
				cout << i.first << " " << i.second << endl;
			}
		}

		// if user selects option 3 on menu
		else if (user_input == 3) {
			cout << endl;
			cout << "********************************************************" << endl;
			cout << "*             Items sold and histogram                 *" << endl;
			cout << "********************************************************" << endl;
			cout << endl;

			for (auto i : Item_Frequency) {
				cout << i.first << " ";
				for (int j = 0; j < i.second; j++) {
					cout << "*";
				}
				cout << endl;
			}
		}
		
		// if user selects option 4 on menu. Exits program
		else if (user_input == 4) {
			cout << "Exiting Corner Grocer System. Thank you!" << endl;
			run_menu = false;
		}

		
		} while (run_menu == true);
	}
