# merge-sort-on-doubly-linked-list
Given Pointer/Reference to the head of a doubly linked list of n nodes, the task is to Sort the given doubly linked list using Merge Sort in both non-decreasing and non-increasing order.

class Solution {
  public:
    // Function to sort the given doubly linked list using Merge Sort.
    Node* merge(Node* first, Node* second){
        if(first == NULL) return second ;
        if(second == NULL) return first ;
        if(first->data < second->data){
            first->next = merge(first->next, second) ;
            first->next->prev = first ;
            first->prev = NULL ;
            return first ;
        }
        else{
            second->next = merge(first, second->next) ;
            second->next->prev = second ;
            second->prev = NULL ;
            return second ;
        }
    }
    Node* getmid(Node* head){
        Node* fast = head ;
        Node* slow = head ;
        while(fast->next != NULL && fast->next->next != NULL){
            fast = fast->next->next ;
            slow = slow->next ;
        }
        Node* temp = slow->next ;
        slow->next = NULL ;
        return temp ;
    }
    struct Node *sortDoubly(struct Node *head) {
        // Your code here
        if(head == NULL || head->next == NULL) return head ;
        Node* mid = getmid(head) ;
        head = sortDoubly(head) ;
        mid = sortDoubly(mid) ;
        return merge(head, mid) ;
    }
};
