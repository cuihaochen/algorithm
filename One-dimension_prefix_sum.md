~~~c++
#include<iostream>                                           
using namespace std;
int main()
{
	const int N=1e5+5;
	int a[N]={0};int sum[N]={0};
    	int n,m;
    	cin>>n>>m;
    	for(int i=1;i<=n;i++)
    	{
    	cin>>a[i];
    	sum[i]=sum[i-1]+a[i];
    	}
    	while(m--)
    	{
    	int l,r;
    	cin>>l>>r;
    	cout<<sum[r]-sum[l-1]<<endl;
    	}
    	return 0;
}

~~~

