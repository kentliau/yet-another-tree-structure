


# Tree/node class #
Core class elements.
For full code see: [TreeNode.java](http://code.google.com/p/yet-another-tree-structure/source/browse/trunk/java/src/com/tree/TreeNode.java)
```
public class TreeNode<T> implements Iterable<TreeNode<T>> {

	public T data;
	public TreeNode<T> parent;
	public List<TreeNode<T>> children;

	public TreeNode(T data) {
		this.data = data;
		this.children = new LinkedList<TreeNode<T>>();
	}

	public TreeNode<T> addChild(T child) {
		TreeNode<T> childNode = new TreeNode<T>(child);
		childNode.parent = this;
		this.children.add(childNode);
		return childNode;
	}

	// other features ...

}
```

# Sample 1: creating tree #
Code to build tree of strings.
Note using null in one of children.
```
TreeNode<String> root = new TreeNode<String>("root");
{
	TreeNode<String> node0 = root.addChild("node0");
	TreeNode<String> node1 = root.addChild("node1");
	TreeNode<String> node2 = root.addChild("node2");
	{
		TreeNode<String> node20 = node2.addChild(null);
		TreeNode<String> node21 = node2.addChild("node21");
		{
			TreeNode<String> node210 = node21.addChild("node210");
			TreeNode<String> node211 = node21.addChild("node211");
		}
	}
	TreeNode<String> node3 = root.addChild("node3");
	{
		TreeNode<String> node30 = node3.addChild("node30");
	}
}
```

# Sample 2: iterating through nodes #
Go through the tree with standard Iterator`<T>`.
```
TreeNode<String> treeRoot = SampleData.getSet1();
for (TreeNode<String> node : treeRoot) {
	String indent = createIndent(node.getLevel());
	System.out.println(indent + node.data);
}
```

Output:
```
root
 node0
 node1
 node2
  null
  node21
   node210
   node211
 node3
  node30
```

# Sample 3: searching for node #
To search define search criteria with Comparable`<T>`.
```
Comparable<String> searchCriteria = new Comparable<String>() {
	@Override
	public int compareTo(String treeData) {
		if (treeData == null)
			return 1;
		boolean nodeOk = treeData.contains("210");
		return nodeOk ? 0 : 1;
	}
};

TreeNode<String> treeRoot = SampleData.getSet1();
TreeNode<String> found = treeRoot.findTreeNode(searchCriteria);
```
Output:
```
Found: node210
```

# Tnx #
If you like this tree -> don't forget to vote up ;] Tnx!

http://stackoverflow.com/a/17490124