# 概述

数据结构包括：**线性结构**和**非线性结构**。  

**线性结构**：

1）线性结构作为最常用的数据结构，其特点是数据元素之间存在一对一的线性关系。

2）线性结构有两种不同的存储结构，即**顺序存储**结构  （数组）和**链式存储**结构（链表）。顺序存储的线性表称为顺序表，顺序表中的存储元素是连续的。

3）链式存储的线性表称为链表，链表中的存储元素不一定是连续的，元素节点中存放数据元素以及相邻元素的地  址信息。

4）线性结构常见的有：数组、队列、链表和栈。

**非线性结构**： 

非线性结构包括：二维数组，多维数组，广义表，**树结构**，**图结构**。

------



# 线性结构

## 1.稀疏数组（SparseArray）

```
import java.io.File;
import java.io.FileReader;
import java.io.FileWriter;
import java.io.IOException;
import java.io.Reader;
import java.io.Writer;

public class SparseArray {

    public static void main(String[] args) throws IOException {
        // 创建一个原始的二维数据 11 * 11
        // 0：表示没有棋子，1表示黑子，2表示蓝子
        int chessArr1[][] = new int[11][11];
        chessArr1[1][2] = 1;
        chessArr1[2][3] = 2;
        chessArr1[4][5] = 2;
        // 输出原始的二维数组
        System.out.println("原始的二维数组");
        for (int[] row : chessArr1) {
            for (int data : row) {
                System.out.printf("%d\t", data);
            }
            System.out.println();
        }

        // 将二维数组 转成 稀疏数组
        // 1、先遍历二维数组，得到非0数据的个数
        int sum = 0;
        for (int i = 0; i < 11; i++) {
            for (int j = 0; j < 11; j++) {
                if (chessArr1[i][j] != 0) {
                    sum++;
                }
            }
        }

        // 2、创建对应的稀疏数组
        int sparseArr[][] = new int[sum + 1][3];

        // 给稀疏数组赋值
        sparseArr[0][0] = 11;
        sparseArr[0][1] = 11;
        sparseArr[0][2] = sum;

        // 遍历二维数组，将非0的值存放到sparseArr中
        int count = 0; // count用于记录第几个非零数据
        for (int i = 0; i < 11; i++) {
            for (int j = 0; j < 11; j++) {
                if (chessArr1[i][j] != 0) {
                    count++;
                    sparseArr[count][0] = i;
                    sparseArr[count][1] = j;
                    sparseArr[count][2] = chessArr1[i][j];
                }
            }
        }

        String sparseArray = "";

        // 输出稀疏数据的形式
        System.out.println();
        System.out.println("得到的稀疏数组为~~~~~~");
        for (int i = 0; i < sparseArr.length; i++) {
            System.out.printf("%d\t%d\t%d\t\n", sparseArr[i][0], sparseArr[i][1], sparseArr[i][2]);
            sparseArray += sparseArr[i][0] + "," + sparseArr[i][1] + "," + sparseArr[i][2] + ",";
        }
        System.out.println();

        // 将稀疏数据存放到sparse.data文件中
        File sparse = new File("C:\\Users\\Administrator\\Desktop\\temp_data_structure_test\\data\\test.txt");
        sparse.createNewFile();
        Writer w = new FileWriter(sparse);
        char[] charArray = sparseArray.toCharArray();
        w.write(charArray);
        w.flush();

        Reader r = new FileReader(sparse);
        char[] flush = new char[1024];
        int len = -1;
        String str = "";
        while ((len = r.read(flush)) != -1) {
            str = new String(flush, 0, len);
        }
        String[] strArr = str.split(",");
        int length = strArr.length / 3;
        int sparseArr1[][] = new int[length][3];

        int index = 0;

        for (int i = 0; i < sparseArr1.length; i++) {
            for (int j = 0; j < sparseArr1[i].length; j++) {
                sparseArr1[i][j] = Integer.parseInt(strArr[index]);
                index++;
            }
        }

        System.out.println("读取出来的稀疏数组！！！");
        for (int i = 0; i < sparseArr1.length; i++) {
            System.out.printf("%d\t%d\t%d\t\n", sparseArr1[i][0], sparseArr1[i][1], sparseArr1[i][2]);
        }

        sparseArr[0][0] = Integer.parseInt(strArr[0]);
        sparseArr[0][1] = Integer.parseInt(strArr[1]);
        sparseArr[0][2] = Integer.parseInt(strArr[2]);
        sparseArr[1][0] = Integer.parseInt(strArr[3]);
        sparseArr[1][1] = Integer.parseInt(strArr[4]);
        sparseArr[1][2] = Integer.parseInt(strArr[5]);
        sparseArr[2][0] = Integer.parseInt(strArr[6]);
        sparseArr[2][1] = Integer.parseInt(strArr[7]);
        sparseArr[2][2] = Integer.parseInt(strArr[8]);
        sparseArr[3][0] = Integer.parseInt(strArr[9]);
        sparseArr[3][1] = Integer.parseInt(strArr[10]);
        sparseArr[3][2] = Integer.parseInt(strArr[11]);


        // 将稀疏数组恢复成原始的二维数组

        // 1、先读取稀疏数组的第一行，根据第一行的数据，创建原始的二维数据
        int chessArr2[][] = new int[sparseArr[0][0]][sparseArr[0][1]];

        // 2、在读取稀疏数组后几行的数据（从第二行开始），并赋给 原始的二维数组 即可
        for (int i = 1; i < sparseArr.length; i++) {
            chessArr2[sparseArr[i][0]][sparseArr[i][1]] = sparseArr[i][2];
        }

        // 输出恢复后的二维数组
        System.out.println();
        System.out.println("恢复后的二维数组");

        for (int[] row : chessArr2) {
            for (int data : row) {
                System.out.printf("%d\t", data);
            }
            System.out.println();
        }
    }

}
```

## 2.队列（queue）

### **顺序队列**

```
import java.util.Scanner;

public class ArrayQueueDemo {

    public static void main(String[] args) {
        // 创建一个队列
        ArrayQueue queue = new ArrayQueue(3);
        char key = ' '; // 接受用户输入
        Scanner scanner = new Scanner(System.in);
        boolean loop = true;
        // 输出一个菜单
        while (loop) {
            System.out.println("s(show)：显示队列");
            System.out.println("e(exit)：退出程序");
            System.out.println("a(add)：添加数据到队列");
            System.out.println("g(get)：从队列取出数据");
            System.out.println("h(head)：查看队列头的数据");
            key = scanner.next().charAt(0); // 接受一个字符
            switch (key) {
                case 's':
                    queue.showQueue();
                    break;
                case 'a':
                    System.out.println("请输入一个数字");
                    int value = scanner.nextInt();
                    queue.addQueue(value);
                    break;
                case 'g': // 取出数据
                    try {
                        int res = queue.getQueue();
                        System.out.printf("取出的数据是%d\n", res);
                    } catch (Exception e) {
                        System.out.println(e.getMessage());
                    }
                    break;
                case 'h': // 查看队列头的数据
                    try {
                        int res = queue.headQueue();
                        System.out.printf("队列头的数据是%d\n", res);
                    } catch (Exception e) {
                        System.out.println(e.getMessage());
                    }
                    break;
                case 'e':
                    scanner.close();
                    loop = false;
                    break;
                default:
                    break;
            }
        }
        System.out.println("程序退出");
    }

}

// 使用数组模拟队列-编写一个ArrayQueue类
class ArrayQueue {
    private int maxSize; // 表示数组的最大容量
    private int front; // 队列头
    private int rear; // 队列尾
    private int arr[]; // 该数组用于存放数据，模拟队列

    // 创建队列的构造器
    public ArrayQueue(int arrMaxSize) {
        this.maxSize = arrMaxSize;
        arr = new int[maxSize];
        front = -1; // 指向队列头部，分析出front是指向队列头的前一个位置
        rear = -1; // 指向队列尾，指向队列尾的数据（即就是队列最后一个数据）
    }

    // 判断队列是否满
    public boolean isFull() {
        return rear == maxSize - 1;
    }

    // 判断队列是否为空
    public boolean isEmpty() {
        return rear == front;
    }

    // 添加数据到队列
    public void addQueue(int n) {
        // 判断队列是否满
        if (isFull()) {
            System.out.println("队列满，不能加入数据！");
            return;
        }
        rear++; // 让rear后移
        arr[rear] = n;
    }

    // 获取队列的数据，出队列
    public int getQueue() {
        // 判断队列是否空
        if (isEmpty()) {
            // 通过抛出异常来处理
            throw new RuntimeException("队列空，不能取数据");
        }
        front++; // front后移
        return arr[front];
    }

    // 显示队列的所有数据
    public void showQueue() {
        // 遍历
        if (isEmpty()) {
            System.out.println("队列空的，没有数据");
            return;
        }
        for (int i = 0; i < arr.length; i++) {
            System.out.printf("arr[%d]=%d\n", i, arr[i]);
        }
    }

    // 显示队列的头数据，注意不是取出数据
    public int headQueue() {
        // 判断
        if (isEmpty()) {
            throw new RuntimeException("队列空的，没有数据");
        }
        return arr[front + 1];
    }
}
```

### **循环队列**

```
import java.util.Scanner;

public class CircleArrayQueueDemo {

	public static void main(String[] args) {
		System.out.println("测试数组模拟环形队列");

		// 创建一个队列
		CircleArray queue = new CircleArray(4); // 注意，其中队列的有效数据最大是3
		char key =' '; // 接受用户输入
		Scanner scanner = new Scanner(System.in);
		boolean loop = true;
		// 输出一个菜单
		while(loop) {
			System.out.println("s(show)：显示队列");
			System.out.println("e(exit)：退出程序");
			System.out.println("a(add)：添加数据到队列");
			System.out.println("g(get)：从队列取出数据");
			System.out.println("h(head)：查看队列头的数据");
			key = scanner.next().charAt(0); // 接受一个字符
			switch (key) {
			case 's':
				queue.showQueue();
				break;
			case 'a':
				System.out.println("请输入一个数字");
				int value = scanner.nextInt();
				queue.addQueue(value);
				break;
			case 'g': // 取出数据
				try {
					int res = queue.getQueue();
					System.out.printf("取出的数据是%d\n", res);
				} catch (Exception e) {
					System.out.println(e.getMessage());
				}
				break;
			case 'h': // 查看队列头的数据
				try {
					int res = queue.headQueue();
					System.out.printf("队列头的数据是%d\n", res);
				} catch (Exception e) {
					System.out.println(e.getMessage());
				}
				break;
			case 'e':
				scanner.close();
				loop = false;
				break;
			default:
				break;
			}
		}
		System.out.println("程序退出");
	}
}

class CircleArray{
	private int maxSize; // 表示数组的最大容量
	// front	变量的含义做一个调整：front就指向队列的第一个元素，也就是arr[front]
	// front 的初始值 = 0
	private int front; 
	// rear  变量的含义做一个跳转：rear指向队列的最后一个元素的后一个位置。因为希望空出一个空间作为约定
	// rear  的初始值 = 0
	private int rear; 
	private int arr[]; // 该数组用于存放数据，模拟队列
	
	public CircleArray(int arrMaxSize) {
		this.maxSize = arrMaxSize;
		arr = new int[maxSize];
	}
	
	// 判断队列是否满
	public boolean isFull() {
		return (rear + 1) % maxSize == front;
	}
		
	// 判断队列是否为空
	public boolean isEmpty() {
		return rear == front;
	}
	
	// 添加数据到队列
	public void addQueue(int n) {
		// 判断队列是否满
		if(isFull()) {
			System.out.println("队列满，不能加入数据！");
			return;
		}
		// 直接将数据加入
		arr[rear] = n;
		// 将rear后移，这里必须考虑取模
		rear = (rear + 1) % maxSize;
	}
	
	// 获取队列的数据，出队列
	public int getQueue() {
		// 判断队列是否空
		if(isEmpty()) {
			// 通过抛出异常来处理
			throw new RuntimeException("队列空，不能取数据");
		}
		// 需要分析出front是指向队列的第一个元素
		// 1、先把front 对应的值保留到一个临时的变量
		// 2、将front 后移，考虑取模
		// 3、将临时保留的变量返回
		int value = arr[front];
		front = (front + 1) % maxSize;
		return value;
	}
	
	// 显示队列的所有数据
	public void showQueue() {
		// 遍历
		if(isEmpty()) {
			System.out.println("队列空的，没有数据");
			return;
		}
		// 思路：从front开始遍历，遍历多少个元素
		for(int i = front; i < front + size(); i++) {
			System.out.printf("arr[%d]=%d\n", i % maxSize, arr[i % maxSize]);
		}
	}
	
	// 求出当前列队有效数据的个数
	public int size() {
		return (rear + maxSize - front) % maxSize;
	}
	
	// 显示队列的头数据，注意不是取出数据
		public int headQueue() {
			// 判断
			if(isEmpty()) {
				throw new RuntimeException("队列空的，没有数据");
			}
			return arr[front];
		}

}

```

## 3.链表（LinkedList）

### 单链表

```
import java.util.Stack;

public class SingleLinkedListDemo {

    public static void main(String[] args) {
        // 进行测试
        // 先创建节点
        HeroNode hero1 = new HeroNode(1, "宋江", "及时雨");
        HeroNode hero2 = new HeroNode(2, "卢俊义", "玉麒麟");
        HeroNode hero3 = new HeroNode(3, "吴用", "智多星");
        HeroNode hero4 = new HeroNode(4, "林冲", "豹子头");

        // 创建一个链表
        SingleLinkedList singleLinkedList = new SingleLinkedList();
        // 加入
		singleLinkedList.add(hero1);
		singleLinkedList.add(hero2);
		singleLinkedList.add(hero3);
		singleLinkedList.add(hero4);

        // 加入按照编号的顺序
//        singleLinkedList.addByOrder(hero1);
//        singleLinkedList.addByOrder(hero4);
//        singleLinkedList.addByOrder(hero2);
//        singleLinkedList.addByOrder(hero3);


//        singleLinkedList.list();
		
//		singleLinkedList.sel(2);
		
		
		//测试修改节点的代码
//		HeroNode newHeroNode = new HeroNode(2, "小卢", "玉麒麟！！！");
//		singleLinkedList.update(newHeroNode);
//		System.out.println("修改之后的列表情况");
//		singleLinkedList.list();
		
		// 删除节点
//		singleLinkedList.del(1);
//		singleLinkedList.del(4);
//		singleLinkedList.del(2);
//		singleLinkedList.del(3);
//		System.out.println("删除之后的列表情况");
//		singleLinkedList.list();
		
//		System.out.println("测试单链表的有效节点个数");
//		System.out.println(getLength(singleLinkedList.getHead()));
		
//		System.out.println("测试是否得到了倒数第k个节点");
		HeroNode res = findLastIndexNode(singleLinkedList.getHead(), 1);
		System.out.println(res);

//		System.out.println("单链表的反转");
//		reversetList(singleLinkedList.getHead());
//		singleLinkedList.list();

//        System.out.println("测试逆序打印单链表，没有改变链表的结构");
//        reversePrint(singleLinkedList.getHead());

    }

    // 利用栈这个数据结构，将各个节点压入到栈中，然后利用栈的先进后出的特点，就实现了逆序打印的效果
    public static void reversePrint(HeroNode head) {
        if (head.next == null) {
            return; // 空链表，不能打印
        }
        // 创建一个栈，将各个节点压入栈中
        Stack<HeroNode> stack = new Stack<>();
        HeroNode cur = head.next;
        // 将链表的所有节点压入栈中
        while (cur != null) {
            stack.push(cur);
            cur = cur.next; //让cur后移，这样就可以压入下一个节点
        }
        // 将栈中的节点打印，pop 出栈
        while (stack.size() > 0) {
            System.out.println(stack.pop()); //stack的特点是先进后出
        }
    }

    // 将单链表进行反转
    public static void reversetList(HeroNode head) {
        // 如果当前链表为空，或者只有一个节点，无需反转，直接返回
        if (head.next == null || head.next.next == null) {
            return;
        }
        // 想定义一个辅助的指针（变量），帮助我们遍历原来的链表
        HeroNode cur = head.next;
        HeroNode next = null; // 指向当前节点[cur]的下一个节点
        HeroNode reverseHead = new HeroNode(0, "", "");
        // 遍历原来的链表，每遍历一个节点，就将其取出，并放在新的链表reverseHead 的最前端
        while (cur != null) {
            next = cur.next; // 先暂时保存当前节点的下一个节点，后面需要使用
            cur.next = reverseHead.next; // 将cur的下一个节点指向新的量表的最前端
            reverseHead.next = cur; // 将cur 连接到新的链表上
            cur = next; // 让cur后移
        }
        // 将head.next 指向reverseHead.next，实现反转
        head.next = reverseHead.next;

    }

    // 查找单链表中的倒数第k个节点
    // 思路
    // 1、编写一个方法，接受head节点，同时接受一个index
    // 2、index 表示是倒数第index个节点
    // 3、先把链表从头到尾遍历，得到链表的总的长度getLength
    // 4、得到size后，从链表的第一个开始遍历（size - index）
    // 5、找到返回，否则返回null
    public static HeroNode findLastIndexNode(HeroNode head, int index) {
        // 判断如果链表为空，返回null
        if (head.next == null) {
            return null; //没有找到
        }
        // 第一次遍历得到链表的长度（节点个数）
        int size = getLength(head);
        // 第二次遍历 size - index 位置，就是我们倒数第k个节点
        // 先做一个index的校验
        if (index <= 0 || index > size) {
            return null;
        }
        // 定义辅助变量
        HeroNode cur = head.next;
        for (int i = 0; i < size - index; i++) {
            cur = cur.next;
        }
        return cur;
    }

    // 方法：获取到单链表的节点的个数（如果是带头节点的链表，需要不统计头节点）

    /**
     * @param head 链表的头节点
     * @return 返回有效节点的个数
     */
    public static int getLength(HeroNode head) {
        if (head.next == null) { // 空链表
            return 0;
        }
        int length = 0;
        // 定义一个辅助变量，这里我们没有统计头节点
        HeroNode cur = head.next;
        while (cur != null) {
            length++;
            cur = cur.next; // 遍历
        }
        return length;
    }

}

// 定义SingleLinkedList 管理我们的英雄
class SingleLinkedList {
    // 初始化一个头节点，头节点不要动，不存放具体的数据
    private HeroNode head = new HeroNode(0, "", "");

    public HeroNode getHead() {
        return head;
    }

    public void setHead(HeroNode head) {
        this.head = head;
    }

    // 添加节点到单向链表
    // 思路，当不考虑编号顺序时
    // 1、找到当前链表的最后节点
    // 2、将最后这个节点的next 指向 新的节点
    public void add(HeroNode heroNode) {
        // 因为head节点不能动，因此我们需要一个辅助变量temp
        HeroNode temp = head;
        // 遍历链表，找到最后
        while (true) {
            // 找到链表的最后
            if (temp.next == null) {
                break;
            }
            // 如果没有找到，将temp后移
            temp = temp.next;
        }
        // 当退出while循环时，temp就指向了链表的最后
        temp.next = heroNode;
    }

    // 第二种方式在添加英雄时，根据排名将英雄插入到指定位置
    // （如果有这个排名，则添加失败，并给出提示）
    public void addByOrder(HeroNode heroNode) {
        // 因为头节点不能动，因此我们仍然通过一个辅助指针（变量）来帮助找到添加的位置
        // 因为单链表，因此我们找的temp 是位于 添加位置的前一个节点，否则插入不了
        HeroNode temp = head;
        boolean flag = false; // flag标志英雄添加的编号是否存在，默认为false
        while (true) {
            if (temp.next == null) { // 说明temp已经在链表的最后
                break;
            }
            if (temp.next.no > heroNode.no) { // 位置找到，就在temp的后面插入
                break;
            } else if (temp.next.no == heroNode.no) { // 希望添加的heroNode的编号已然存在
                flag = true; // 说明编号存在
                break;
            }
            temp = temp.next; // 后移
        }
        // 判断flag的值
        if (flag) { // 不能添加，说明编号已经存在
            System.out.printf("准备插入的英雄的编号%d 已经存在，不能加入\n", heroNode.no);
        } else {
            // 插入到链表中，temp的后面
            heroNode.next = temp.next;
            temp.next = heroNode;
        }
    }

    // 修改节点的信息，根据no编号来修改，即no编号不能改
    // 说明
    // 1、根据newHeroNode 的 no 来修改即可
    public void update(HeroNode newHeroNode) {
        // 判断是否为空
        if (head.next == null) {
            System.out.println("列表为空！！！");
            return;
        }
        // 找到需要修改的节点，根据no编号
        // 定义一个辅助变量
        HeroNode temp = head.next;
        boolean flag = false; // 表示是否找到该节点
        while (true) {
            if (temp == null) {
                break; // 已经遍历完链表
            }
            if (temp.no == newHeroNode.no) {
                // 找到
                flag = true;
                break;
            }
            temp = temp.next;
        }
        // 根据flag判断是否找到要修改的节点
        if (flag) {
            temp.name = newHeroNode.name;
            temp.nickname = newHeroNode.nickname;
        } else { // 没有找到
            System.out.printf("没有找到 编号 %d 的节点，不能修改\n", newHeroNode.no);
        }
    }

    // 删除节点
    // 思路
    // 1、head 不能动，因此需要一个temp辅助节点找到带删除节点的前一个节点
    // 2、说明我们在比较是，是temp.next.no 和 需要删除的节点的no比较
    public void del(int no) {
        HeroNode temp = head;
        boolean flag = false; // 标志是否找到带删除节点的前一个节点
        while (true) {
            if (temp.next == null) { // 已经到链表的最后
                break;
            }
            if (temp.next.no == no) {
                // 找到带删除节点的前一个节点
                flag = true;
                break;
            }
            temp = temp.next;
        }
        if (flag) { // 找到
            // 可以删除
            temp.next = temp.next.next;
        } else {
            System.out.printf("要删除的%d 节点不存在\n", no);
        }
    }

    // 查询链表
    public void sel(int no) {
        HeroNode temp = head;
        boolean flag = false;
        while (true) {
            if (temp.next == null) {
                break;
            }
            if (temp.next.no == no) {
                flag = true;
                break;
            }
            temp = temp.next;
        }
        if (flag) {
            System.out.println(temp.next);
        } else {
            System.out.println("没有找到此人");
        }
    }

    // 显示链表[遍历]
    public void list() {
        // 判断链表是否为空
        if (head.next == null) {
            System.out.println("链表为空");
            return;
        }
        // 因为头节点不能动，需要一个辅助变量来遍历
        HeroNode temp = head.next;
        while (true) {
            // 判断是否到链表最后
            if (temp == null) {
                break;
            }
            // 输出节点信息
            System.out.println(temp);
            // 将next后移，一定小心
            temp = temp.next;
        }
    }
}


// 定义一个HeroNode，每个HeroNode对象就是一个节点
class HeroNode {
    public int no;
    public String name;
    public String nickname;
    public HeroNode next; // 指向下一个节点

    // 构造器
    public HeroNode(int no, String name, String nickname) {
        this.no = no;
        this.name = name;
        this.nickname = nickname;
    }

    // 为了显示方便，重新toString方法
    @Override
    public String toString() {
        return "HeroNode [no=" + no + ", name=" + name + ", nickname=" + nickname + "]";
    }

}
```

### 双向链表

```
public class DoubleLinkedListDemo {
	public static void main(String[] args) {
		HeroNode2 hero1 = new HeroNode2(1, "宋江", "及时雨");
		HeroNode2 hero2 = new HeroNode2(2, "卢俊义", "玉麒麟");
		HeroNode2 hero3 = new HeroNode2(3, "吴用", "智多星");
		HeroNode2 hero4 = new HeroNode2(4, "林冲", "豹子头");
		HeroNode2 hero5 = new HeroNode2(4, "公孙胜", "入云龙");
		HeroNode2 hero6 = new HeroNode2(5, "李哈哈", "嘿嘿");

		// 创建一个双向链表对象
		DoubleLinkedList doubleLinkedList = new DoubleLinkedList();
		
		/*//测试
		System.out.println("双向链表的测试");
		doubleLinkedList.add(hero1);
		doubleLinkedList.add(hero2);
		doubleLinkedList.add(hero3);
		doubleLinkedList.add(hero4);
		doubleLinkedList.list();
		
		// 修改
		doubleLinkedList.update(hero5);
		System.out.println("修改后的链表情况");
		doubleLinkedList.list();
		
		// 删除
		doubleLinkedList.del(3);
		System.out.println("删除后的链表情况");
		doubleLinkedList.list();*/
		
		// 第二种方式在添加英雄时，根据排名将英雄插入到指定位置
		doubleLinkedList.addByOrder(hero5);
		doubleLinkedList.addByOrder(hero4);
		doubleLinkedList.addByOrder(hero1);
		doubleLinkedList.addByOrder(hero3);
		doubleLinkedList.addByOrder(hero2);
		doubleLinkedList.addByOrder(hero6);
		
		doubleLinkedList.list();
	}
}

// 创建一个双向链表的类
class DoubleLinkedList {
	// 先初始化 一个头节点，头节点不要动，不存放具体数据
	private HeroNode2 head = new HeroNode2(0, "", "");

	public HeroNode2 getHead() {
		return head;
	}

	// 显示链表[遍历]
	public void list() {
		// 判断链表是否为空
		if (head.next == null) {
			System.out.println("链表为空");
			return;
		}
		// 因为头节点不能动，需要一个辅助变量来遍历
		HeroNode2 temp = head.next;
		while (true) {
			// 判断是否到链表最后
			if (temp == null) {
				break;
			}
			// 输出节点信息
			System.out.println(temp);
			// 将next后移，一定小心
			temp = temp.next;
		}
	}

	// 添加一个节点到双向链表的最后
	public void add(HeroNode2 heroNode) {
		// 因为head节点不能动，因此我们需要一个辅助变量temp
		HeroNode2 temp = head;
		// 遍历链表，找到最后
		while (true) {
			// 找到链表的最后
			if (temp.next == null) {
				break;
			}
			// 如果没有找到，将temp后移
			temp = temp.next;
		}
		// 当退出while循环时，temp就指向了链表的最后
		// 形成一个双向链表
		temp.next = heroNode;
		heroNode.pre = temp;
	}
	
	// 修改一个节点的内容，可以看到双向链表的节点内容修改和单向链表一样
	// 只是 节点的类型改成了HeroNode2
	public void update(HeroNode2 newHeroNode) {
		// 判断是否为空
		if(head.next == null) {
			System.out.println("列表为空！！！");
			return;
		}
		// 找到需要修改的节点，根据no编号
		// 定义一个辅助变量
		HeroNode2 temp = head.next;
		boolean flag = false; // 表示是否找到该节点
		while(true) {
			if(temp == null) {
				break; // 已经遍历完链表
			}
			if(temp.no == newHeroNode.no) {
				// 找到
				flag = true;
				break;
			}
			temp = temp.next;
		}
		// 根据flag判断是否找到要修改的节点
		if(flag) {
			temp.name = newHeroNode.name;
			temp.nickname = newHeroNode.nickname;
		}else { // 没有找到
			System.out.printf("没有找到 编号 %d 的节点，不能修改\n", newHeroNode.no);
		}
	}
	
	// 从双向链表中删除一个节点
	// 说明
	// 1、对于双向链表，我们可以直接找到要删除的节点
	// 2、找到后，自我删除即可
	public void del(int no) {
		// 判断当前链表是否为空
		if(head.next == null) { // 空链表
			System.out.println("链表为空，无法删除");
			return;
		}
		
		HeroNode2 temp = head.next; // 辅助变量（指针）
		boolean flag = false; // 标志是否找到待删除节点
		while(true) {
			if(temp == null) { // 已经到链表的最后
				break;
			}
			if(temp.no == no) {
				// 找到带删除节点的前一个节点
				flag = true;
				break;
			}
			temp = temp.next;
		}
		if(flag) { // 找到
			// 可以删除
			// temp.next = temp.next.next; [单向链表]
			temp.pre.next = temp.next;
			// 这里我们的代码有问题？
			// 如果是最后一个节点，就不需要执行下面这句话，否则出现空指针异常
			if(temp.next != null) {
				temp.next.pre = temp.pre;
			}
		}else {
			System.out.printf("要删除的%d 节点不存在\n", no);
		}
	}
	
	// 按照顺序添加节点到双链表
	public void addByOrder(HeroNode2 heroNode) {
		// 因为头节点不能动，因此我们仍然通过一个辅助指针（变量）来帮助找到添加的位置
		// 因为单链表，因此我们找的temp 是位于 添加位置的前一个节点，否则插入不了
		HeroNode2 temp = head;
		boolean flag = false; // flag标志英雄添加的编号是否存在，默认为false
		while(true) {
			if(temp.next == null) { // 说明temp已经在链表的最后
				break;
			}
			if(temp.next.no > heroNode.no) { // 位置找到，就在temp的后面插入
				break;
			}else if(temp.next.no == heroNode.no){ // 希望添加的heroNode的编号已然存在
				flag = true; // 说明编号存在
				break;
			}
			temp = temp.next; // 后移
		}
		// 判断flag的值
		if(flag) { // 不能添加，说明编号已经存在
			System.out.printf("准备插入的英雄的编号%d 已经存在，不能加入\n", heroNode.no);
		}else {
			// 插入到链表中，temp的后面
			heroNode.next = temp.next;
			if(temp.next != null) {
				temp.next.pre = heroNode;
			}
			temp.next = heroNode;
			heroNode.pre = temp;
		}
	}

}

// 定义一个HeroNode，每个HeroNode对象就是一个节点
class HeroNode2 {
	public int no;
	public String name;
	public String nickname;
	public HeroNode2 next; // 指向下一个节点，默认为null
	public HeroNode2 pre; // 指向前一个节点，默认为null

	// 构造器
	public HeroNode2(int no, String name, String nickname) {
		this.no = no;
		this.name = name;
		this.nickname = nickname;
	}

	// 为了显示方便，重新toString方法
	@Override
	public String toString() {
		return "HeroNode2 [no=" + no + ", name=" + name + ", nickname=" + nickname + ", next=" + next + "]";
	}

}
```

