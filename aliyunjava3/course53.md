## [上一页](course52)
## 比较器（二叉树）

之前学习过链表程序，链表程序的关键是节点的互相引用，但是之前的链表有一个缺点：所有数据的保存顺序就是你的添加顺序，而且无法排序，
如果想要进行排序的保存就可以通过树的结构来完成 

树的结构：取第一个元素作为树的根节点，而后比这个根节点大的数据放在节点的右子树，如果比根节点小的放在左子树，在输出的时候按照中序遍历的原则取出。

中序遍历：左-中-右

![](http://ww2.sinaimg.cn/large/0060lm7Tly1fnfvg6ghdmj30ne0d2gnc.jpg)

那么这种树的结构的实现关键就是大小比较，而这种大小的比较就可以使用Comparable接口来完成

**范例** 实现二叉树：

    package cn.mldn.demo;

    import java.util.Arrays;

    class BinaryTree{//现在实现一个二叉树
      private class Node{
        private Comparable data;//保存的操作数据，因为必须是Comparable子类，需要比较大小
        private Node left;//保存左边节点
        private Node right;//保存右边节点
        public Node(Comparable data){
          this.data = data;
        }
        public void addNode(Node newNode){
          if (this.data.compareTo(newNode.data) > 0) {
            if (this.left == null) {
              this.left = newNode ;
            }else {
              this.left.addNode(newNode);
            }
          }else {
            if (this.right == null) {
              this.right = newNode;
            }else {
              this.right.addNode(newNode);
            }
          }
        }
        public void toArrayNode(){
          if (this.left != null) {
            this.left.toArrayNode();
          }
          BinaryTree.this.retData[BinaryTree.this.foot++] = this.data;
          if (this.right != null) {
            this.right.toArrayNode();
          }
        }
      }
      //-----------------------------//
      private Node root;
      private int count;
      private int foot =0;
      private Object[] retData;//返回数据
      public Object[] toArray(){
        this.foot = 0;//角标清零
        this.retData = new Object[this.count];
        this.root.toArrayNode();
        return this.retData;
      }
      public void add(Object data){
        if (data == null) {
          return ;
        }
        Node newNode = new Node((Comparable) data);
        if (this.root == null) {
          this.root = newNode;
        }else{
          this.root.addNode(newNode);
        }
        this.count++;
      }
    }

    public class BTDemo {
      public static void main(String[] args) {
        BinaryTree bt = new BinaryTree();
        bt.add("B");
        bt.add("X");
        bt.add("A");
        System.out.println(Arrays.toString(bt.toArray()));
      }
    }
**console:**
  
  [A, B, X]

链表的功能可以在此处补充后完整实现

二叉树实现的前提是必须能进行对象比较



## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course54)
