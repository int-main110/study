# LeetCode 2.两数相加

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        ListNode head = new ListNode();
        ListNode cur = head;
        int add = 0;
        while(l1 != null && l2 != null){ 
            cur.next = new ListNode((l1.val + l2.val + add) % 10);
            add = (l1.val + l2.val + add) / 10;
            l1 = l1.next;
            l2 = l2.next;
            cur = cur.next;
        }
        if(l1 == null){
            while(l2 != null){
                cur.next = new ListNode((l2.val + add) % 10);
                add = (l2.val + add) / 10;
                l2 = l2.next;
                cur = cur.next;
            }
        }else{
            while(l1 != null){
                cur.next = new ListNode((l1.val + add) % 10);
                add = (l1.val + add) / 10;
                l1 = l1.next;
                cur = cur.next;
            }
        }
        if(add > 0){
            ListNode node = new ListNode(add);
            cur.next = node;
        }
        return head.next;
    }
}
```

```
输入：l1 = [2,4,3], l2 = [5,6,4]
输出：[7,0,8]
解释：342 + 465 = 807.
```

思路：从左往右依次相加，建一个变量保存进位。

当两个链表长度不同时，L1[2,3,4],L2[5,6,7,8,9],在L1[2,3,4]相加用完后，L2就要继续算L2+add（进位）同时创造新的节点。

当出现L1[5,5],L2[5,5]时，需要在新的链表内创造一个新的节点来存最后进位产生的数。