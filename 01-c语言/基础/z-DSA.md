[2.6 Deletion of a node from Linked List (from beginning, end, specified position) | DSA Tutorials (youtube.com)](https://www.youtube.com/watch?v=ClvYytk5Rlg)
##### 链表的实现
注意：头节点始终存储第一个节点的地址
![[Pasted image 20240814151855.png]]
![[Pasted image 20240815091824.png]]
###### 思路：
```c
📌struct node{//定义一个结构体
	int data;//一个数据域
	struct node*next;//一个指针域
}; 
//首先定义结构体，仅仅定义了类型，没分配内存
1️⃣struct node* head ️//然后定义头指针
//类比int *p p保存的是int型的变量，数据类型是int型
//head指针要存储node的地址，并且node的数据类型就是struct node

head = 0;//初始化头节点，防止出事
⭕️malloc(sizeof(struct node))
//malloc分配内存，按照节点的大小来分配,还有节点类型，分配完之后这个函数返回一个指向该内存的指针

2️⃣struct node*head,*newnode;
//所以新定义一个newnode，来接受返回的内存
⭕️newnode = (struct node*)malloc(sizeof(struct node));

if(head)==0{
head = newnode;//如果头指针为空，直接赋值
}else{
head->next = newnode;//将头指针指向newnode
️}
3️⃣struct node*head,*newnode,*temp;
//新建一个temp去链接其他节点
```
###### 🔍遇到的疑惑点：
>- **`malloc` 分配内存**：`malloc(sizeof(struct node))` 这一行会为一个 `struct node` 类型的节点分配所需的内存（大小为 `struct node` 的大小）。 
>- **`malloc` 返回指针**：`malloc` 返回的是这块新分配内存的起始地址，这个地址就是新节点在内存中的位置。
>- **`newnode` 保存指针**：`newnode = (struct node *)malloc(sizeof(struct node));` 这行代码把 `malloc` 返回的指针赋值给了 `newnode`，从而使 `newnode` 指向这块新分配的内存，也就是新节点
##### 在链表中插入节点
###### 1. 在链表中插入节点
- 节点插入在最开始的位置
![[Pasted image 20240815091833.png]]

- 思路：![[Pasted image 20240815103626.png]]
首先有三个节点的链表，想在开头插入一个新的节点，
1.newnode->next = head;//把头节点保存的地址给newnode->next里面
2.头节点保存newnode的地址：head = newnode;
```c
//已经有头节点 
struct ListNode* newNode = (struct ListNode*)malloc(sizeof(struct ListNode));  // 创建新节点
newNode->val = 2;  // 给新节点赋值
newNode->next = head;  
// 将新节点的 next 指向原链表的头节点|让头节点保存的值放进newnode的数据域里面
head = newNode;  // 更新链表头指针，使其指向新节点
```



![[Pasted image 20240815135149.png]]
###### 2. 在后面插入节点
- 思路![[Pasted image 20240815135205.png]]
1.将要插入的newnode的数据域变成0
2.新建一个temp来指向头节点
(temp和头指针一样，头指针指向头节点不能动，temp代替头指针遍历链表来操作)
3.当temp遍历到最后一个之前(节点的数据域不为空的时候)，就一直遍历
4.当最后一个时，把temp里的值变成新节点的地址(temp = newnode)
```c
    struct node{  
    int data;  
    struct node*next;  
};  
//定义三个指向节点类型的指针：头指针，辅助的指针，指向新节点的指针
//节点类型是struct node类型
struct node*head,*newnode,*temp; 
```
 ⭕️newnode= (struct node*)malloc(sizeof(struct node));
malloc 函数的作用是分配一块内存，并返回该内存块的起始地址。这个地址就是一个指向新节点的指针 [[#🔍遇到的疑惑点：|🔍遇到的疑惑点：]]
```c
newnode= (struct node*)malloc(sizeof(struct node));
 scanf("%d",&newnode->data); // 
 newnode->next = 0;  
 temp = head;  
 while(temp->next != 0){  
     temp = temp->next;  
 }  
 temp->next = newndode;
```
###### 3. 在给定地址之后插入节点
![[Pasted image 20240815152253.png]]
- 思路![[Pasted image 20240815153310.png]]
1.输入想插入的节点的位置,用pos来记录它，i用来遍历
2.然后创建一个temp来遍历到要插入的位置
3.然后输入要插入的新节点的数据（&newnode->data）
4.将新节点指向要插入位置的下一个节点,
>记得先让新节点链接到下一个节点，不然旧节点丢失
>newnode->next = temp->next;
> temp->next = newnode;

```c
struct node{
	int data;
	struct node* next;
};
struct node *head,*newnode,*temp;
int pos;//插入节点的位置
int i = 0;
 newnode = (struct node*)malloc (sizeof(struct node));
 scanf("%d",&pos);
 
 if(pos > count){
 //它是在检查用户输入的插入位置 `pos` 是否超过了链表的长度 `count`
 printf("invalid ");
 }else{
	 temp = head;//temp指向头节点
	 while(i < pos){
	 temp = temp->next;
	 i++;
	 }
	 scanf("%d",&newnode->data);
	 newnode->next = temp->next;
	 temp->next = newnode;
 }
```

##### 在链表中删除节点
###### 删除链表前面的节点
![[Pasted image 20240815203919.png]]
- 思路![[Pasted image 20240815204021.png]]
1.先把第一个要删除的节点保存起来
2.然后把头指针后移
3.free第一个被删除的节点
```c
delete from begining{
struct node*temp;
	temp = head;
	head = head->next;
	free(temp);
}
```
###### 删除链表后面的节点
- 思路![[Pasted image 20240815221931.png]]
1.定义两个节点temp和p，temp后移，p在temp的后一个
2.
```c
struct node* p;
	temp = head;
	while(temp->next != 0){//当temp遍历到最后一个之前
		p = temp;
		temp = temp->next;
	}
	if(temp == head){
		head = 0;
		free(temp);
	}else{
		p->next = 0;
		free(temp);
	}
```

###### 删除给定位置处的节点
![[Pasted image 20240815221729.png]]
- 思路![[Pasted image 20240815221949.png]]4
```c
struct node{
int data;
struct node*next;
};
struct node*head,*temp;
delete_from_pos()
struct node*next node;
	int pos,i = 1;
	temp = head;
	printf("enter position");
	scanf("%d",&pos);//输入要删除的节点数
while( i< pos-1){//让temp往下走起来
	temp = temp->next;
	i++;
}//知道遍历到要删除的节点的前一个
nextnode = temp->next;//用新的节点保存要删除的节点
temp->next = nextnode->next;
//把要删除的后一个节点的地址给被删除的前一个
free(nextnode);
}
```


##### 栈
###### - 用数组实现栈
![[Pasted image 20240818132243.png]]
思路![[Pasted image 20240818212037.png]]
1. `top` 是栈顶指针，它表示栈中当前最后一个元素的索引。初始时，`top` 被设置为 `-1`，表示栈为空。当执行 `push` 操作时，`top` 会增加，指向新加入元素的位置。
```c
//入栈操作
#define N 5;
int stack[N];
int top = -1;
void push(){
	printf("输入数据");
	scanf("%d",&x);
}
if(top == N-1){
printf("超出限制");
}else{
	top++;
	stack[top] = x;
}
```
2. 当 `top == -1` 时，表示栈是空的，此时不能进行出栈操作，输出 "下溢出"。否则，将栈顶的元素存储在 `item` 中，输出后将 `top` 减少，表示元素已经被移除
```c
//出栈操作
void pop(){
	int item;//先判断栈上有没有元素，如果无就没办法出元素
	if(top == -1){
	printf("under flow");
	}else{
	item = stack[top];
	top--;
	printf("%d",item);
	}
}
```
3. `peek()` 函数中，应该检查栈是否为空，以确保在访问栈顶元素时不会出现错误。如果 `top == -1`，则栈为空，否则输出栈顶元素。
以下是修改后的 `peek` 函数：
```c
void peek() {
    if (top == -1) {  // 如果栈为空
        printf("栈为空，无法查看栈顶元素\n");
    } else {
        printf("栈顶元素是: %d\n", stack[top]);  // 输出栈顶元素
    }
}
```
4. `display` 函数中，应该循环遍历栈中的元素，从栈顶到栈底依次输出
```c
void display() {
    int i;  
    if (top == -1) {
        printf("栈为空\n");  // 如果栈为空，提示
    } else {
        printf("栈中的元素是: ");
        for (i = top; i >= 0; i--) { // 从栈顶遍历到栈底
            printf("%d ", stack[i]);
        }
        printf("\n");  // 输出换行符
    }
}
```
