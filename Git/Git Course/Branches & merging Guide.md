- For list, create or delete a branch:
```
git branch
```
- For making a new branch in your repository:
```
git branch <name>
```
- For deleting a branch from your repository:
```
git branch -d <name>
```
- For deleting forcefully a branch from your repository:
```
git branch -D <name>
```
- For changing your active branch:
```
git checkout <branch>
```
- For making a branch and active that branch for working in it at the same time:
```
git checkout -b <new-branch>
```
- For merging a branch into the active branch:
```
git merge <branch>
```
- For using only if **conflict** happens in merging. This command undo the merging and try to back the state before merging:
```
git merge --abort
```
- For printing (showing) an ASCII chart of commits and merges. It helps to see better what's happened:
```
git log --graph
```
- For showing a summery of commits:
```
git log --oneline
```
