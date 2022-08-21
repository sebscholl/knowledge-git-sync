# Code Module (debugger)

Last Edited: December 19, 2019 11:43 PM

#Import code module

import code

# Place where you want to pry

code.interact(local=dict(globals(), **locals()))

Follow up with Shlafman