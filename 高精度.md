### 高精度加法

~~~c++
#define _CRT_SECURE_NO_WARNINGS
#include<iostream>
#include<algorithm>
using namespace std;
int main()
{
	int  a[1005] = { 0 };
	int  b[1005] = { 0 };
	int  c[1005] = { 0 };
	string s1, s2;
	cin >> s1 >> s2;
	for (int i = 0; i < s1.size(); i++)
		a[i] = s1[s1.size() - i - 1] - '0';//逆序存储
	for (int i = 0; i < s2.size(); i++)
		b[i] = s2[s2.size() - i - 1] - '0';//逆序存储
	int x = 0;//进位
	int len = 0;
	while (len < s1.size() || len < s2.size())
	{
		c[len] = a[len] + b[len] + x;
		x = c[len] / 10;
		c[len] %= 10;
		len++;
	}
	c[len] = x;
	while (c[len] == 0 && len > 0)//删除前导零
		len--;
	for (int i = len; i >= 0; --i)
		cout << c[i];
	return 0;
}
~~~

### 高精度减法

```c++
#define _CRT_SECURE_NO_WARNINGS
#include<algorithm>
#include<iostream>
using namespace std;
int main()
{
	int  a[1005] = { 0 };
	int  b[1005] = { 0 };
	int  c[1005] = { 0 };
	string s1, s2;
	cin >> s1 >> s2;
	if (s1.size() < s2.size() || s1.size() == s2.size() && s1 < s2)//判断大小
		swap(s1, s2), cout << '-';
	for (int i = 0; i < s1.size(); i++)//逆序存储
		a[i] = s1[s1.size() - i - 1] - '0';
	for (int i = 0; i < s2.size(); i++)
		b[i] = s2[s2.size() - i - 1] - '0';//逆序存储
	for (int i = 0; i < s1.size(); i++)
	{
		if (a[i] < b[i])//借位
		{
			a[i + 1]--;
			a[i] += 10;
		}
		c[i] = a[i] - b[i];
	}
	int len = s1.size()-1;
	while (c[len] == 0 && len > 0)//删除前导零
		len--;
	for (int i = len; i >= 0; --i)
		cout << c[i];
	return 0;
}
```

### 高精度乘以单精度

~~~c++
#define _CRT_SECURE_NO_WARNINGS
#include<algorithm>
#include<iostream>
using namespace std;
int main()
{
	int  a[1005] = { 0 };
	string s;
	int n = 0;
	cin >> s >> n;//n不超过10000
	for (int i = 0; i < s.size(); i++)
	{
		a[i] = s[s.size() - i - 1] - '0';
		a[i] *= n;
	}
	for (int i = 0; i < s.size() + 4; i++)
	{
		a[i + 1] += a[i] / 10;
		a[i] %= 10;
	}
	int len = s.size() + 4 - 1;
	while (a[len] == 0 && len > 0)
		len--;
	for (int i = len; i >= 0; i--)
		cout << a[i];
	return 0;
}
~~~



### 高精度乘以高精度

~~~c++
#define _CRT_SECURE_NO_WARNINGS
#include<algorithm>
#include<iostream>
using namespace std;
int main()
{
	int a[245] = { 0 };
	int b[245] = { 0 };
	int c[500] = { 0 };
	string s1, s2;
	cin >> s1 >> s2;
	for (int i = 0; i < s1.size(); i++)
		a[s1.size() - i] = s1[i] - '0';
	for (int i = 0; i < s2.size(); i++)
		b[s2.size() - i] = s2[i] - '0';
	for (int i = 1; i <= s1.size(); i++)//被乘数
	{
		int x = 0;//存放进位
		for (int j = 1; j <= s2.size(); j++)//对乘数的每一位进行处理
		{
			c[i + j - 1] = a[i] * b[i] + x + c[i + j - 1];//当前乘积+上次乘积进位+原数
			x = c[i + j - 1] / 10;
			c[i + j - 1] %= 10;
		}
		c[s2.size() + i] = x;//进位
	}
	int len = s1.size() + s2.size();
	while (c[len] == 0 && len > 1)//删除前导零
		len--;
	for (int i = len; i >= 1; i--)
		cout << c[i];
	return 0;
}
~~~



