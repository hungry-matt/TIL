~~~JAVA
package list.doublylinkedlist.implementation.implementation;

public class DoublyLinkedList {
    private Node head; // 첫번째 노드
    private Node tail; // 두번째 노드
    private int size = 0;

    public Object removefirst() {
        //첫번째 노드 탐색
        Node temp = head;
        //head의 위치를 next 노드로 변경
        head = head.next;
        //삭제된 값을 리턴하기 위해 임시 변수에 담기
        Object returnData = temp.data;
        //노드 삭제
        temp = null;
        //노드의 크기 변경
        size--;
        //삭제된 값을 리턴
        return returnData;
    }

    public Object remove(int k) {
        //첫번째 노드를 삭제할때
        if(k == 0){
            return removefirst();
        }
        //삭제할 노드의 이전 노드 지정
        Node temp = node(k-1);
        //삭제할 노드 지정
        Node todoDeleted = temp.next;

        //삭제할 노드의 다음 노드를 이전 노드의 다음으로 지정
        temp.next = temp.next.next;
        //삭제될 데이터를 임시 변수에 담기
        Object returnData = todoDeleted.data;
        //삭제하려는 노드가 tail 이라면 이전 노드로 지정
        if(todoDeleted == tail){
            tail = temp;
        }
        todoDeleted = null;
        size--;
        return returnData;
    }
    
    //노드의 크기 반환
    public int size() {
        return size;
    }

    //선택 노드의 데이터 반환
    public Object get(int i) {
        Node temp = node(i);
        return temp.data;
    }

    //검색 데이터의 노드 위치 반환
    //강의전 예습 메소드
//    public int indexOf(Object data) {
//        Node temp = head;
//        int index = 0;
//        while(temp != tail){
//            Node currentNode = temp;
//            if(currentNode.data == data){
//                return index;
//            }
//            temp = currentNode.next;
//            index++;
//        }
//        return -1;
//    }
    public int indexOf(Object data){
        //비교 탐색을 위해 첫번째 노드를 temp로 지정
        Node temp = head;
        //탐색 데이터의 위치 반환을 위한 변수
        int index = 0;
        //탐색 데이터와 탐색 대상 데이터를 비교
        while(temp.data != data){
            //현재 노드 데이터와 맞지 않을 경우 다음 노드 지정
            temp = temp.next;
            //다음 노드의 위치 반환을 위해 증가
            index++;
            //다음 노드가 null. 즉, 현재 노드가 tail 일 경우
            if(temp == null){
                return -1;
            }
        }
        //탐색 대상을 찾았다면 대상의 인덱스 값을 리턴
        return index;
    }

    public ListIterator listIterlator() {
        //새로운 ListIterator를 인스턴스화 해서 리턴함.
        return new ListIterator();
    }

    class ListIterator{
        private Node next;
        private Node lastReturned;
        private int nextIndex;

        ListIterator(){
            next = head;
        }

        //현재 노드의 데이터 반환과 다음 노드 지정
        public Object next(){
            lastReturned = next;
            next = next.next;
            nextIndex++;
            return lastReturned.data;
        }
        
        //다음 노드의 유무 반환
        public boolean hasNext(){
            return nextIndex < size();
        }

        //새로운 노드 추가
        public void add(Object input){
            //노드 생성
            Node newNode = new Node(input);

            //lastReturned는 현재 노드의 이전 노드를 가지고 있어야 하는데
            //노드를 처음 생성시 lastReturned의 값은 null 이므로
            //이걸로 분기를 생성 한다.
            if(lastReturned == null){
                //head 지정
                head = newNode;
                //head를 바라보고 있던 next 노드를 신규 노드의 다음 으로 지정 한다.
                newNode.next = next;
            }else{
                //이전 노드의 다음을 신규 노드로 지정 한다.
                lastReturned.next = newNode;
                //next 노드를 신규 노드의 다음 으로 지정 한다.
                newNode.next = next;
            }
            //반환 노드를 생성된 노드로 지정
            lastReturned = newNode;
            //노드의 크기 증가
            size++;
            //다음 노드의 위치 값 증가
            nextIndex++;
        }

        public void remove() {
            //java의 int의 default value는 0 이다.
            if(nextIndex == 0){
                throw new IllegalStateException();
            }
            DoublyLinkedList.this.remove(nextIndex-1);
            nextIndex--;
        }
    }

    private class Node{
        private Object data;
        private Node next;
        private Node prev;
        public Node(Object input){
            this.data = input;
            this.next = null;
            this.prev = null;
        }
        public String toString() {
            return String.valueOf(this.data);
        }
    }

    public void addFirst(Object input){
        Node newNode = new Node(input);
        newNode.next = head;

        //처음 추가 되는 노드는 head 가 null 이기 때문에 확인
        if(head != null){
            head.prev = newNode;
        }

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
            //추가 되는 노드의 이전 노드 가르키기
            newNode.prev = tail;
            //마지막 노드를 갱신
            tail = newNode;
            //엘리먼트 개수를 증가
            size++;
        }
    }
    Node node(int index){
        if(index > size/2){
            //특정 위치의 노드 찾기
            //첫번째 노드 확인
            Node x = head;
            //index 번째의 노드를 찾아 반환
            for(int i=0 ; i < index ; i++){
                x = x.next;
            }
            return x;
        }else{
            Node x = tail;
            for(int i = size-1 ; i > index  ; i--){
                x =  x.prev;
            }
            return x;
        }
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
            //temp2가 null이 아닐때 즉, temp1의 다음 노드가 없는지 확인
            if(temp2 != null){
                temp2.prev =  newNode;
            }
            newNode.prev = temp1;
            size++;
            //추가된 노드의 다음 노드가 null 일 경우
            if(newNode.next == null){
                tail = newNode;
            }
        }
    }
    public String toString(){
        //노드가 없다면 []를 리턴
        if(head == null){
            return "[]";
        }
        Node temp = head;
        String str = "[";
        
        //다음 노드가 없을 때까지 반복문 실행
        while(temp.next != null){
            str += temp.data + ", ";
            temp = temp.next;
        }
        //마지막 노드는 위의 반복문 에서 제외 됬기 때문에 마지막 노드 data를 포함
        str += temp.data;
        return str + "]";
    }
}
~~~
