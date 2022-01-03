#include <iostream>
#include <conio.h>
#include <fstream>
#include <string.h>
#include <stdio.h>
#include <stdlib.h>
#include <process.h>

int bill_no = 1;

using namespace std;

class hostel
{
private:
    int room_no;
    char name[30];
    char address[50];
    char phone[10];
    int  uni_roll;
    char course[10];
    char branch[10];
    char semester[10];
    char batch[10];

public:
    void main_menu();
    void book_room();
    void search_bar();
    void uni_search();
    void search_roomno();
    void room_alloc();
    void edit_menu();
    int check(int);
    void modify();
    void vacate_room();
    void bill_generate();
    bool check_digit(string x);

}hos;

void hostel::main_menu()
{
    int option;
    while (option != 6)
    {

        system("cls");
        cout << "\n************************************************************************************************************************";
        cout << "\n\t\t                      * WELCOME TO AGC ONLINE HOSTEL BOOKING PORTAL *";
        cout << "\n************************************************************************************************************************";
        cout << "\n************************************************************************************************************************";
        cout << "\n\t\t\t                              * MAIN MENU *";
        cout << "\n************************************************************************************************************************";
        cout << "\n\n\n\t\t\t1.Book A Room";
        cout << "\n\t\t\t2.Search Room Records";
        cout << "\n\t\t\t3.Rooms Allotted lsit";
        cout << "\n\t\t\t4.Edit Menu";
        cout << "\n\t\t\t5.Generate My Bill";
        cout << "\n\t\t\t6.Exit";
        cout << "\n\n\t\t\tEnter Option you want to choose: ";
        cin >> option;

        switch (option)
        {
        case 1:
            book_room();
            break;

        case 2:
            search_bar();
            break;

        case 3:
            room_alloc();
            break;

        case 4:
            edit_menu();
            break;

        case 5:
            bill_generate();
            break;
        case 6:
            exit(0);

        default:
        {
            cout << "\n\n\t\t\tWrong choice.....!!!";
            cout << "\n\t\t\tPress any key to   continue....!!";
            getch();
        }
        }
    }
}

void hostel::book_room()
{

    system("cls");
    int r, n, flag;
    char ch;
    ofstream fout("Record.dat", ios::app);
    cout << "\n************************************************************************************************************************";
    cout << "\n\t\t                      * WELCOME TO AGC ONLINE HOSTEL BOOKING PORTAL *";
    cout << "\n************************************************************************************************************************";
    cout << "\n============================================= Room List is as follows: =================================================";
    cout << "\n\n\t\t\t Total no. of Rooms present:  \t   60    ";
    cout << "\n\t\t   -------------------------------------------------";
    cout << "\n\t\t   |     Types of room         |    Room Number    |";
    cout << "\n\t\t   -------------------------------------------------";
    cout << "\n\t\t   | AC Room                   |\t01 - 20    |";
    cout << "\n\t\t   | Water-Cooler Room         |\t21 - 40    |";
    cout << "\n\t\t   | Fan Room                  |\t41 - 60    |";
    cout << "\n \t\t   -------------------------------------------------";
top:
    cout << "\n\n\t\t Enter the room you want to book:- ";
    cin >> r;
    if( r ==0 || r >60)
    {
       cout << "\n\t\t\t Room number invalid....!!";
       goto top;
    }
   else
   {
       flag = check(r);
       if (flag)
    {
        cout << "\n Sorry..!!! Room is already booked";
        goto top;
    }
    else
    {
        char space[10],p[10];
        room_no = r;
        cout << "\n\t\t\tThe room is available.........!!" << endl;
        cout << "\n\t\t---------------------------- Kindly enter your details: --------------------------------------" << endl;
        gets(space);
        cout << " Name: ";
        gets(name);
        cout << " Course: ";
        gets(course);
        cout << " Branch: ";
        gets(branch);
        cout << " Semester: ";
        gets(semester);
        cout << " Address: ";
        gets(address);
        cout<<  " University Roll number: ";
        cin>>uni_roll;
        cout << " Phone Number: ";
        cin >> p;
        if (check_digit(p) == true)
        {
            strcpy(phone,p);
          cout << endl;
        }
        else
        {
            cout << "\t\t Phone Number you entered is not valid";
            cout << "\n Please enter your phone number again: ";
            cin >> phone;
        }
        cout << "\n\n\t\t Do you want to save the data? (y/n)";
        cin >> ch;
        if (ch == 'y')
        {
            fout.write((char *)this, sizeof(hostel));
            cout << "\n Room booked successfully...!!!";
            cout << "\n You can get your bill from the main menu.........";
            fout.close();
        }
        else
        {
            cout << "Data not entered.. " << endl;
            fout.close();
        }
    }
    cout << "\n Press any key to continue.....!!";
    getch();
    fout.close();
   }
}

void hostel ::search_bar()
{
    system("cls");
    int  opt;
    do
    {
        system("cls");
        cout << "\n************************************************************************************************************************";
        cout << "\n\t\t                      * WELCOME TO AGC ONLINE HOSTEL BOOKING PORTAL *";
        cout << "\n************************************************************************************************************************";
        cout << "\n==================================================== * SEARCH MENU * ===================================================";
        cout << "\n\n 1.Search details by university roll no.";
        cout << "\n 2.Search details by room no.";
        cout << "\n 3.Go to Main menu .";
        cout << "\n\n Enter your choice: ";
        cin >> opt;
        switch (opt)
        {
        case 1:
            uni_search();
            break;

        case 2:
            search_roomno();
            break;

        case 3:
            main_menu();
            break;
        default:
        {
            cout << "\n Wrong Choice.....!!";
            cout << "\n Press any key to continue....!!!";
            getch();
        }
        }
    }while (opt != 3);

}

void hostel::search_roomno()
{
    int r,flag =0;
    ifstream fin("Record.dat", ios::in);
    system("cls");
    cout << "\n************************************************************************************************************************";
    cout << "\n\t\t                      * WELCOME TO AGC ONLINE HOSTEL BOOKING PORTAL *";
    cout << "\n************************************************************************************************************************";
    cout << "\n==================================================== * SEARCH MENU * ===================================================";
    cout << "\n\n Enter room no.to get the student`s details :- ";
    cin >> r;

    while (!fin.eof())
    {
        fin.read((char *)this, sizeof(hostel));
        if (room_no == r)
        {
            cout << "\n Student Details";
            cout << "\n ---------------";
            cout << "\n\n Room no: " << room_no;
            cout << "\n University Roll Number : " << uni_roll;
            cout << "\n Name: " << name;
            cout << "\n Address: " << address;
            cout << "\n Semester: " <<semester ;
            cout << "\n Branch: " << branch;
            cout << "\n Course: " << course;
            cout << "\n Phone number: " << phone;
            flag = 1;
            break;
        }
    }
    if (flag == 0)
    {
        cout << "\n Sorry Room you entered found vacant....!!";
    }

    cout << "\n\n Press any key to continue....!!";
    getch();
    fin.close();

}

void hostel ::uni_search()
{
    int ur,u,flag =0,temp =0;
    ifstream fin("Record.dat", ios::in);
    system("cls");
    cout << "\n************************************************************************************************************************";
    cout << "\n\t\t                      * WELCOME TO AGC ONLINE HOSTEL BOOKING PORTAL *";
    cout << "\n************************************************************************************************************************";
    cout << "\n==================================================== * SEARCH MENU * ===================================================";
    num:
    cout << "\n\n Enter university roll no.to get the student`s details :- ";
    cin >> ur;
          while (!fin.eof())
         {
           fin.read((char *)this, sizeof(hostel));
           if (uni_roll == ur)
          {
            cout << "\n Student Details";
            cout << "\n ---------------";
            cout << "\n\n Room no: " << room_no;
            cout << "\n Name: " << name;
            cout << "\n Address: " << address;
            cout << "\n University Roll Number : " << uni_roll;
            cout << "\n Semester: " <<semester ;
            cout << "\n Branch: " << branch;
            cout << "\n Course: " << course;
            flag = 1;
            break;
           }
           else
         }
    if (flag == 0)
    {
        cout << "\n Sorry Room not found....!!";
    }
        }
    cout << "\n\n Press any key to continue....!!";
    getch();
    fin.close();




void hostel ::room_alloc()
{
    system("cls");
    cout << "\n************************************************************************************************************************";
    cout << "\n\t\t                      * WELCOME TO AGC ONLINE HOSTEL BOOKING PORTAL *";
    cout << "\n************************************************************************************************************************";
    cout << "\n============================================== ROOM ALLOCATION MENU: ===================================================";
    ifstream fin("Record.dat", ios::in);
    cout << "\n\n\t    List Of Rooms Allotted";
    cout << "\n\t    ----------------------";
    cout << "\n\n Room No.\t\tName\t\tRollNO\t\t\tAddress\t\t\tPhone Not\t\tSemester\t\t\tCourse\t\t\tBranch\n";

    while (fin.read((char *)this, sizeof(hostel)))
    {

        cout << "\n\n " << room_no << "\t\t\t" << name;
        cout << "\t\t\t" << uni_roll << "\t\t\t\t" << address;
        cout << "\t\t\t" << phone << "\t\t\t\t" << semester;
        cout << "\t\t\t" << course << "\t\t\t\t" << branch;

    }
    cout << "\n\n\n\t\t\tPress any key to continue.....!!";
    getch();
    fin.close();
}

int hostel ::check(int r)
{

    int flag = 0;
    ifstream fin("Record.dat", ios::in);

    while (!fin.eof())
    {
        fin.read((char *)this, sizeof(hostel));
        if (room_no == r)
        {
            flag = 1;
            break;
        }
    }
    fin.close();
    return (flag);
}

void hostel ::bill_generate()
{
    system("cls");
    int dd, mm, yy, r, flag = 0;
    int acprice = 40000, cprice = 30000, fprice = 24000;
    static int mess = 15000;
    cout << "\n************************************************************************************************************************";
    cout << "\n\t\t                       * WELCOME TO AGC ONLINE HOSTEL BOOKING PORTAL *                                             ";
    cout << "\n************************************************************************************************************************";
    cout << "\n================================================= GENERATE BILL: =======================================================";
    cout << "Enter the date of the bill" << endl;
    cin >> dd >> mm >> yy;
    ifstream rd;
    rd.open("record.dat", ios::in | ios::binary);
    cout << "Enter the room number " << endl;
    cin >> r;

    if (!rd)
    {
        cout << "Error opening file.........!" << endl;
    }
    else
    {
        rd.read((char *)&hos, sizeof(hostel));
        while (rd)
        {
            rd.read((char *)&hos, sizeof(hostel));
        }
        if (hos.room_no == r)
        {
            system("cls");
            cout << "\n************************************************************************************************************************";
            cout << "\n\t\t                       * WELCOME TO AGC ONLINE HOSTEL BOOKING PORTAL *                                             ";
            cout << "\n************************************************************************************************************************";
            cout << "\n================================================== HOSTEL BILL: ========================================================";
            if (hos.room_no >= 1 && hos.room_no <= 20)
            {
                cout << "\n\n\n========================================================================================================================";
                cout << "\n\tDate:" << dd << "-" << mm << "-" << yy << "\t\t\t\t\t\t\t\t "
                     << "Bill Number:" << bill_no;
                ;
                cout << "\n========================================================================================================================";
                cout << "\n\n Student Details";
                cout << "\n ---------------";
                cout << "\n\n Room no: " << room_no;
                cout << "\n Name: " << name;
                cout << "\n Address: " << address;
                cout << "\n University Roll Number : " << uni_roll;
                cout << "\n Semester: " <<semester ;
                cout << "\n Branch: " << branch;
                cout << "\n Course: " << course;
                cout << "\n\n\t\t You are booked for AC Room";
                cout << "\n\n Charges:";
                cout << "\n --------";
                cout << "\n Hostel Room Charges: \t\t\t" << acprice;
                cout << "\n Mess Charges: \t\t\t\t" << mess;
                cout << "\n ------------- ";
                cout << "\n Total Charges: \t\t\t" << (mess + acprice);
            }
            else if (hos.room_no >= 21 && hos.room_no <= 40)
            {
                cout << "\n\n\n========================================================================================================================";
                cout << "\n\tDate:" << dd << "-" << mm << "-" << yy << "\t\t\t\t\t\t\t\t "
                     << "Bill Number:" << bill_no;
                ;
                cout << "\n========================================================================================================================";
                cout << "\n\n Student Details";
                cout << "\n ---------------";
                cout << "\n\n Room no: " << room_no;
                cout << "\n Name: " << name;
                cout << "\n Address: " << address;
                cout << "\n University Roll Number : " << uni_roll;
                cout << "\n Semester: " <<semester ;
                cout << "\n Branch: " << branch;
                cout << "\n Course: " << course;
                cout << "\n\n\t\t You are booked for cooler Room";
                cout << "\n\n Charges:";
                cout << "\n --------";
                cout << "\n Hostel Room Charges: \t\t\t" << cprice;
                cout << "\n Mess Charges: \t\t\t\t" << mess;
                cout << "\n ------------- ";
                cout << "\n Total Charges: \t\t\t" << (mess + cprice);
            }
            else
            {
                cout << "\n\n\n========================================================================================================================";
                cout << "\n\tDate:" << dd << "-" << mm << "-" << yy << "\t\t\t\t\t\t\t\t "
                     << "Bill Number:" << bill_no;
                ;
                cout << "\n========================================================================================================================";
                cout << "\n\n Student Details";
                cout << "\n ---------------";
                cout << "\n\n Room no: " << room_no;
                cout << "\n Name: " << name;
                cout << "\n Address: " << address;
                cout << "\n University Roll Number : " << uni_roll;
                cout << "\n Semester: " <<semester ;
                cout << "\n Branch: " << branch;
                cout << "\n Course: " << course;
                cout << "\n\n\t\t You are booked for Fan Room";
                cout << "\n\n Charges:";
                cout << "\n --------";
                cout << "\n Hostel Room Charges: \t\t\t" << fprice;
                cout << "\n Mess Charges: \t\t\t\t" << mess;
                cout << "\n ------------- ";
                cout << "\n Total Charges: \t\t\t" << (mess + fprice);
            }
            bill_no++;
            cout << "\n\n\t\t\t\t\t THANK YOU...!";
            cout << "\n\n\n========================================================================================================================";
            flag = 1;
            getch();
        }
     }

}

void hostel ::edit_menu()
{

    int choice;
    do
    {
        system("cls");
        cout << "\n******************************************";
        cout << "\n\t\t                      * WELCOME TO AGC ONLINE HOSTEL BOOKING PORTAL *";
        cout << "\n******************************************";
        cout << "\n=================================================== EDIT MENU: =========================================================";
        cout << "\n\n 1.Modify My Record.";
        cout << "\n 2.Vacate My Room.";
        cout << "\n 3.Go to Main menu .";
        cout << "\n\n Enter your choice: ";
        cin >> choice;
        switch (choice)
        {
        case 1:
            modify();
            break;

        case 2:
            vacate_room();
            break;

        case 3:
            main_menu();
            break;
        default:
        {
            cout << "\n Wrong Choice.....!!";
            cout << "\n Press any key to continue....!!!";
            getch();
        }
        }
    } while (choice != 3);
}

void hostel::modify()
{
    system("cls");
    int pos, flag = 0, r;
    char space[10];
    fstream file("Record.dat", ios::in | ios::out | ios::binary);
    cout << "\n************************************************************************************************************************";
    cout << "\n\t\t                      * WELCOME TO AGC ONLINE HOSTEL BOOKING PORTAL *";
    cout << "\n************************************************************************************************************************";
    cout << "\n=============================================== MODIFY RECORD MENU: ===================================================";
    cout << "\n\n Enter room no: ";
    cin >> r;

    while (!file.eof())
    {

        pos = file.tellg();
        file.read((char *)this, sizeof(hostel));
        if (room_no == r)
        {
            cout << "\n Enter New Details";
            cout << "\n -----------------";
            gets(space);
            cout << " Name: ";
            gets(name);
            cout << " Course: ";
            gets(course);
            cout << " Branch: ";
            gets(branch);
            cout << " Semester: ";
            gets(semester);
            cout << " Address: ";
            gets(address);
            cout<<  " University Roll number: ";
            cin>>uni_roll;
            cout << " Phone Number: ";
            cin >> phone;
            file.seekp(pos);
            file.write((char *)this, sizeof(hostel));
            cout << "\n\n\t\t Record is modified....!!";
            cout << "\n\n Updated details are:";
            cout << "\n\n Room no: " << room_no;
            cout << "\n Name: " << name;
            cout << "\n Address: " << address;
            cout << "\n University Roll Number : " << uni_roll;
            cout << "\n Semester: " <<semester ;
            cout << "\n Branch: " << branch;
            cout << "\n Course: " << course;

            flag = 1;
            break;
        }
    }
    if (flag == 0)
    {
        cout << "\n Sorry Room found vacant...!!";
    }
    file.close();
}

void hostel::vacate_room()
{
    system("cls");
    int flag = 0, r;
    char ch;
    ifstream fin("Record.dat", ios::in);
    ofstream fout("temp.dat", ios::out);
    cout << "\n************************************************************************************************************************";
    cout << "\n\t\t                      * WELCOME TO AGC ONLINE HOSTEL BOOKING PORTAL *";
    cout << "\n************************************************************************************************************************";
    cout << "\n============================================== VACATE MY ROOM MENU: ===================================================";
    cout << "\n\n Enter room no: ";
    cin >> r;

    while (fin.read((char *)this, sizeof(hostel)))
    {
        if (room_no == r)
        {

            cout << "\n\n Room no: " << room_no;
            cout << "\n Name: " << name;
            cout << "\n Address: " << address;
            cout << "\n University Roll Number : " << uni_roll;
            cout << "\n Semester: " <<semester ;
            cout << "\n Branch: " << branch;
            cout << "\n Course: " << course;
            cout << "\n\n Do you want to delete this record(y/n): ";
            cin >> ch;
            if (ch == 'y')
            {
               cout << "\t\t\t\t\tYour record is deleted. ";
                flag = 1;
            }
            else
            {
                cout<< "\n\n\t\t\tRecord not deleted....";
                cout << "\n\t\t\t Press any key to continue....!!!";
                getch();
            }
        }
        else
        {
            fout.write((char *)this, sizeof(hostel));
        }
    }
    fin.close();
    fout.close();
    if (flag == 0)
    {
        cout << "\t\tSorry room not found vacant......!!!!! " << endl;
    }
    else
    {
        remove("Record.dat");
        rename("temp.dat", "Record.dat");
    }
}

bool hostel::check_digit(string x)
{
    if (x.length() == 10)
    {
        return true;
    }
    else
    {
        return false;
    }
}

int main()
{

    hostel hos;
    system("cls");
    cout << "\n************************************************************************************************************************";
    cout << "\n\t\t                      * WELCOME TO AGC ONLINE HOSTEL BOOKING PORTAL *";
    cout << "\n************************************************************************************************************************";
    cout << "\n\n\n\n\t\tProject Developed By:";
    cout << "\n\n\t\t\t\t Shelly \t\t\t\t\t (1900262)";
    cout << "\n\t\t\t\t Abhishek Bavoria \t\t\t\t (1900105)";
    cout << "\n\t\t\t\t Salil Chandan \t\t\t\t\t (1900250)";
    cout << "\n\t\t\t\t Shewani Katal \t\t\t\t\t (1900263)";
    cout << "\n\n\n\n\n\n\n\t\t\t\t\tPress any key to continue....!!";

    getch();
    hos.main_menu();
    return 0;
}
