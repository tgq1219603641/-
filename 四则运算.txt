对于这个程序，我只能写出整数，分数的运行和判断对错，支持多个运算符。但是对于累计分数，倒计时，支持括号，用户界面由用户选择用中文英文或日文的问题还不能解决。
希望大神赐教，完善我的程序！！！




#define _CRT_SECURE_NO_WARNINGS


#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <time.h>
#include <conio.h>//控制台输入输出
#include <math.h>

int cnt1, cnt2;
int gcd(int a, int b)//最大公约数
{
	if (b == 0)
		return a;
	return gcd(b, a % b);
}

int main(int argc, char const *argv[])//* argv[ ]: 字符串数组,用来存放指向你的字符串参数的指针数组,每一个元素指向一个参数

argv[0]:指向程序的全路径名
{
	int n = 0;
	for (int i = 0; i < strlen(argv[2]); i++) {
		n = n * 10 + (argv[2][i] - '0');
	}
	printf("%d\n", n);
	srand(time(NULL));
	char input[100], ans1[100], ans2[100];
	while (n--) {
		memset(input, 0, sizeof(input));//memset函数用来对一段内存空间全部设置为某个字符，常用于内存空间初始化。
		memset(ans1, 0, sizeof(ans1));
		memset(ans2, 0, sizeof(ans2));
		fflush(stdin);                  //清除文件缓冲区，文件以写方式打开时将缓冲区内容写入文件
		printf("输入q退出,按其他任意键继续\n");
		char ch = getch();
		if (ch == 'q') {
			break;
		}
		int a, b, c, d, op;
		a = rand() % 100;
		while (1) {
			b = rand() % 100;
			if (b != 0) {
				break;
			}
		}
		c = rand() % 100;
		while (1) {
			d = rand() % 100;
			if (d != 0) {
				break;
			}
		}
		op = rand() % 4;

		int tmp = abs(gcd(a, b));//abs描述 返回数字的绝对值
		a /= tmp;
		b /= tmp;

		tmp = abs(gcd(c, d));
		c /= tmp;
		d /= tmp;


		printf("%d", a);
		if (b != 1) {
			printf("/%d", b);
		}
		if (op == 0) printf(" + ");//op是一种二目运算符的简便用法
		else if (op == 1) printf(" - ");
		else if (op == 2) printf(" * ");
		else printf(" / ");

		printf("%d", c);
		if (d != 1) {
			printf("/%d", d);
		}
		printf(" = ");

		int m, n;
		if (op == 0){
			m = a * d + b * c;
			n = b * d;
		}
		else if (op == 1) {
			m = a * d - b * c;
			n = b * d;
		}
		else if (op == 2) {
			m = a * c;
			n = b * d;
		}
		else {
			m = a * d;
			n = b * c;
		}

		tmp = abs(gcd(m, n));
		m /= tmp;
		n /= tmp;


		sprintf(ans1, "%d", m);
		if (n != 1) {
			sprintf(ans2, "/%d", n);
		}
		strcat(ans1, ans2);

		gets(input);
		puts(ans1);
		if (strcmp(ans1, input) == 0) {
			printf("right\n");
			cnt1++;
		}
		else {
			printf("wrong\n");
			cnt2++;
		}

	}
	int zql;
	zql = (100 * cnt1) / (cnt1 + cnt2);
	printf("共答了%d道题，答对%d道题，答错%d道题,正确率为%d%%。\n", cnt1 + cnt2, cnt1, cnt2, zql);
	return 0;
}