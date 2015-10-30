


# Tree/node class #
Core class elements.
For full code see: [TreeNode.cs](http://code.google.com/p/yet-another-tree-structure/source/browse/trunk/csharp/CSharpTree/TreeNode.cs)
```
public class TreeNode<T> : IEnumerable<TreeNode<T>>
{

    public T Data { get; set; }
    public TreeNode<T> Parent { get; set; }
    public ICollection<TreeNode<T>> Children { get; set; }


    public TreeNode(T data)
    {
        this.Data = data;
        this.Children = new LinkedList<TreeNode<T>>();
    }

    public TreeNode<T> AddChild(T child)
    {
        TreeNode<T> childNode = new TreeNode<T>(child) { Parent = this };
        this.Children.Add(childNode);
        return childNode;
    }

    // other features ...
}
```

# Sample 1: creating tree #
Code to build tree of strings.
Note using null in one of children.
```
TreeNode<string> root = new TreeNode<string>("root");
{
    TreeNode<string> node0 = root.AddChild("node0");
    TreeNode<string> node1 = root.AddChild("node1");
    TreeNode<string> node2 = root.AddChild("node2");
    {
        TreeNode<string> node20 = node2.AddChild(null);
        TreeNode<string> node21 = node2.AddChild("node21");
        {
            TreeNode<string> node210 = node21.AddChild("node210");
            TreeNode<string> node211 = node21.AddChild("node211");
        }
    }
    TreeNode<string> node3 = root.AddChild("node3");
    {
        TreeNode<string> node30 = node3.AddChild("node30");
    }
}
```

# Sample 2: iterating through nodes #
Go through the tree with standard IEnumerable`<T>`.
```
TreeNode<string> treeRoot = SampleData.GetSet1();
foreach (TreeNode<string> node in treeRoot)
{
    string indent = CreateIndent(node.Level);
    Console.WriteLine(indent + (node.Data ?? "null"));
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
TreeNode<string> treeRoot = SampleData.GetSet1();
TreeNode<string> found = treeRoot.FindTreeNode(node => node.Data != null && node.Data.Contains("210"));
Console.WriteLine("Found: " + found);
```
Output:
```
Found: node210
```

# Tnx #
If you like this tree -> don't forget to vote up ;] Tnx!

http://stackoverflow.com/a/18774221/1367449