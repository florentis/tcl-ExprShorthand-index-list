This is the patch of **Tcl 9.1a1** source distribution, including a shorthand for expr.

With these files, you should be able to write :
* using main shorthand :
> set A [(1+1)]; # eq to : set A [expr {1+1}].
* using index shorthand :
> set B[(1+1)] 1; #  eq to : set B([expr {1+1}]) 1
* using native list capabilities :
> set L [((1,0,0),(0,1,0),(0,0,1))]; # eq to set L {{1 0 0} {0 1 0} {0 0 1}}
