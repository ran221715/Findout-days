#include <iostream>
#include <string>
using namespace std;

int leapyear(int m1, int m2, int y1, int y2)
{
    if (y1 > y2)
    {
        int j = 0;
        int n = y1 - y2;
        for (int i = 1; i < n; i++)
        {
            if ((y2 + i) % 4 == 0)
            {
                j++;
            }
        }
        if (y2 % 4 == 0 && m2 <= 2)
        {
            j++;
        }
        if (y1 % 4 == 0 && m1 > 2)
        {
            j++;
        }
        return j;
    }
    else
    {
        int j = 0;
        int n = y2 - y1;
        for (int i = 1; i < n; i++)
        {
            if ((y1 + i) % 4 == 0)
            {
                j++;
            }
        }
        if (y1 % 4 == 0 && m1 <= 2)
        {
            j++;
        }
        if (y2 % 4 == 0 && m2 > 2)
        {
            j++;
        }
        return j;
    }
}

int countmonths(int m)
{
    int a;
    switch (m)
    {
    case 1:
        a = 31;
        break;
    case 2:
        a = 28;
        break;
    case 3:
        a = 31;
        break;
    case 4:
        a = 30;
        break;
    case 5:
        a = 31;
        break;
    case 6:
        a = 30;
        break;
    case 7:
        a = 31;
        break;
    case 8:
        a = 31;
        break;
    case 9:
        a = 30;
        break;
    case 10:
        a = 31;
        break;
    case 11:
        a = 30;
        break;
    case 12:
        a = 31;
        break;
    default:
        a = 0;
    }
    return a;
}

  int checkInvalid(int d1,int d2,int m1,int m2,int y1,int y2){
     if(m1>12 || m2>12 || m1<0 || m2<0){
        return 1;
    }
    if(d1<0 || d2<0 || d1>31 || d2>31){
        return 1;
    }
    if(m1==4 || m1==6 || m1==9 || m1==11){
        if(d1>30){
            return 1;
        }
    }
    if(m2==4 || m2==6 || m2==9 || m2==11){
        if(d2>30){
            return 1;
        }
    }
    if(m1==2 && y1 % 4==0){
        if(d1>29){
            return 1;
        }
    }
    if(m1==2 && y1 % 4!=0){
        if(d1>28){
            return 1;
        }
    }
    if(m2==2 && y2 % 4==0){
        if(d2>29){
            return 1;
        }
    }
    if(m2==2 && y2 % 4!=0){
        if(d2>28){
            return 1;
        }
    }
    return 0;
}

int main()
{
    int d1, d2, m1, m2, y1, y2, n1, l, n2, k, r;
    int days, y;
    int extradays;

    cout << "the first date which day is known OR today date\nEnter date as 'dd' " << endl;
    cin >> d1;
    cout << "Enter mounths as 'mm' " << endl;
    cin >> m1;
    cout << "Enter year as 'yyyy'" << endl;
    cin >> y1;
    cout << "if days name is sunday then Enter 0\n monday then enter 1 \n tuesday then enter 2";
    cout << "\n wednesday then enter 3\n thursdaythen enter 4\n friday then enter 5 \n saturday then enter 6" << endl;
    cin >> days;
    cout << "the second date which day is find out \nEnter date as 'dd' " << endl;
    cin >> d2;
    cout << "Enter mounths as 'mm' " << endl;
    cin >> m2;
    cout << "Enter year as 'yyyy'" << endl;
    cin >> y2;
    int z=checkInvalid(d1,d2,m1,m2,y1,y2);
    if(z==1){
        cout<<"Data does not exist";
        return 0;
    }

    n1 = 0;
    if (y1 > y2)
    {
        y = y1 - y2;
        l = leapyear(m1, m2, y1, y2);
        n1 = (l + y) % 7;
        if (y1 > y2)
        {
            n1 = 0 - n1;
        }
    }
    else if (y1 < y2)
    {
        y = y2 - y1;
        l = leapyear(m1, m2, y1, y2);
        n1 = (l + y) % 7;
    }

    n2 = 0;
    if (m1 > m2)
    {

        for (int i = m2 + 1; i < m1; i++)
        {
            n2 += countmonths(i);
        }
        k = countmonths(m2);
        n2 += (k - d2);
        n2 += d1;
        n2 = n2 % 7;
        n2 = 0 - n2;
    }
    else if (m1 < m2)
    {
        for (int i = m1 + 1; i < m2; i++)
        {
            n2 += countmonths(i);
        }
        k = countmonths(m1);
        n2 += (k - d1);
        n2 += d2;
        n2 = n2 % 7;
    }
    else
    {
        if (d2 > d1)
        {
            n2 = d2 - d1;
        }
        else
            n2 = d2 - d1;
    }
    extradays = ((n1 + n2) + 7) % 7;
    string arr[7] = {"sunday", "monday", "tuesday", "wednesday", "thursday", "friday", "saturday"};
    r = extradays + days;
    r = r % 7;
    cout << endl;
    cout << endl;
    cout << arr[r];

    return 0;
}

