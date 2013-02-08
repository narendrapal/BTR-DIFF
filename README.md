Efficient storage and retrieval of data has always been of utmost importance. The BtrFs file system is a copy-on-write 
(COW) based B-tree file system that has an in-built support for snapshots and is considered a potential replacement
for the EXT4 file system. Snapshots are useful to have local online “copies” of the file system that can be referred back
to, or to implement a form of de-duplication, or for taking a full backup of the file system. Ability to compare 
snapshots becomes crucial for the system administrators as well as end users. The existing snapshot management tools
perform directory based comparison on block level in user space.

Our objective is to leverage the BtrFs 'send' code in the kernel to implement a new mechanism to list all the files
that have been added, removed, changed or had their metadata changed in some way. The 'send' code does the tree 
compare in kernel space  using the on-disk metadata format (rather than the abstract 'stat' format exported to the 
user space), which includes the ability to recognize when entire sub-trees can be skipped. This solution finds usage
when daily incremental backups of the file system are to be taken and can be very easily integrated with existing
snapshot management tools.
