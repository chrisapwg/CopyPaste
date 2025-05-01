# Grouping Object to 0

import maya.cmds as cmds

selected = cmds.ls(selection=True)
nameGRP = '_pos'

for sel in selected:
    i = str(sel)
    iSplit = i.split('_')
    iTotalNumber = len(i)
    iSplitLast = len(iSplit[-1])
    iNumber = iTotalNumber - iSplitLast - 1
    iName = i[:iNumber]

    # Check if the object has a parent
    checkParent = []
    try:
        checkParent = cmds.listRelatives(sel, parent=True) or []
    except Exception:
        pass

    # Create group with modified naming convention
    if len(iSplit) <= 1:
        createGroup = cmds.group(empty=True, name=sel + nameGRP)
    else:
        createGroup = cmds.group(empty=True, name=iName + nameGRP)

    # Position the group at the object's location
    cmds.delete(cmds.parentConstraint(i, createGroup))
    cmds.delete(cmds.scaleConstraint(i, createGroup))
    cmds.parent(i, createGroup)

    # Reparent group to the original parent, if any
    if checkParent:
        cmds.parent(createGroup, checkParent[0])

    # Select the original objects after grouping
    cmds.select(selected)
