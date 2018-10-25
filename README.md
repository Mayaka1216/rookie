# rookie-from-ntu
personal learning materials of c++
#include <iostream>
using namespace std;
 
struct Node
{
	int id;
	Node *next;
	Node(int i) { id = i; next = NULL; }
};
struct LinkedList
{
	Node *head;
	int length;
	LinkedList(){ head = NULL; length = 0; }
};

int Josephus(int n, int m, int k)
{
	if (n<0||k<0||m<0)
	{
		cout << "三个输入参数必须都为正整数" << endl;
		return 0;
	}
	if (n < k)
	{
		cout << "起始序号必须大于总人数" << endl;
		return 0;
	}
	//先建立循环链表
	LinkedList *list = new LinkedList();
	Node *node = list->head;
	Node *pnode = list->head;  //先驱节点
	for (int i = 1; i <= n; i++)
	{
		if (i == 1)
		{
			node = new Node(i);
			list->head = node;
			list->length++;
			node->next = node;
		}
		else
		{
			pnode = node;
			node = new Node(i);
			pnode->next = node;
			node->next = list->head;
			list->length++;
		}
	}
	//打印下，验证现有链表信息正确
	Node *temp = list->head;
	for (int i = 1; i <= n; i++)
	{
		cout << temp->id << ends;
		temp = temp->next;
	}
	cout << endl;
	
	node = list->head;
	pnode = list->head;
	//找到第一个开始报数的人
	while (--k)
	{
		pnode = node;
		node = node->next;
	}
	cout << "第一个开始报数的人的id:" << node->id << endl;
	int j = m - 1;
	cout << "出列人的id依次是：" << ends;
	while (n--)
	{
		for (j = m-1; j > 0; j--)
		{
			pnode = node;
			node = node->next;
		}
			cout << node->id << " " << ends;
			pnode->next = node->next;
			node = pnode->next;
	}
}
 
int main()
{
	Josephus(7, 20, 10);
	cout<<endl;
}
