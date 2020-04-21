~~~JAVA
package list.linkedlist.implementation;

public class LinkedList {
	private Node head; //첫번째 노드
	private Node tail; //마지막 노드
	private int size = 0; // 노드의 개수
	private class Node{
		private Object data; //값을 저장한 변수
		private Node next; //다음 노드
		public Node(Object input){
			this.data  = input;
			this.next = null;
		}
		public String toString(){
			return String.valueOf(this.data);
		}
	}
}
~~~
