//# Tax-Calculation
//You can calculate tax for the commercial and residential property.


#include <iostream>
#include <string>
#include <cmath>
#include <iomanip>
using namespace std;

int main ()
{
        //step 1
          cout<< "+--------------------------------------------------------------+" << endl;
          cout<< "|        Name       : Rieshab Kumar Dev                        |" <<endl;
          cout<< "|        Email      : rieshab.dev12@gmail.com                  |"<<endl;
          cout<< "|        Department : XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX        |"<<endl;
          cout<< "|        Course No. : XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX         |" << endl;
          cout<< "+--------------------------------------------------------------+" << endl;
         

        //step 2  (declare integer constant by 6)
        int ACCOUNT_LENGTH = 6;

        //step 3        (declaring enumaration constant for property type)
        enum Property {COMMERCIAL = 1, RESIDENTIAL = 2};
             
        //step 4  (asking the name from the user and checking)
        string name;
        bool valid = false;
        while (!valid)
        {
                cout<< "Enter your name : ";
                getline (cin,name);
                
                for (int i = 0 ; i < name.length() ; i++)
                {
                        if (!isspace(name[i]) && !isalpha(name[i]) )
                        {
                                cout<< "The name can only have alphabets and whitespace. Enter again : "<< endl;
                                valid = false;
                                break;
                        }
                        else
                        {
                                valid = true;
                                name[0] = toupper(name[0]);
                                if(isspace(name[i]))
                                        name[i+1] = toupper(name[i+1]);
                        }
                }
        }


        //step 5        (asking the account number from the user and checking if it is correct as per need )
        valid = false;
        string accountNumber;
        while (!valid)
        {
                cout << "Enter the account number : " ;
                getline (cin, accountNumber);

                if (accountNumber.length() != ACCOUNT_LENGTH)
                {
                        cout << "The account number should be exactly 6 digits. Enter again : " << endl;
                }
                else
                {
                        for (int i=0 ; i< accountNumber.length();i++)
                        {
                                if (!isalpha(accountNumber[i]) && !isdigit(accountNumber[i]) )
                                {
                                        valid = false;
                                        cout << "The account number must have alphanumeric character. Please enter again : " << endl;
                                        break;
                                }
                                else
                                        valid = true;
                        }
                }
        }
        //step 6        (asking the number of properties)
        valid = false;
        int numProperty;
        while (!valid)
        {
                cout << "Enter the number of properties to process : " <<endl;
                cin >> numProperty;
        
                if (numProperty < 0)
                {
                        valid = false;
                        cout << "Number of properties can not be negative or 0." << endl;
                }
                else
                        valid = true;
        }
        //step 7        (declaring totaltax)
        double totalTax = 0.0;
        
        //step 8        (making operation for the calculation)
        for (int i=1; i <= numProperty; i++)
        {
                double currentTax = 0.00, value;
                valid = false;
                cout << "Processing property #" << i << endl;
                while (!valid)
                {
                        int propertyType;
                        cout << "Enter the property type : " << endl;
                        cout << "1. COMMERCIAL \n2. RESIDENTIAL" << endl;
                        cin >> propertyType;

                        switch (propertyType)
                        {
                                case COMMERCIAL:
                                valid = true;
                                cout << "Enter the value of property : " << "$" ;
                                cin >> value;

                                if (value <= 1000000)
                                {
                                        currentTax = 3.5/100 * value;
                                        totalTax += currentTax;
                                }
                                else
                                {
                                        currentTax = (3.5/100 * 1000000) + 0.05 * (value - 1000000) ;
                                        totalTax += currentTax;
                                }
                                cout << " The total tax for property #"<<i<< "is : " "$" <<fixed<< setprecision(2) << currentTax << endl;
                                break;

                        
                                case RESIDENTIAL:
                                double exemptedTax;
                                valid = true;
                                cout << "Enter the value of the property: " << "$" ;
                                cin >> value;
                                if (value <= 100000)
                                {
                                        currentTax = 0.00;
                                        totalTax += currentTax;
                                }
                                else
                                {
                                       currentTax = 3.5/100 * (value - 100000);
                                        if (numProperty == 1)
                                        {
                                                srand((unsigned int) time(NULL));
                                                exemptedTax = rand() % 1001 + 1000;
                                                currentTax -= exemptedTax;
                                                if (currentTax < 0)
                                                {
                                                        currentTax = 0;
                                                        totalTax = 0;

                                                }

                                        }
                                }
                                totalTax += currentTax;
                                cout << "The total tax for property #" << i<< " is : $" << fixed << setprecision(2)<<currentTax<<endl;
                                cout << "Single property tax exemption is : $" << fixed << setprecision(2)<< exemptedTax << endl;
                                break;
                                default:
                                        valid = false;
                                        cout << "Invalid property type. Enter again : "<<endl;
                                        break;
                        }

                }

        }
        //step 9        (displaying output)
        cout << "Name                 : " << name << endl;
        cout << "Account Number       : " << accountNumber << endl;
        cout << "Your total taxes are : " << totalTax <<endl;
        return 0;
}



