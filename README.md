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

