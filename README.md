# SHAIKGN
# PROBLEM STATEMENT
Kekocity's population consist of N gnomes numbered with unique ids from 1 to N. As they are very joyful gnomes, they usually send jokes to their friends right after they get any (even if they knew it before) via their social network named as Mybeard. Mybeard became popular in the city because of message auto-deletion. It takes exactly one minute to read and resend joke to mates.

Mayor of Kekocity, Mr. Shaikhinidin, is interested in understanding how the jokes are spread. He gives you database of Mybeard social network, and wants you to answer some queries on it.

You will be given a list of friends for every gnome and M queries of the following type: Who will receive a message with joke after exactly K minutes, if the creator of joke was gnome with id x?

Input

The first line contains a single integer N denoting the number of gnomes.

The next N lines contain the the matrix g[N][N]. Each of the i-th line, will contain N space separated integers - j-th of those will denote g[i][j]. If gnome j is friend of gnome i, then g[i][j] is 1. Otherwise it will be zero. Plese note that the friendship relationship is not bidirectional, i.e. it might happen that g[i][j] may not be equal to g[j][i]. Also one can be friend of itself also, i.e. g[i][i] may be equal to 1.

The next line contains a single integer M denoting the number of queries. The next M lines contain two integers k and x described above.
Output

For each query, output two lines.

In the first line, output how many gnomes will know the joke after k minutes.

In the second line, print these ids (numbering) of these gnomes in increasing order. If no one will know the joke after K minutes, then print -1 in this line.
Constraints

    1 ≤ N ≤ 500
    1 ≤ M ≤ 500
    0 ≤ k ≤ 109
    1 ≤ x ≤ N
    0 ≤ g[i][j] ≤ 1

Subtasks
Subtask #1 : (10 points)

    1 ≤ N ≤ 50
    1 ≤ M ≤ 50
    0 ≤ k ≤ 50


Subtask #2 : (15 points)

    Original constraints
    Every gnome has exactly one friend (for every i there is exactly one j such that g[i][j] = 1. Note that j can be equal to i)


Subtask #3 : (30 points)

    1 ≤ N ≤ 75
    1 ≤ M ≤ 75
    0 ≤ k ≤ 109


Subtask #4 : (45 points)

    Original constraints

Example

Input:

    5
    0 1 0 0 0
    0 0 1 1 0
    1 0 0 0 0
    0 0 0 1 0
    0 0 0 0 0
    4
    3 1
    10000 1
    0 5
    1 5

Output:

    2
    1 4
    2
    2 4
    1
    5
    0
    -1
    
******************************************************************************************************************************

#SOLUTION

    #include <iostream>
    #include <string>
 
    using namespace std;
    int n,b,d,top,y;
    string s[1000];
    string multiply(string g,int **a)
    {
        string f;
        int i,j;
        for(i=0;i<n;i++)
            f+='0';
        for(i=0;i<n;i++)
        {
            if(g[i]=='1')
            {
                for(j=0;j<n;j++)
                {
                    if(a[i][j]==1)
                        f[j]='1';
                }
            }
        }
        return f;
    }
    void dp(string p,int **a)
    {
        int i;
        while(1)
        {
            top++;
            p=multiply(p,a);
            for(i=0;i<top;i++)
            {
                if(p.compare(s[i])==0)
                    break;
            }
            if((y>50)&&(i!=top))
            {
                b=i;
                d=top-i;
                break;
            }
            else
                s[top]=p;
            if(top==y)
                break;
        }
    }   
    void output(string p)
    {
        int c=0,i;
        for(i=0;i<n;i++)
        {
            if(p[i]=='1')
                c++;
        }
        if(c==0)
            cout<<"0\n-1\n";
        else
        {
            cout<<c<<"\n";
            for(i=0;i<n;i++)
            {
                if(p[i]=='1')
                    cout<<i+1<<" ";
            }
            cout<<"\n";
        }
    }
    int main()
    {
        ios_base::sync_with_stdio(false);
        int m,i,j,x;
        cin>>n;
        int **a;
        a=new int*[n];
        for(i=0;i<n;i++)
        {
            a[i]=new int[n];
            for(j=0;j<n;j++)
                cin>>a[i][j];
        }
        cin>>m;
        while(m--)
        {
            cin>>y>>x;
            top=0;
            if(y==0)
                cout<<"1\n"<<x<<"\n";
            else
            {
                for(i=0;i<n;i++)
                {
                    if(i==x-1)
                        s[top]+='1';
                    else
                        s[top]+='0';
                }
                dp(s[top],a);
                /*for(i=0;i<=top;i++)
                    cout<<s[i]<<"\n";*/
                if(top==y)
                    output(s[top]);
                else
                    output(s[b+((y-b)%d)]);
            }
            for(i=0;i<=top;i++)
                s[i].clear();
        }
        return 0;
    }
