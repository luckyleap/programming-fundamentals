# Delete From BST
You're given a binary search tree t and an array of numbers queries. Your task is to remove queries[0], queries[1], etc., from t, step by step, following the algorithm above. Return the resulting BST. [More Details...](https://codefights.com/interview-practice/task/oZXs4td52fsdWC9kR)

## Hint 1
Use recursion to search through the nodes for values and delete

## Hint 2
Deleting a node with two child requires finding the smallest of the right child or the largest of the left child and replacing it with the current node

## Algorithm
To delete a BST node there are 3 scenarios (Deleting the given node):
1. Either node's left is none OR node's right is none
2. Both node's children 
3. Node is none

If node only has one child, set node's parent to node's child
If both children -> you can replace either the smallest of the right child or the largest of the left child
If node is none return none

Knowing this, you can simply traverse through the tree looking for the key and then once the node has the key you delete the node. To traverse: If key is less than current node, you will search the left tree as values are less than current node's value. If key is greater than current node, you will search the right tree as values are greater than current node's value

Example:

![](http://www.algolist.net/img/bst-remove-case-3-3.png)
![](http://www.algolist.net/img/bst-remove-case-3-4.png)
![](http://www.algolist.net/img/bst-remove-case-3-5.png)
![](http://www.algolist.net/img/bst-remove-case-3-6.png)

## Code

```python
# Search function for the largest value of the left subtree
def searchMin(node):
    if node is None:
        return node
    while node.right is not None:
        node = node.right
    
    return node
```

```python
# Search for the value, then delete node with the value
def deleteNode(node, key):
    if node is None:
        return node
    
    if node.value < key:
        node.right = deleteNode(node.right, key)
    elif node.value > key:
        node.left = deleteNode(node.left, key)
    else:
        # Delete current node
        if node.left is None:
            temp = node.right
            node = None
            return temp
        elif node.right is None:
            temp = node.left
            node = None
            return temp
        else:
            # print(node.value, node.left.value, node.right.value)
            # Search for min node and delete current node while replacing min node
            minNode = searchMin(node.left)
            # print(minNode.value)
            if minNode is None:
                return node
            else:
                node.value = minNode.value
                node.left = deleteNode(node.left, minNode.value)
    
    return node
```