# ClassProj
#include <iostream>
#include <string>
#include <vector>
#include <fstream>
#include <iomanip>

using namespace std;

struct Shareholder {

	//variables for the vector
	string userName; //name of user 
	string shareType; //gold, silver or bronze 
	int numShares; //number of shares 
}; 

void fillVector(vector<Shareholder>& ClientList) {
	int i = 0;
	int clientNum = 1; 
	ifstream infs; 
	infs.open("shares.txt"); //connect the file so it can be opened  
	if (!infs) {
		cerr << "error" << endl; 
	}

	Shareholder invest; 

	while (!infs.eof()) {
		//continue 
		getline(infs, invest.userName);
		infs >> invest.shareType; 
		infs >> invest.numShares; 
		ClientList.push_back(invest); 
		infs.ignore(); //you need the ignore statment 
	}

	infs.close(); //closing the file 

	//printing out values 
	cout << "#" << "    " << "Name" << "    " << "               Category   " << "   Shares" << endl; 
	cout << "--" << "   " << "--------" << "    " << "           -------" << "    " << " ------" << endl; 
	for (i = 0; i < ClientList.size(); ++i) {
		cout << setw(5) << left << clientNum << setw(25) << left << ClientList.at(i).userName << setw(12) << left << ClientList.at(i).shareType << right << ClientList.at(i).numShares << endl; 
		++clientNum; 
	}
}

void PrintShareType(vector<Shareholder> ClientList) { //clean up the code
	cout << endl; 
	cout << "Enter the Category <gold, silver, or bronze>: "; 
	string share;
	cin >> share;
	int i = 0;
	
	cout << "---------------------------" << endl; 
	if (share == "gold") { //if user input is gold 
		cout << "The Gold Clients." << endl; 
		cout << "---------------------------" << endl; 
		int GoldSum = 0;
		int GoldPeople = 0;
		int GoldAvg;
		for (i = 0; i < ClientList.size(); ++i) {
			if (ClientList.at(i).shareType == "Gold") {
				cout << setw(25) << left << ClientList.at(i).userName << right << ClientList.at(i).numShares << endl;
				GoldSum = GoldSum + ClientList.at(i).numShares;
				GoldPeople = GoldPeople + 1;
			}
		}
		cout << "-----------------------------------" << endl; 
		cout << "The average shares for gold is " << GoldSum / GoldPeople << endl; 
		cout << endl; 
	}

	else if (share == "silver") { // if user input is silver 
		cout << "The Silver clients." << endl; 
		cout << "---------------------------" << endl; 
		int sum = 0;
		int people = 0;
		int avgNum;
		for (i = 0; i < ClientList.size(); ++i) {
			if (ClientList.at(i).shareType == "Silver") {
				cout << setw(25) << left << ClientList.at(i).userName << right << ClientList.at(i).numShares << endl;
				sum = sum + ClientList.at(i).numShares;
				++people;
			}
			
		}
		cout << "-----------------------------------" << endl; 
		cout << "The average shares for silver is " << sum / people << endl; 
		cout << endl; 
	}
	
	else if (share == "bronze") {//if user input is bronze 
		cout << "The Bronze clients." << endl; 
		cout << "---------------------------" << endl; 
		int sum = 0;
		int people = 0;
		int avgNum;
		for (i = 0; i < ClientList.size(); ++i) {
			if (ClientList.at(i).shareType == "Bronze") {
				cout << setw(25) << left << ClientList.at(i).userName << right << ClientList.at(i).numShares << endl;
				sum = sum + ClientList.at(i).numShares;
				++people;
			}
		}
		cout << "-----------------------------------" << endl; 
		cout << "The average shares for bronze is " << sum / people << endl; 
		cout << endl; 
	}

	else {
		cout << "Invalid input! Please input gold, silver, or bronze" << endl; 
	}

	cout << "-----------------------------------" << endl; 
}

void FindValues(vector<Shareholder> ClientList) { //FIXMEE make the output match the intended output 
	double GoldVal = 8.95; 
	double SilverVal = 4.95; 
	double BronzeVal = 1.95; 
	int i; 
	double GoldSum = 0.0; 
	double SilverSum = 0.0; 
	double BronzeSum = 0.0; 
	double totalSum; 

	
	for (i = 0; i < ClientList.size(); ++i) {

		if (ClientList.at(i).shareType == "Gold") {
			ClientList.at(i).numShares = ClientList.at(i).numShares * GoldVal;
			GoldSum = ClientList.at(i).numShares + GoldSum;
		}

		else if (ClientList.at(i).shareType == "Silver") {
			ClientList.at(i).numShares = ClientList.at(i).numShares * SilverVal;
			SilverSum = ClientList.at(i).numShares + SilverSum;
		}

		else {
			ClientList.at(i).numShares = ClientList.at(i).numShares * BronzeVal;
			BronzeSum = ClientList.at(i).numShares + BronzeSum; 
		}
	}
	totalSum = GoldSum + SilverSum + BronzeSum;

	cout << "================= FindAssets ===================" << endl; 
	cout << "************************************************" << endl; 
	cout << setw(44) << left << "The value of the Gold shareholders is " <<  right << GoldSum << endl;
	cout << setw(44) << left << "The value of the Silver shareholder is " << right << SilverSum << endl;
	cout << setw(44) << left << "The value of the Bronze shareholder is " << right << BronzeSum << endl;
	cout << setw(44) << left << "The Total value of the Shareholders is " << right << totalSum << endl;

	cout << endl; 
}







int main() { //Clean up code, Good Job Today!
	vector<Shareholder> ClientList; //client list vector 
	fillVector(ClientList);
	cout << "=================" << " " << "FindCat " << "==================" << endl; 

	cout << endl; 
	PrintShareType(ClientList); 
	cout << endl; 
	FindValues(ClientList);
	cout << endl; 
	cout << "apple" << endl; 
}
