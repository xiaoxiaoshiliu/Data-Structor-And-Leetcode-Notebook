# 删除链表的重复元素I
## 题目连接
https://leetcode-cn.com/problems/remove-duplicates-from-sorted-list/
## 题目描述
删除链表中的重复元素，使得每个元素只出现一次。<br>
示例：输入：1->2->2->3 输出:1->2->3
## 思路及算法
知道如何删除节点即可，即从头结点开始遍历，若head->next==head->next->next,则将head->next=head->next->next即可<br>
可用递归和迭代那种方式。`注意考虑到空链表和链表只有一个元素的情况。`

## 代码
```cpp
//迭代
 ListNode* deleteDuplicates(ListNode* head) {
        if(!head||!head->next) return head;
        auto p=head;
        while(p->next)
        {
            if(p->val!=p->next->val) p=p->next;
            else p->next=p->next->next;
        }
        return head;
    }
    
  //递归
    ListNode* deleteDuplicates(ListNode* head)
    {
       if(!head) return head;
       if(!head->next) return head;
       auto cur=deleteDuplicates(head->next);
    }
```

# 删除链表重复元素II
## 题目连接：
https://leetcode-cn.com/problems/remove-duplicates-from-sorted-list-ii/
## 题目描述：
给定一个排序链表，删除所有含有重复数字的节点，只保留原始链表中 没有重复出现 的数字。

示例 1:
输入: 1->2->3->3->4->4->5
输出: 1->2->5

示例 2:
输入: 1->1->1->2->3
输出: 2->3
## 思路及算法
参考上一题的解法，可知，若p->val=p->next->val,则要使prev->next=p->next->next,这里可以定义一个prev作为p的前驱指针即可。<br>
此位也可用递归解法<br>
'注意:可能涉及到删除头结点的操作，因此需要使用哑结点'

## 代码
```cpp
时间复杂度O(n),空间复杂度O(1)
 ListNode* deleteDuplicates(ListNode* head) 
    {
        if(!head) return head;
        auto dummy=new ListNode(0);
        dummy->next=head;
        auto cur=dummy;
        while(cur->next)
        {   
            auto p=cur->next;
            auto q=p->next;
            while(q&&p->val==q->val) q=q->next;
            if(p->next==q)
            {
                cur=cur->next;
            }
            else
            {
                cur->next=q;
            }
        }
        return dummy->next;
    }
    
    //递归
    ListNode* deleteDuplicates(ListNode* head) {
        if(!head) return head;
        if(head->next&&head->val==head->next->val)
        {
            while(head->next&&head->val==head->next->val)
            {
                head=head->next;
            }
            return deleteDuplicates(head->next);
        }
        else
        {
            head->next=deleteDuplicates(head->next);
        }
        return head;
    }
```
