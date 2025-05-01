# LAT - Local Aligment Tools
# Creste Locator

import maya.cmds as cmds

sel = cmds.ls(os=1)
c = 0
listLocator = []
for x in sel:
    loc = cmds.spaceLocator(n=x+'_LOC'+str(c))[0]
    cmds.delete(cmds.parentConstraint(x, loc, mo=0))
    c += 1
    listLocator.append(loc)
if sel == []:
    loc = cmds.spaceLocator(n='C_locator0_LOC')[0]
    listLocator.append(loc)
cmds.select(listLocator)
