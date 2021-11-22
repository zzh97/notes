### C语言复习笔记
#### 1 HelloWorld
##### （1）基本格式
```
// 导入头文件（标准输入输出库） 
# include <stdio.h>
// 程序主入口 （程序从这里开始执行） 
int main (void) {
	// 格式化输出（这是上方头文件里的一个函数）"\n"表示换行 
	printf ("Hello World\n");
	// 返回值 = 0（表示程序正常结束） 
	return 0;
}
```
##### （2）输入与输出
```
# include <stdio.h>
int main (void) {
	// 声明一个整型变量a 
	int a;
	// 等待用户输入（输入一个十进制数，传给a） 
	scanf("%d", &a);
	// 把a以十进制的方式输出 
	printf ("%d\n", a);
	return 0;
}
```
##### （3）宏定义
```
# include <stdio.h>
// 自定义输出函数（宏定义）相当于一种语法糖 
# define put(a) printf(a)
int main (void) {
	// 使用它，效果和printf("hello world\n");一样 
	put("hello world\n");
	return 0;
}
```
进阶版
```
# include <stdio.h> 
# define put(a) printf("%s\n", a);
int main (void) {
	put("hello world")
	return 0;
}
```
类型定义
```
# include <stdio.h>
// 给int取个别名，叫myInt 
typedef int myInt; 
int main(void) {
	// 使用myInt来定义变量 
	myInt a = 5;
	printf ("%d\n", a);
	return 0;
}
```
#### 2 变量与常量
##### （1）声明与定义
```
# include <stdio.h> 
int main (void) {
	// 定义一个整型变量a，其值为1 
	int a = 1;
	// 定义一个整型常量b，其值为2
	const int b = 2;
	// 输出二者 
	printf("a=%d, b=%d\n", a, b);
	// 更改a的值 
	a = 3;
	// b = 4; 因为b是常量，所以不能更改
	printf("a=%d, b=%d\n", a, b);
	// 声明一个整型变量c 
	int c;
	// 设置c的值为5 
	c = 5;
	// 输出c 
	printf("c=%d\n", c);
	return 0;
}
```
##### （2）数据类型
```
# include <stdio.h> 
int main (void) {
	// 整型 
	int a = 1;
	// 长整型 
	long b = 9999999;
	// 字符型 
	char c = 'c';
	// 单精度（短的小数） 
	float d = 1.1;
	// 双精度（长的小数） 
	double f = 9999.99;
	// %d表示十进制，%c表示字符，%f表示小数，%.2f表示保留两位小数 
	printf("%d, %d, %c, %.2f, %.2f\n", a, b, c, d, f); 
	return 0;
}
```
显式转换（强制转换）和隐式转换
```
# include <stdio.h> 
int main (void) { 
	// 隐式转换（1.1变成1） 
	int a = 1.1;
	printf("%d\n", a); 
	float b = 1.1;
	// 强制转换（float变成int） 
	printf("%d\n", int(b)); 
	return 0;
}
```
##### （3）作用域
```
# include <stdio.h> 
// 全局变量 
int a = 1;
int main (void) { 
	printf("a = %d\n", a);
	// 局部变量 
	int b = 2;
	printf("b = %d\n", b);
	{
		// 更局部的变量 
		int c = 3;
		printf("c = %d\n", c);
	}
	return 0;
}
```
在C语言中，用块来划分作用域
内层可调用外层定义的内容，反之不可
```
// 最外层
{
	// 中间层
	{
		{
			// 最内层
		}
	}
}
```
#### 3 流程控制
##### （1）跳转语句
```
# include <stdio.h> 
int main (void) { 
	// 跳转到a处 
	goto a;
	printf ("这是一");
a:
	printf ("这是二");
	return 0;
}
```
##### （2）分支语句
```
# include <stdio.h> 
int main (void) {
	int a;
	printf("请输出一个整数\n"); 
	scanf("%d", &a);
	if (a > 5) {
		// 当if中条件成立，执行 
		printf("您输入的这个整数大于5\n");
	} 
	else {
		// 当if中条件不成立，执行 
		printf("您输入的这个整数不大于5\n");
	}
	return 0;
}
```
注：C语言中没有elseif，VB中有elseif，C语言中的elseif其实是else if（也就是说，是在else中套if）
```
# include <stdio.h> 
int main (void) {
	int a;
	printf("请输出一个整数\n"); 
	scanf("%d", &a);
	switch (a) {
		case 1:
			printf("您输入的数是1\n");
			break;
		case 2:
			printf("您输入的数是2\n");
			break;
		default:
			printf("您输入的数既不是1也不是2\n");
			break;
	}
	return 0;
}
```
注：与VB一样，C语言中的switch不能匹配字符串，不同的是它还不能判断范围
##### （3）循环语句
while（先判断后执行）
```
# include <stdio.h> 
int main (void) { 
	int a = 1;
	// 当条件（a < 10）成立时，进入循环 
	while (a < 10) {
		printf ("%d\n", a);
		// 自增，相当于a = a + 1 
		a++;
	}
	return 0;
}
```
do...while（先执行后判断）
```
# include <stdio.h> 
int main (void) { 
	int a = 1;
	// 先执行一遍
	do {
		printf ("%d\n", a);
		a++;
	// 当条件（a < 10）成立时，进入循环 
	} while (a < 10);
	return 0;
}
```
for循环
```
# include <stdio.h> 
int main (void) {
	// （初始值，条件，变化）
	for (int i=1; i<10; i++){
		printf("%d\n", i);
	} 
	return 0;
}
```
#### 4 数组
##### （1）定义与遍历
```
# include <stdio.h> 
int main (void) { 
	// 定义整型数组a，最多能存5个元素，分别存了1~5
	int a[5] = {1, 2, 3, 4, 5};
	// 遍历数组（打印数组中所有元素） 
	for (int i=0; i<5; i++){
		printf("a[%d] = %d\n", i, a[i]);
	}
	// "hello"是5个char，可这里用了6个，因为字符串结尾默认有一个结束符（'\0'） 
	char s[6] = "hello";
	printf("%s", s);
	return 0;
}
```
##### （2）二维数组
```
# include <stdio.h> 
int main (void) { 
	// 定义5行6列的二维数组 
	int a[5][6] = {
		{1, 2, 3, 4, 5, 6},
		{7, 8, 9, 10, 11, 12},
		{13, 14, 15, 16, 17, 18},
		{19, 20, 21, 22, 23, 24},
		{25, 26, 27, 28, 29, 30}
	};
	// 遍历数组
	for (int i=0; i<5; i++){
		for (int j=0; j<6; j++)
		printf("a[%d][%d] = %d\n", i, j, a[i][j]);
	}
	return 0;
}
```
##### （3）枚举
```
# include <stdio.h> 
int main (void) { 
	// 定义枚举类Week，并声明一个该类变量week
	enum Week {
		// 设置M=1后，下面的会依次类推，如T=2，W=3... 
		Monday = 1,
		Tuesday,
		Wednesday,
		Thursday,
		Friday,
		Saturday,
		Sunday 
	} week;
	// 设置Week的值（只能在Week中选） 
	week = Thursday;
	// 定义一个Week类的变量one 
	enum Week one = Monday;
	printf("%d\t%d", week, one);
	return 0;
}
```
##### （4）数组名
```
# include <stdio.h> 
int main (void) { 
	int a[5] = {1, 2, 3, 4, 5};
	// 打印数组名与数组首地址（相同） 
	printf("a=%d, &a[0]=%d\n", a, &a[0]);
	// 打印二者的长度（不同），前者是整个数组的长度，后者是首元素的长度
	printf("a=%d, &a[0]=%d\n", sizeof(a), sizeof(&a[0]));
	return 0;
}
```
注：数组名a在大多数情况下，几乎等价于&a
#### 5 函数
##### （1）定义与调用
```
# include <stdio.h> 
// 定义幂函数 
int fun (int a, int n) {
	int c = a;
	for (int i=1; i<n; i++) {
		c = c * a;
	}
	return c;
};
int main (void) { 
	// 调用幂函数 
	printf("%d\n", fun (3, 3));
	return 0;
}
```
##### （2）函数名
```
# include <stdio.h>  
// 定义空函数
void fun () {};
int main (void) { 
	// 打印函数名和函数地址（相同）
	printf("fun=%d，&fun=%d\n", fun, &fun);
	return 0;
}
```
##### （3）递归函数
```
# include <stdio.h> 
// 定义阶乘函数 
int fun (int a) {
	// 结束条件 
	if(a <= 1){
		return 1;
	}
	// 函数递归（自己调用自己） 
	return a * fun (a-1);
};
int main (void) {
	// 打印5的阶乘 
	printf("%d", fun(5));
	return 0;
}
```
##### （4）回调函数
```
# include <stdio.h>  
// 定义fun1 
void fun1 () {
	printf("fun1");
};
// 定义fun2，其参数为一个能容纳fun1的函数指针 
void fun2 (void (* p) ()) {
	// 回调函数 
	p();
}
int main (void) {
	// 调用fun2，把fun1作为参数 
	fun2(fun1);
	return 0;
}
```
#### 6 指针
###### （1）定义与使用
```
# include <stdio.h>
void fun () {};
int main (void) {
	// 整型指针 
	int a = 5;
	int * p1 = &a;
	printf("内存地址：%d，其值：%d\n", p1, *p1);
	// 字符型指针 
	char b = 'b';
	char * p2 = &b;
	// p2 = (char *)2686715; 表示指针可以修改 
	printf("内存地址：%d，其值：%c\n", p2, *p2);
	// 数组指针 
	int c[3] = {1, 2, 3};
	int * p3 = c;
	for (int i=0; i<3; i++) {
		// p+1表示p+一个基本长度（视类型而定） 
		printf("内存地址：%d，其值：%d\n", p3+i, *(p3+i));上 
	}
	// 函数指针
	void (* p4) () = fun;
	// 函数的值没有对应的输出类型，所以不打印 
	printf("内存地址：%d\n", p4);
	return 0;
}
```
###### （2）二级指针
```
# include <stdio.h>
void fun () {};
int main (void) {
	// 整型变量 
	int a = 5;
	// 一级指针 
	int * p1 = &a;
	// 二级指针 
	int ** p2 = &p1;
	// p1的地址 
	printf("p2 = %d\n", p2);
	// a的地址 
	printf("p2的值 = %d\n", *p2);
	// a的值 
	printf("p2的值的值 = %d\n", **p2);
	return 0;
}
```
###### （3）指针的妙用
```
# include <stdio.h>
void fun (int * p) {
	// 通过指针，修改a的值 
	*p = 100;
};
int main (void) {
	int a = 5;
	double b = 99.6;
	// int=4，double=8 
	printf("int的长度：%d，double的长度：%d\n", sizeof(a), sizeof(b));
	// 都等于4 
	printf("int指针的长度：%d，double指针的长度：%d\n", sizeof(&a), sizeof(&b));
	fun (&a);
	// a = 100 
	printf("a=%d\n", a);
	return 0;
}
```
##### （4）指针的优点：
①只占4字节（无论类型）
②跨作用域调用（只要没被释放）
③自定义数据结构（如：链表、二叉树）
上例介绍了前两个，第三个留给《数据结构》这门课
#### 7 结构体
##### （1）定义和用法
```
# include <stdio.h>
# include <string.h>
int main (void) {
	// 定义"学生"结构体，并声明汤姆 
	struct Student {
		int age;
		char name[10];
	}Tom;
	// 设置汤姆 
	Tom.age = 18;
	strcpy(Tom.name, "汤姆");
	// 定义爱丽丝 
	struct Student Alice = {17, "爱丽丝"};
	// 定义简 
	struct Student jane;
	jane.age = 19;
	strcpy(jane.name, "简");
	printf("%s今年%d岁\n", Tom.name, Tom.age);
	printf("%s今年%d岁\n", Alice.name, Alice.age);
	printf("%s今年%d岁\n", jane.name, jane.age);
	// 利用指针来修改和调用，p->age等价于Tom.age 
	struct Student * p = &Tom;
	p->age = 20;
	printf("%s今年%d岁\n", p->name, p->age);
	return 0;
}
```
##### （2）与类的区别
结构体中只有属性
类中有属性和方法
```
// 结构体
struct Student {
	// 属性
	int age;
	char name[10];
}
// 类（以Java为例）
class Student {
	// 属性
	int age;
	String name;
	// 方法
	void readBook (){
		...
	};
}
```
#### 8 字符串
##### （1）赋值和拼接
```
#include <stdio.h>
#include <string.h>
int main(){
    char a[6] = "Hello";
    char b[6] = "World";
    // 赋值
	strcpy (a, b)
	printf ("%s\n", a);
    strcpy (a, "Hello")
    // 拼接
    strcat (a, b);
    printf ("%s\n", a);
    return 0;
}
```
##### （2）长度和比较
```
#include <stdio.h>
#include <string.h>
int main(){
    char a[6] = "Hello";
	char b[6] = "World";
    // 字符串a的长度 = 5 
    printf ("%d\n", strlen(a));
    // 字符数组a的长度 = 6
    printf ("%d\n", sizeof(a));
	// 比较（返回a-b的值） 
    if (strcmp(a, b)) {
    	printf("a != b\n");
    }
    else {
    	printf("a = b\n");
    }
    return 0;
}
```
#### 9 文件操作
##### （1）写入文件
```
#include <stdio.h>
int main(){
	// 一个空的文件指针 
    FILE * fp = NULL;
    // 打开文件目录 （"w+"会自动创建文件，但不会自动创建文件夹） 
    fp = fopen("./aaa/bbb.txt", "w+");
    // 写入一个字符 
    fputc('a', fp);
    // 写入一段字符串（第一种） 
    fprintf(fp, "Hello world!\n");
    // 写入一段字符串（第二种） 
    fputs("Hello world!\n", fp);
    // 释放文件指针 
    fclose(fp);
    return 0;
}
```
##### （2）读取文件
```
#include <stdio.h>
int main(){
	// 一个空的文件指针 
    FILE * fp = NULL;
    char buff[255];
    // 打开文件目录 （"w+"会自动创建文件，但不会自动创建文件夹） 
    fp = fopen("./aaa/bbb.txt", "r");
    // 第一种读法 
    fscanf(fp, "%s", buff);
   	printf("%s\n", buff );
   	// 第二种读法 
   	fgets(buff, 255, (FILE*)fp);
   	printf("%s\n", buff );
    // 释放文件指针 
    fclose(fp);
    return 0;
}
```
#### 10 内存管理
##### （1）分配内存
```
#include <stdio.h>
#include <stdlib.h>
int main(){
	int a;
	printf ("请输入想要分配的内存大小：");
	scanf ("%d", &a);
	// malloc返回的是void *，"(int *)"强制转换，以确定一个元素占多少字节 
	int * p = (int *) malloc (sizeof (int) * a); 
	// 设置前三个元素 
	*p = 1; 
	p[1] = 2;
	*(p+2) = 3;
	// 遍历 
	for (int i=0; i<a; i++) {
		printf ("%d\n", p[i]);
	}
    return 0;
}
```
##### （2）释放内存
```
#include <stdio.h>
#include <stdlib.h>
int main(){
	// 动态分配内存
	int * p = (int *) malloc (sizeof (int) * 3); 
	// 释放内存
	free (p);
    return 0;
}
```
注：malloc的明显好处有两个，一个是动态分配（能实现变成数组），另一个是手动释放（常规数组要在程序结束后才会释放内存）

毕竟C语言没有垃圾回收机制┓( ´∀` )┏
##### （3）调整内存
```
#include <stdio.h>
#include <stdlib.h>
int main(){
	// 分配3个int 
	int * p = (int *) malloc (sizeof (int) * 3); 
	// 设置5个元素 
	for (int i=0; i<3; i++) {
		p[i] = i+1;
	}
	// 遍历
	for (int i=0; i<3; i++) {
		printf("%d\n", p[i]);
	} 
	// 重新分配5个int 
	realloc (p, sizeof (int) * 5);
	// 再设置5个元素 
	for (int i=0; i<3; i++) {
		p[i] = i+1;
	}
	// 遍历
	for (int i=0; i<3; i++) {
		printf("%d\n", p[i]);
	}
	// 两趟遍历均能成功，但是第一种有风险
	// 分配3个，却用了5个，容易出现内存错乱，把别的内容覆盖了 
    return 0;
}
```
#### 11 图形化界面
##### （1）图形库
##### （2）MFC
##### （3）Win32API
#### 12 大作业
##### （1）通讯录
##### （2）魔塔游戏
##### （3）植物大战僵尸修改器