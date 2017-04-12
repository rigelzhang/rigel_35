# rigel_35
1101 //buluogeju
#include<iostream>
using namespace std;
#define NSIZE 100
int map[NSIZE][NSIZE];
int tmap[NSIZE][NSIZE];
int flag[NSIZE][NSIZE];
int count[6];
int N;
int prex,prey;
int res;
 
void input()
{
    cin>>N;
    for(int i=0;i<N;++i)
    {
        for(int j=0;j<N;++j)
        {
            cin>>map[i][j];
            flag[i][j] = 0;
        }
    }
 
}
 
void clearflag()
{
    for(int i=0;i<N;++i)
    {
        for(int j=0;j<N;++j)
        {
            flag[i][j] = 0;
        }
    }
}
 
 
void DFS(int i,int j)
{
    if(flag[i][j] == 1 || i<0 || i>= N || j<0 || j>=N)
    {
        return;
    }
 
    if(map[i][j] == 0)
    {
        if(map[prex][prey] == 0)
        {
            //find zero point
            tmap[i][j] = 6;
        }else{
            return;
        }
    }else{
        if(map[i][j] == map[prex][prey] || map[prex][prey] == 0)
        {
            ++count[map[i][j]];
        }else
            return ;
    }
 
    flag[i][j] =1;
    int savex = prex;
    int savey = prey;
    prex = i;
    prey = j;
    DFS(i-1,j);
    DFS(i,j+1);
    DFS(i+1,j);
    DFS(i,j-1);
//  flag[i][j] = 0;
    prex = savex;
    prey = savey;
}
 
int conq()
{
    int index = 1;
    for(int i=2;i<=5;++i)
    {
        if(count[index] <= count[i])
        {
            index = i;
        }
    }
    return index;
}
 
void update(int index)
{
    for(int k= 0;k<N;++k)
    {
        for(int l= 0;l<N;++l)
        {
            if(tmap[k][l] == 6)
            {
                tmap[k][l] = index;
            }
        }
    }
}
 
 
 
 
void output()
{
    for(int i=0;i<N;++i)
    {
        for(int j=0;j<N;++j)
        {
            cout<<flag[i][j]<<" ";
        }
        cout<<endl;
    }
    cout<<endl;
 
    //for(int i=0;i<N;++i)
    //{
    //  for(int j=0;j<N;++j)
    //  {
    //      cout<<tmap[i][j]<<" ";
    //  }
    //  cout<<endl;
    //}
}
 
void merge()
{
    for(int i=0;i<N;++i)
    {
        for(int j=0;j<N;++j)
        {
            if(tmap[i][j] != 0)
            {
                map[i][j] = tmap[i][j];
                tmap[i][j] = 0;
            }
        }
    }
}
 
void DFS1(int i,int j)
{
    if(i<0 || i>= N || j<0||j>=N ||flag[i][j] == 1 || map[i][j] != map[prex][prey]  )
        return ;
    flag[i][j] = 1;
    DFS1(i-1,j);
    DFS1(i,j+1);
    DFS1(i+1,j);
    DFS1(i,j-1);
}
 
void outcount()
{
    for(int i=1;i<=5;++i)
        cout<<count[i]<<" ";
    cout<<endl;
}
     
     //1102 赌气散播
     #include<iostream>
using namespace std;
#define WSIZE 50
#define LSIZE 50
int W,L;
int map[WSIZE][LSIZE];
int flag[WSIZE][LSIZE];
int x,y;
int s;
int prei,prej;
int res;
int qx[2500];
int qy[2500];
int qs[2500];
int index;
 
 
void input()
{
    cin>>W>>L>>x>>y>>s;
    for(int i=0;i<W;++i)
    {
        for(int j=0;j<L;++j)
        {
            cin>>map[i][j];
            flag[i][j] = 0;
        }
    }
}
 
int canspread(int i,int j)
{
    if(i < 0 || i>=W || j<0 || j>=L || map[i][j] <=0)
        return 0;
    if(prei == -1 && prej == -1)
        return 1;
    switch(map[prei][prej])
    {
    case 1:
        if(prei == i)
        {
            if(prej < j)//left
            {
                if(map[i][j] == 1 || map[i][j] == 3 || map[i][j] == 6 || map[i][j] == 7 )
                    return 1;
                else
                    return 0;
            }else{//right
                if(map[i][j] == 1 ||map[i][j] == 3 || map[i][j] == 4 || map[i][j] == 5 )
                    return 1;
                else
                    return 0;
            }
        }else
        {
            if(prei < i)//up
            {
                if(map[i][j] == 1 ||map[i][j] == 2 || map[i][j] == 4 || map[i][j] == 7 )
                    return 1;
                else
                    return 0;
            }else{
                //down
                if(map[i][j] == 1 ||map[i][j] == 2 || map[i][j] == 5 || map[i][j] == 6 )
                    return 1;
                else
                    return 0;
            }
        }
        break;
    case 2:
        if(prei == i)
        {
            return 0;
        }else
        {
            if(prei < i)//up
            {
                if(map[i][j] == 1 ||map[i][j] == 2 || map[i][j] == 4 || map[i][j] == 7 )
                    return 1;
                else
                    return 0;
            }else{
                //down
                if(map[i][j] == 1 || map[i][j] == 2 || map[i][j] == 5 || map[i][j] == 6 )
                    return 1;
                else
                    return 0;
            }
        }
        break;
    case 3:
        if(prei == i)
        {
            if(prej < j)//left
            {
                if(map[i][j] == 1 || map[i][j] == 3 || map[i][j] == 6 || map[i][j] == 7 )
                    return 1;
                else
                    return 0;
            }else{//right
                if(map[i][j] == 1 ||map[i][j] == 3 || map[i][j] == 4 || map[i][j] == 5)
                    return 1;
                else
                    return 0;
            }
        }else
        {
            return 0;
        }
        break;
    case 4:
        if(prei == i)
        {
            if(prej < j)//left
            {
                if(map[i][j] == 1 || map[i][j] == 3 || map[i][j] == 6 || map[i][j] == 7 )
                    return 1;
                else
                return 0;
            }else{//right
                    return 0;
            }
        }else
        {
            if(prei < i)//up
            {
                    return 0;
            }else{
                //down
                if(map[i][j] == 1 ||map[i][j] == 2 || map[i][j] == 5 || map[i][j] == 6 )
                    return 1;
                else
                return 0;
            }
        }
        break;
    case 5:
        if(prei == i)
        {
            if(prej < j)//left
            {
                if(map[i][j] == 1 ||map[i][j] == 3 || map[i][j] == 6 || map[i][j] == 7)
                    return 1;
                else
                return 0;
            }else{//right
                    return 0;
            }
        }else
        {
            if(prei < i)//up
            {
                if(map[i][j] == 1 ||map[i][j] == 2 || map[i][j] == 4 || map[i][j] == 7 )
                    return 1;
                else
                return 0;
            }else{
                //down
                    return 0;
            }
        }
        break;
    case 6:
        if(prei == i)
        {
            if(prej < j)//left
            {
                    return 0;
            }else{//right
                if(map[i][j] == 1 ||map[i][j] == 3 || map[i][j] == 4 || map[i][j] == 5 )
                    return 1;
                else
                return 0;
            }
        }else
        {
            if(prei < i)//up
            {
                if(map[i][j] == 1 ||map[i][j] == 2 || map[i][j] == 4 || map[i][j] == 7 )
                    return 1;
                else
                return 0;
            }else{
                //down
                    return 0;
            }
        }
        break;
    case 7:
        if(prei == i)
        {
            if(prej < j)//left
            {
                    return 0;
            }else{//right
                if(map[i][j] == 1 ||map[i][j] == 3 || map[i][j] == 4 || map[i][j] == 5 )
                    return 1;
                else
                return 0;
            }
        }else
        {
            if(prei < i)//up
            {
                    return 0;
            }else{
                //down
                if(map[i][j] == 1 ||map[i][j] == 2 || map[i][j] == 5 || map[i][j] == 6 )
                    return 1;
                else
                return 0;
            }
        }
        break;
    default: break;
    }
    return 0;
}
 
void bfs()
{
    int tx,ty,ts;
    int i =0;
    while(i<index)
    {
        tx= qx[i] ;
        ty = qy[i];
        ts = qs[i];
        prei = tx;
        prej = ty;
        ++i;
        ++res;
        if(ts <= 1)
             continue;
        if( flag[tx-1][ty] == 0 && canspread(tx-1,ty))
        {
            qx[index] = tx-1;
            qy[index] = ty;
            qs[index] = ts -1;
            ++index;
            flag[tx-1][ty] =1;
        };
 
        if(flag[tx][ty+1] == 0 && canspread(tx,ty+1))
        {
            qx[index] = tx;
            qy[index] = ty+1;
            qs[index] = ts -1;
            ++index;
            flag[tx][ty+1] = 1;
        };
 
        if(flag[tx+1][ty] == 0 && canspread(tx+1,ty))
        {
            qx[index] = tx+1;
            qy[index] = ty;
            qs[index] = ts -1;
            ++index;
            flag[tx+1][ty] = 1;
        };
 
        if(flag[tx][ty-1] == 0 && canspread(tx,ty-1))
        {
            qx[index] = tx;
            qy[index] = ty-1;
            qs[index] = ts -1;
            ++index;
            flag[tx][ty-1] = 1;
        };
    }
}
 
 
int main()
{
    int T;
    //freopen("D:\\1062.txt","r",stdin);
    cin>>T;
    for(int i=1;i<=T;++i)
    {
        input();
        res = 0;
        prei = -1;
        prej = -1;
        qx[0] = x;
        qy[0] = y;
        qs[0] = s;
        index=1;
        flag[x][y] =1;
        bfs();
        cout<<"#"<<i<<" "<<res<<endl;
    }
 
    return 0;
}
//青蛙找伙伴
#include<iostream>
using namespace std;
#define NSIZE (50)
int N,M;
int map[NSIZE][NSIZE];
int res;
int findans;
int x[NSIZE*NSIZE];
int y[NSIZE*NSIZE];
int start,tail;
 
void input()
{
    cin>>N>>M;
    for(int i=0;i<N;++i)
    {
        for(int j =0;j<M;++j)
        {
            cin>>map[i][j];
            if(map[i][j] == 2)
            {
                x[0] = i;
                y[0] = j;
            }
        }
    }
}
 
void add(int i,int j)
{
    if(i<0 || i>= N || j<0 || j>=M ||map[i][j] == 0 || map[i][j] == 4)
    {
        return;
    }else if (map[i][j] == 3)
    {
        findans = 1;
        return;
    }else if(map[i][j] == 1 )
    {
        map[i][j] = 4;
        x[tail] = i;
        y[tail] = j;
        ++tail;
    }
    return;
}
 
void bfs()
{
    int end = tail;
    while(start<end)
    {
        add(x[start],y[start]-1);
        add(x[start],y[start]+1);
 
        for(int i=0;i<=res;++i)
        {
            add(x[start]-i,y[start]);
            add(x[start]+i,y[start]);
        }
        ++start;
        end = tail;
        if(findans)
            return;
        if(start >= end)
        {
            start = 0;
            end = tail;
            ++res;
        }
    }
}
 
int main()
{
    int T;
    //freopen("D:\\1066.txt","r",stdin);
    cin>>T;
    for(int i=1;i<=T;++i)
    {
        input();
        res = 0;
        findans = 0;
        start = 0;
        tail = 1;
        bfs();
        cout<<"#"<<i<<" "<<res<<endl;
    }
    return 0;
}
 
/**************************************************************
    Problem: 1066
    User: dengfangwen
    Language: C++
    Result: 正确
    Time:172 ms
    Memory:1704 kb
****************************************************************/
//1068 修剪草坪
#include<iostream>
#include<iomanip>
using namespace std;
#define KSIZE 100
int sx[KSIZE];
int sy[KSIZE];
int ex[KSIZE];
int ey[KSIZE];
int K;
 
void input()
{
    cin>>K;
    sx[0] =0;
    sy[0] = 0;
    ex[0] =0;
    ey[0] =0;
    int d,l;
    cin>>d>>l;
    switch(d)
    {
    case 1:ey[0] += l;break;
    case 2:ey[0] -= l;break;
    case 3:ex[0]+= l;break;
    case 4:ex[0]-= l;break;
    default:break;
    }
 
    for(int i=1;i<K;++i)
    {
        sx[i] = ex[i-1];
        sy[i] = ey[i-1];
        ex[i] = sx[i];
        ey[i] = sy[i];
        cin>>d>>l;
        switch(d)
        {
        case 1:ey[i] += l;break;
        case 2:ey[i] -= l;break;
        case 3:ex[i]+= l;break;
        case 4:ex[i]-= l;break;
        default:break;
        }
    }
}
 
void output()
{
    for(int i=0;i<K;++i)
    {
        cout<<"line:"<<setw(5)<<sx[i]<<setw(5)<<sy[i] <<setw(5)<<ex[i] <<setw(5)<<ey[i] <<endl;
    }
}
 
int cross(int i,int j)
{
    if(sx[i] == ex[i]  && sx[j] == ex[j] && sx[i] == sx[j] )//all x same
    {
        int sy1,ey1,sy2,ey2;
        sy1 = sy[i] > ey[i] ? ey[i]:sy[i];
        ey1 = sy[i] >ey[i] ? sy[i] :ey[i];
        sy2 = sy[j] > ey[j] ? ey[j]:sy[j];
        ey2 = sy[j] >ey[j] ? sy[j] :ey[j];
 
        if(sy2 < ey1 && ey2  > sy1)
            return 1;
    }
 
    if(sy[i] == ey[i]  && sy[j] == ey[j] && sy[i] == sy[j] )//all y same
    {
        int sx1,ex1,sx2,ex2;
        sx1 = sx[i] > ex[i] ? ex[i]:sx[i];
        ex1 = sx[i] >ex[i] ? sx[i] :ex[i];
        sx2 = sx[j] > ex[j] ? ex[j]:sx[j];
        ex2 = sx[j] >ex[j] ? sx[j] :ex[j];
 
        if(sx2 < ex1 && ex2  > sx1)
            return 1;
    }
 
    if(ey[i] == sy[i] && sx[j] ==ex[j] )
    {
        int startx,endx,midx;
        int starty,endy,midy;
 
        startx = sx[i] < ex[i] ? sx[i] :ex[i];
        endx = sx[i] >ex[i] ? sx[i] :ex[i];
        midx = sx[j];
 
        starty = sy[j] < ey[j] ? sy[j] : ey[j];
        endy = sy[j] > ey[j] ? sy[j] : ey[j];
        midy = sy[i];
 
        if(midx < endx && midx > startx && midy <endy && midy >starty)
            return 1;
        else
            return 0;
    }
 
    if(ey[j] == sy[j] && ex[i] == sx[i] )
    {
        int startx,endx,midx;
        int starty,endy,midy;
 
        startx = sx[j] < ex[j] ? sx[j] :ex[j];
        endx = sx[j] >ex[j] ? sx[j] :ex[j];
        midx = sx[i];
 
        starty = sy[i] < ey[i] ? sy[i] : ey[i];
        endy = sy[i] > ey[i] ? sy[i] : ey[i];
        midy = sy[j];
 
        if(midx < endx && midx > startx && midy <endy && midy >starty)
            return 1;
        else
            return 0;
    }
    return 0;
}
 
int cal(int n)
{
    for(int i=0;i<n;++i)
    {
        if(cross(i,n))
            return 1;
    }
    return 0;
}
 
int main()
{
    int T;
    //freopen("D:\\1068.txt","r",stdin);
    cin>>T;
    for(int li = 1;li<=T;++li)
    {
        input();
        //output();
        int i;
        for(i=0;i<K;++i)
        {
            if(cal(i))
                break;
        }
        cout<<"#"<<li<<" ";
        if(i>=K)
        {
            cout<<-1<<endl;
        }else{
            cout<<i+1<<endl;
        }
    }
    return 0;
}
 
/**************************************************************
    Problem: 1068
    User: dengfangwen
    Language: C++
    Result: 正确
    Time:8 ms
    Memory:1680 kb
****************************************************************/
//1088 supply route
 In the 2nd World War, the battle between the Allied Forces and the German troops are getting fiercer. Many parts of the roads in the region where the battle is taking place are damaged. As seen in the figure 1(a), vehicles such as trucks and tanks cannot use the roads due to massive bombings and street battle. To win the battle, there must be roads on which Armored Division and Supply Unit move promptly.

The Corps of Engineers will do the road repair work within a short amount of time so that the travel can be possible from the starting place(S) to the arrival place(G). The repair time increases in proportion to the depth by which the roads are damaged. Find the total repair time for the path with the shortest repair time among the paths from the starting place to the arrival place. Assume if the depth is 1, 1 hour is needed for repair work.

Map information is represented in the form of two-dimensional array as seen in the figure 1(b).  The starting point is section S in the upper left corner, and the arrival place is section G in the lower right corner. Movement can be made in up, down, left, and right directions, and it can be made by one section. For map information, the depth by which the roads are damaged is given in each section. Movement to another section is possible only after repair of the current section is completed.

 

Assume it takes much more time to repair the roads compared to the time needed for moving. Therefore, you do not need to consider the distance from the starting place to the arrival place.

The map information, as seen in the figure 2, has two-dimensional array format. The starting place(S) and arrival place(G) are in the upper left and lower right side respectively, and are represented as 0 in input data. Sections represented as 0 other than the starting and arrival places do not need repair work.

 

In the map below, the minimum time for repair work is 2 and the grey area will be the path.

输入
10 test cases are given continuously through standard input.  

The size of the map(N x N) is given for each test case. The maximum size of the map is 100 x 100.

From the next line, map information in the form of two-dimensional array is given.
输出
Print answers for each of the test cases in order, and print “#C” at start of line for each test case with C being the case number.

Leave a blank space in the same line, and print out the repair time of the path with the shortest repair time among the paths from the starting place to the arrival place.   

#include<iostream>
using namespace std;
#define NSIZE 100
int map[NSIZE][NSIZE];
int flag[NSIZE][NSIZE];
int N;
int tx[NSIZE*NSIZE];
int ty[NSIZE*NSIZE];
int tc;
 
void input()
{
    unsigned char ch;
    cin>>N;
    for(int i=0;i<N;++i)
    {
        for(int j=0;j<N;++j)
        {
            cin>>ch;
            map[i][j] = ch - 0x30;
            flag[i][j] =0;
        }
    }
}
 
void output()
{
    cout<<"matrix:"<<endl;
    for(int i=0;i<N;++i)
    {
        for(int j=0;j<N;++j)
            cout<<map[i][j]<<" ";
        cout<<endl;
    }
    cout<<"flag:"<<endl;
    for(int i=0;i<N;++i)
    {
        for(int j=0;j<N;++j)
            cout<<flag[i][j]<<" ";
        cout<<endl;
    }
}
 
void outputflag()
{
    cout<<"flag:"<<endl;
    for(int i=0;i<N;++i)
    {
        for(int j=0;j<N;++j)
            cout<<flag[i][j]<<" ";
        cout<<endl;
    }
 
}
 
void cal()
{
     
    for(int k=1;k<N*N;++k)
    {
        //output();
        int tm = 1000000000;
        int ti=0,tj=0;
        for(int l= 0;l<tc;++l)
        {
            int i = tx[l];
            int j = ty[l];
            if( i-1 >0 && flag[i-1][j] == 0)
            {
                if(tm > map[i-1][j]+map[i][j])
                {
                    tm = map[i-1][j]+map[i][j];
                    ti = i-1;
                    tj = j;
                }
            }
 
            if( i+1 < N && flag[i+1][j] ==0)
            {
 
                if(tm > map[i+1][j] +map[i][j] )
                {
                    tm = map[i+1][j] +map[i][j];
                    ti = i+1;
                    tj = j;
                }
            }
 
            if( j-1 >0 && flag[i][j-1] == 0)
            {
                if(tm > map[i][j-1]+map[i][j])
                {
                    tm = map[i][j-1]+map[i][j];
                    ti = i;
                    tj = j-1;
                }
            }
 
            if( j+1 < N && flag[i][j+1] ==0)
            {
 
                if(tm > map[i][j+1]+map[i][j])
                {
                    tm =map[i][j+1]+map[i][j];
                    ti = i;
                    tj = j+1;
                }
            }
        }
        flag[ti][tj] = 1;
        map[ti][tj] = tm;
        tx[tc]= ti;
        ty[tc] = tj;
        tc++;
    }
}
     
 
 
int main()
{
    int T;
    //freopen("D:\\1088.txt","r",stdin);
    cin>>T;
    for(int li = 1;li<=T;++li)
    {
        input();
        tx[0] =0 ;
        ty[0] = 0;
        tc=1;
        flag[0][0] = 1;
        cal();
        //output();
        cout<<"#"<<li<<" ";
        cout<<map[N-1][N-1]<<endl;
    }
    return 0;
}
/**************************************************************
    Problem: 1088
    User: dengfangwen
    Language: C++
    Result: 正确
    Time:2660 ms
    Memory:1836 kb
****************************************************************/
//1089 hanaro
 You are going to take charge of ‘Hanaro’ – the project to design a transport system that connects N islands within Indonesia. The Hanaro project aims to reduce obstacles caused by poor connection among the islands since they undermine the development of Indonesian tourism industry, thereby creating added values. The goal of this project is to connect all the islands within Indonesia through underwater tunnels.

Underwater tunnels must connect two islands with a line segment and even if two tunnels intersect, it is assumed the two tunnels are not connected physically (In the case of figure 1 below, even though island A and island D are connected, the crossing two tunnels are considered as “not connected” since it is not possible to reach from island A to island B, or to island C.  

 

In the following two cases, all islands are connected.

 
 

You should connect the all islands within Indonesia using the methods above.

As shown in figure 3, there are cases where islands are connected directly as is the case with island B and island A, but there are also cases where islands are connected indirectly through several islands as is the case with island B and C.

The government of Indonesia has a policy as follows that makes it mandatory to pay pollution charges for environmental damage caused by the construction of underwater tunnels.

- Amount of payment: Pollution tax rate (E) x square of underwater tunnel length (L) = (E * L2)

Design a transport system that can connect all N islands while minimizing the total amount of pollution charges.

If variables are not defined as 64 bit integer or double, overflow could take place.

(In C/C++, a 64 bit integer is declared as long long.)

(You can see that all islands are connected by minimizing pollution charges in figure 2 above, but it is not the case for figure 3.)

 
输入
 

The number of test cases K is given.

For each test case,  

In the first line , the number of islands N is given (1≤N≤1,000).

In the second line, coordinates of x – the integers of each island- are given. In the third line, coordinates of y – the integers of each island- are given. (0≤X≤1,000,000, 0≤Y≤1,000,000)

Lastly, a real number E – pollution tax rate for underwater tunnel construction – is given. (0≤E≤1)
输出
 

Print answers for each of the test cases through standard input and print “#C” at start of line for each test case with C being the case number. In the same line, leave a blank space and print the minimum pollution charge for connecting all islands in the given input by rounding off to the nearest ones place in the form of integer.
样例输入

3
2
0 0
0 100
1.0
4
0 0 400 400
0 100 0 100
1.0 
6
0 0 400 400 1000 2000
0 100 0 100 600 2000
0.3

样例输出

#1 10000
#2 180000
#3 1125000

代码
#include<iostream>
#include<iomanip>
using namespace std;
#define NSIZE 1000
double px[NSIZE];
double py[NSIZE];
int N;
double d[NSIZE][NSIZE];
 
int ti[NSIZE];
int tc;
double gd;
double e;
int visit[NSIZE];
 
void input()
{
    cin>>N;
    for(int i=0;i<N;++i)
    {
        cin>>px[i];
        visit[i] =0 ;
    }
 
    for(int i=0;i<N;++i)
    {
        cin>>py[i];
    }
 
    cin>>e;
 
    for(int i=0;i<N;++i)
    {
        for(int j=i+1;j<N;++j)
        {
            d[i][j] = (px[i] -px[j])*(px[i] -px[j]) + (py[i]-py[j] )* (py[i]-py[j] );
            d[j][i] = d[i][j];
        }
    }
    int start=0,end=0;
    double td = 10e100;
    for(int i=0;i<N;++i)
    {
        for(int j= i+1;j<N;++j)
        {
            if(td>d[i][j])
            {
                td = d[i][j];
                start = i;
                end = j;
            }
        }
    }
    ti[0]= start;
    ti[1]= end;
    visit[start]=1;
    visit[end] =1;
    tc =2;
    gd =0;
    gd += td;
}
 
void cal()
{
    for(int i=2;i<N;++i)
    {
        int add= 0;
        double td = 10e100;
        for(int j=0;j<tc;++j)
        {
            int k= ti[j];
            for(int l =0;l<N;++l)
            {
                if(visit[l] ==0  && k!= l && td>d[k][l])
                {
                    td = d[k][l];
                    add = l;
                }
            }
        }
        visit[add] = 1;
        ti[tc] = add;
        tc++;
        gd += td;
    }
}
 
void output()
{
    cout<<"the distance between two points:"<<endl;
    for(int i=0;i<N;++i)
    {
        for(int j =0;j<N;++j)
        {
            cout<<setw(10)<<d[i][j];
        }
        cout<<endl;
    }
}
int main()
{
    int T;
    //freopen("D:\\1089.txt","r",stdin);
    cin>>T;
    for(int li=1;li<=T;++li)
    {
        input();
        //output();
        cal();
        long long temp = e*gd;
        if(e*gd - temp >= 0.5)
            ++temp;
        cout<<"#"<<li<<" "<<temp<<endl;
    }
    return 0;
}
/**************************************************************
    Problem: 1089
    User: dengfangwen
    Language: C++
    Result: 正确
    Time:4332 ms
    Memory:9512 kb
**********************************
1103 愚公移山
 愚公家门前有多座大山挡着路，他决心把山平掉，另一个“聪明”的智叟笑他太傻， 认为不能。愚公说：“我死了有儿子，儿子死了还有孙子，子子孙孙无穷无尽的，又何必担心挖不平呢？”

然而他的子孙可不想陪他玩。为了说服愚公放弃他的移山大计， 他们要估算出山的体积, 说明山体何其庞大， 移到世界末日都移不完


图中 0表示 平原， 1表示 山体.

某个位置的山体高度等于它离平原的最短路径长度（平面距离， 只能算前后左右四个方向）



上图的例子， 红色框所在的山体位置离平原的最短路是2 ，所以该位置的高度就是2


现在给出平面地图(地图边缘一定为平原)， 请求出地图中所有山体的体积总和
已知： 山体高度总和等于山体的体积总和
输入

第一行给定测试用例个数T，接下来T组数据

每组数据第一行为N，代表地图大小为 N*N (N <= 100)

接下来是 N*N的地图信息
输出
输出每个 case 的山体的体积总和
样例输入

2
6
0 0 0 0 0 0
0 0 1 1 0 0
0 1 1 1 1 0
0 1 1 1 1 0
0 0 1 0 0 0
0 0 0 0 0 0
8
0 0 0 0 0 0 0 0
0 1 1 1 1 0 1 0
0 1 1 1 1 0 1 0
0 1 1 1 1 0 1 0
0 1 1 1 1 1 1 0
0 1 0 1 1 1 1 0
0 0 0 1 1 1 1 0
0 0 0 0 0 0 0 0

样例输出

#1 14
#2 38
#include<iostream>
using namespace std;
#define NSIZE 100
int N;
int map[NSIZE][NSIZE];
int x[NSIZE*NSIZE];
int y[NSIZE*NSIZE];
int r[NSIZE*NSIZE];
int start;
int tail;
int flag[NSIZE][NSIZE];
int gv;
 
void input()
{
    cin>>N;
    for(int i=0;i<N;++i)
    {
        for(int j=0;j<N;++j)
            cin>>map[i][j];
    }
}
 
int cal()
{
    int res = 0;
    for(int i=0;i<N;++i)
    {
        for(int j=0;j<N;++j)
            res += map[i][j];
    }
    return res;
}
 
void add(int i,int j,int v)
{
    if(i<0 || i>=N || j<0 || j>=N  || flag[i][j] == 1)
        return;
    if(map[i][j] == 0)
    {
        gv = v;
    }
    flag[i][j] = 1;
    x[tail] = i;
    y[tail] = j;
    r[tail] = v;
    ++tail;
}
 
void bfs()
{
    while(start < tail)
    {
        int i = x[start];
        int j = y[start];
        int v = r[start];
        ++start;
 
        add(i-1,j,v+1);
        add(i,j+1,v+1);
        add(i+1,j,v+1);
        add(i,j-1,v+1);
        if(gv > 0)
            break;
    }
 
    for(int i=0;i<tail;++i)
    {
        flag[x[i]][y[i]] = 0;
    }
    tail = 0;
}
 
int main()
{
    int T;
    //freopen("D:\\1103.txt","r",stdin);
    cin>>T;
    for(int i=1;i<=T;++i)
    {
        input();
        for(int j= 0;j<N;++j)
        {
            for(int k=0;k<N;++k)
            {
                if(map[j][k] == 0)
                    continue;
                x[tail] = j;
                y[tail] = k;
                r[tail] = 0;
                tail++;
                start = 0;
                gv = 0;
                bfs();
                map[j][k] = gv;
            }
        }
        cout<<"#"<<i<<" "<<cal()<<endl;
 
    }
    return 0;
}
 
 
/**************************************************************
    Problem: 1103
    User: dengfangwen
    Language: C++
    Result: 正确
    Time:108 ms
    Memory:1872 kb
****************************************************************/
