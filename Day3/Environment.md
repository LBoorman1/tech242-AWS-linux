# Environment Variables

`MYNAME=luke` - creates a variable
`export MYNAME=luke` - creates an environment variable

To make environment variable persist after logging out, add it to .bashrc

Environment variables can be accessed anywhere in the VM compared to regular variables that can only be accessed
from within a script.

This is useful if a variable is needed in another process.