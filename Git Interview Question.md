#

## Q. 
The `merge` and `rebase` commands in Git serve to integrate changes from one branch into another, but they do so in fundamentally different ways, leading to different outcomes in the commit history. 
### Merge 
The `merge` command creates a new "merge commit" in the target branch that joins the histories of the two branches being merged. This approach preserves the entire history of both branches, showing exactly when and how they diverged and were rejoined. 
```git
git checkout target_branch
git merge source_branch
```

### Rebase 
The `rebase` command, on the other hand, rewrites the commit history of the source branch by moving its commits on top of the target branch. This results in a linear history, as if the source branch was created directly from the latest commit of the target branch. 
```git
git checkout source_branch
git rebase target_branch
```

### Key Differences 

| Feature | Merge | Rebase  |
| --- | --- | --- |
| Commit History | Preserves the entire history, including branches and merges | Rewrites history to create a linear sequence of commits  |
| Merge Commits | Introduces merge commits to join branches | Avoids merge commits, resulting in a cleaner history  |
| Complexity | Simpler to understand and use | Can be more complex, especially when resolving conflicts  |
| Safety | Generally safer, as it doesn't rewrite history | Can be risky if the rebased branch has been shared with others, as it changes the commit IDs  |
| Use Cases | Suitable for teams that prefer to maintain a detailed history of all changes | Ideal for individuals or small teams that prioritize a clean, linear history  |
| Conflict Resolution | Resolves conflicts in a single merge commit | Resolves conflicts commit by commit, which can be more time-consuming  |

### Choosing Between Merge and Rebase 

- Use `merge` when it's important to preserve the complete history of changes, or when working in a team where rewriting history could cause issues. 
- Use `rebase` when a clean, linear history is desired, or when preparing a feature branch for merging into the main branch. 
