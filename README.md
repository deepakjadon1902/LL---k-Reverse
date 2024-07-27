import java.util.Scanner;

class Node {
    int data;
    Node next;

    Node(int data) {
        this.data = data;
        this.next = null;
    }
}

public class Main {
    public static Node reverseKGroup(Node head, int k) {
        if (head == null || k == 1) {
            return head;
        }

        Node dummy = new Node(0);
        dummy.next = head;
        Node curr = dummy, nex = dummy, pre = dummy;
        int count = 0;

        // Count the number of nodes in the linked list
        while (curr.next != null) {
            curr = curr.next;
            count++;
        }

        // Reverse every k nodes
        while (count >= k) {
            curr = pre.next;
            nex = curr.next;
            for (int i = 1; i < k; i++) {
                curr.next = nex.next;
                nex.next = pre.next;
                pre.next = nex;
                nex = curr.next;
            }
            pre = curr;
            count -= k;
        }

        return dummy.next;
    }

    public static void printList(Node head) {
        while (head != null) {
            System.out.print(head.data + " ");
            head = head.next;
        }
        System.out.println();
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        // Read inputs
        int N = sc.nextInt();
        int K = sc.nextInt();
        
        if (N == 0) {
            return;
        }

        Node head = new Node(sc.nextInt());
        Node current = head;

        for (int i = 1; i < N; i++) {
            current.next = new Node(sc.nextInt());
            current = current.next;
        }

        // Reverse the linked list in groups of K
        head = reverseKGroup(head, K);

        // Print the modified linked list
        printList(head);
    }
}
