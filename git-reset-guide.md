When you modify a file in your repository, the change is initially unstaged. In order to commit it, you must stage it—that is, add it to the index—using <code>git add</code>. When you make a commit, the changes that are committed are those that have been added to the index.

<code>git reset</code> changes, at minimum, where your current branch is pointing. The difference between <code>--mixed</code> and <code>--soft</code> is whether or not your index is also modified. So, if we're on branch <code>master</code> with this series of commits:

    - A - B - C (master)

<code>HEAD</code>points to <code>C</code> and the index matches <code>C</code>.

** --soft

When we run <code>git reset --soft B</code>, **<code>master</code> (and thus <code>HEAD</code>) now points to <code>B</code>**, but the index still has the changes from <code>C</code>; <code>git status</code> will **show them as staged**. So if we run <code>git commit</code> at this point, we'll get a new commit with the same changes as <code>C</code>.

----------

** --mixed

Okay, so starting from here again:

    - A - B - C (master)

Now let's do <code>git reset --mixed B</code>. Once again, <code>master</code> and <code>HEAD</code> point to B, but this time the index is also modified to match <code>B</code>. If we run <code>git commit</code> at this point, nothing will happen since the index matches <code>HEAD</code>. We **still have the changes in the working directory**, but since they're not in the index, <code>git status</code> shows them as **unstaged**. To commit them, you would <code>git add</code> and then commit as usual.

----------

** --hard

And finally, <code>--hard</code> is the same as <code>--mixed</code> (it changes your <code>HEAD</code> and index), except that <code>--hard</code> **also modifies your working directory**. If we're at <code>C</code> and run <code>git reset --hard B</code>, then the changes added in <code>C</code>, as well as any uncommitted changes you have, will be removed, and the files in your working copy will match commit <code>B</code>. Since you can permanently lose changes this way, you should always run <code>git status</code> before doing a hard reset to make sure your working directory is clean or that you're okay with losing your uncommitted changes.