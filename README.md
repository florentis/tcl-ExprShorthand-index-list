This is the patch of **Tcl 9.1a1** source distribution, including a shorthand for expr.

With these files, you should be able to write :
* using main shorthand :
> set A [(1+1)]; # eq to : set A [expr {1+1}].
* using index shorthand :
> set B[(1+1)] 1; #  eq to : set B([expr {1+1}]) 1
* using native list capabilities :
> set L [((1,0,0),(0,1,0),(0,0,1))]; # eq to set L [list [list 1 0 0] [list 0 1 0] [list 0 0 1]]
>

**Example** :

    proc MatrixTranspose {M} {
        set i 1
        foreach row $M {
        	lassign $row m${i}1 m${i}2 m${i}3
        	incr i
        }
        set R []
        return [(
    	     ($m11, $m21, $m31),
    	     ($m12, $m22, $m32),
    	     ($m13, $m23, $m33)
    	  )]
    }
    proc MatrixProduct {M1 M2} {
         set i 1
         foreach row $M1 {
	         lassign $row m${i}1 m${i}2 m${i}3
	         incr i
         }
         set R []
         foreach v [MatrixTranspose $M2] {
	          lassign $v x y z
            lappend R [(
               $m11*$x + $m12*$y + $m13*$z,
               $m21*$x + $m22*$y + $m23*$z,
               $m31*$x + $m32*$y + $m33*$z
            )]
         }
         return [MatrixTranspose $R]
     }
     
     set M1 {{1 2 3} {4 5 6} {7 8 9}}
     set M2 {{2 0 0} {0 2 0} {0 0 2}}
     puts $M1
     puts [MatrixTranspose $M2]
     puts [MatrixProduct $M1 $M2]
