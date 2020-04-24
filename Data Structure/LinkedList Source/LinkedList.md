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
	public void addFirst(Object input){
       		Node newNode = new Node(input);
        	newNode.next = head;
        	head = newNode;
        	size++;
        	if(head.next == null){
            		tail = head;
        	}
    }
	public void addLast(Object input){
        Node newNode = new Node(input);
        //리스트의 노드가 없다면 첫번째 노드를 추가 하는 메소드 호출
        if(size == 0){
            addFirst(input);
        } else{
            //마지막 노드의 다음을 새로 생성한 노드로 지정
            tail.next = newNode;
            //마지막 노드를 갱신
            tail = newNode;
            //엘리먼트 개수를 증가
            size++;
        }
    }
    Node node(int index){
        //특정 위치의 노드 찾기
        //첫번째 노드 확인
        Node x = head;
        //index 번째의 노드를 찾아 반환
        for(int i=0 ; i < index ; i++){
            x = x.next;
        }
        return x;
    }
    //특정한 위치에 노드 추가
    public void add(int k, Object input){
        if(k == 0){
            addFirst(input);
        } else {
            //추가 하려는 위치의 이전 노드
            Node temp1 = node(k -1);
            //추가 하려는 위치의 다음 노드
            Node temp2 = temp1.next;
            //추가될 노드
            Node newNode = new Node(input);
            temp1.next = newNode;
            newNode.next = temp2;
            size++;
            //추가된 노드의 다음 노드가 null 일 경우
            if(newNode.next == null){
                tail = newNode;
            }
        }
    }
}
~~~
