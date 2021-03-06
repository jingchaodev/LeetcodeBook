#### Question
Given a binary tree, find all of its path sum. The path doesn’t need to start from root and end at leaf. But it has to be straight down.
#### Examples
Given 1,2,3,#,4,2,#,3, return [2,4], [1,3,2]
#### Analysis
Actually this is a question using backtracking. It’s kind of similar to traverse method. But it's different with other path sum problems, we don't decrease sum in every step, instead we keep the sum as same.
#### Code
```java
public List<List<Integer>> binaryTreePathSum2(TreeNode root, int target) {
    List<List<Integer>> res = new ArrayList<>();
    List<Integer> buffer = new ArrayList<>();
    helper(res, buffer, root, target);
    return res;
}
    
private void helper(List<List<Integer>> res, List<Integer> buffer, TreeNode root, int sum) {
    if (root == null) {
        return;
    }
    int temp = sum;
    buffer.add(root.val);
    int level = buffer.size();
    for (int i = level - 1; i >= 0; i--) {
        temp -= buffer.get(i);
        if (temp == 0) {
            List<Integer> list = new ArrayList<>();
            for (int j = i; j < level; j++) {
                list.add(buffer.get(j));
            }
            res.add(list);
        }
    }
    helper(res, buffer, root.left, sum);
    helper(res, buffer, root.right, sum);
    buffer.remove(buffer.size() - 1);
}
```