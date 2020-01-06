# Notebook-Checker
A non-intrusive tool for maintaining Jupyter/IPython notebooks and encouraging safe coding prectices. Designed to aleviate some common issues that arise when sharing a directory of notebooks with multiple people. These issues can result in notebooks that appear to be working but actually have a bug that prevents them from being reproduced or shared.

Here are some common issues that can be automatically flagged.

* A notebook only runs because of variables remembered by the kernel.
* A notebook only runs if the cells are run out of order, or some cells are skipped.
* A notebook creates/modifies/deletes a file that is accessed by another notebook.
* A notebook requires some files outside of the target directory.


This tool will never modify any of your files. It operates by taking snapshots of a directory. The snapshots include files and subdirectories but not python kernels. Notebooks' output cells are also discounted, so it does not matter if a notebook is left running. 

Periodic checks are conducted as follows:

1. take a snapshot of the target directory
2. for each notebook in the snapshot,
    1. restore the entire directory snapshot to a temporary working directory
    2. run the notebook programmatically 
    3. record files accessed by the notebook (read, created, modified, or deleted)
    4. record any errors that prevented the notebook from running fully.
3. report or flag notebooks that had errors
4. check for any files that were modified by one notebook and accessed by another. Flag both notebooks as a potential issue. (They may be dependant on eachother, or they may not coexist)

  
