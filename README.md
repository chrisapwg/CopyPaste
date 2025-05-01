# Control Library
# By Chris Gultom

import maya.cmds as cmds

windowName_CL = 'controlLibrary'
windowTitle_CL = 'Control Library'
titleText_CL = 'Simple Control Library'
sizeHeight_CL = 275
sizeWidth_CL = 310
holderSize_CL = 10
sliceText_CL = '# ---------------------------------------------------------------------- #'

CTL_name = '_ctl'
GRP_name = '_pos'
TRN_name = '_trn'
JNT_name = '_jnt'
C_side = 'M_'
L_side = 'L_'
R_side = 'R_'
yellowColor = 17
orangeColor = 21
redColor = 13
cherryColor = 20
blueColor = 6
blueseaColor = 18

# --- Define ---

findNameResult = []
def findName(sel):
    global findNameResult
    i = str(sel)
    iSplit = i.split('_')
    iTotalNumber = len(i)
    iSplitLast = len(iSplit[-1])
    iNumber = iTotalNumber - iSplitLast
    ina = i[:iNumber-1]
    findNameResult = ina

findNameLastResult = []
def findNameLast(sel):
    global findNameLastResult
    i = str(sel)
    iSplit = i.split('_')
    iTotalNumber = len(i)
    iSplitLast = len(iSplit[-1])
    iNumber = iTotalNumber - iSplitLast
    ina = i[iNumber-1:]
    findNameLastResult = ina

###

def shapeChange0_CL(o, shapeColor, shapeBold):
    shapeList = cmds.listRelatives(o, s=1)
    print (o)
    print (shapeList)
    
    if shapeList != None:
        for i in shapeList:
            cmds.delete(i)
        
    CTL = cmds.circle(n='{}TEMP'.format(o), normalX=0, normalY=0, normalZ=0)
    cmds.rename(cmds.listRelatives(CTL[0], s=1), '{}Shape'.format(o))
    try:
        cmds.setAttr('{}Shape.overrideEnabled'.format(o), 1)
        cmds.setAttr('{}Shape.overrideColor'.format(o), shapeColor)
        cmds.setAttr('{}Shape.lineWidth'.format(o), shapeBold)
    except:
        pass
    
    cmds.setAttr('{}.sections'.format(CTL[1]), 10)
    cmds.setAttr('{}.degree'.format(CTL[1]), 1)
    cmds.addAttr(CTL[0], ln='radius', at='double', k=0, dv=1)
    cmds.setAttr('{}.radius'.format(CTL[0]), l=1)
    cmds.addAttr(CTL[0], ln='shapeType', dt='string')
    cmds.setAttr('{}.shapeType'.format(CTL[0]), 'star', type='string', l=1)
    
    cmds.select('{}.cv[0]'.format(CTL[0]))
    cmds.move(0.25, 0, -1)
    cmds.select('{}.cv[1]'.format(CTL[0]))
    cmds.move(0.5, 0, -1)
    cmds.select('{}.cv[2]'.format(CTL[0]))
    cmds.move(0, 0, -2)
    cmds.select('{}.cv[3]'.format(CTL[0]))
    cmds.move(-0.5, 0, -1)
    cmds.select('{}.cv[4]'.format(CTL[0]))
    cmds.move(-0.25, 0, -1)
    cmds.select('{}.cv[5]'.format(CTL[0]))
    cmds.move(-0.25, 0, 1)
    cmds.select('{}.cv[6]'.format(CTL[0]))
    cmds.move(-0.5, 0, 1)
    cmds.select('{}.cv[7]'.format(CTL[0]))
    cmds.move(0, 0, 2)
    cmds.select('{}.cv[8]'.format(CTL[0]))
    cmds.move(0.5, 0, 1)
    cmds.select('{}.cv[9]'.format(CTL[0]))
    cmds.move(0.25, 0, 1)
    cmds.select('{}.cv[10]'.format(CTL[0]))
    cmds.move(0.25, 0, -1)
    
    DUP1 = cmds.duplicate(CTL[0], n='{}1'.format(o), rc=True)
    cmds.rename(cmds.listRelatives(DUP1[0], s=1), '{}Shape1'.format(o))
    cmds.select('{}.cv[0:10]'.format(DUP1[0]))
    cmds.rotate(90, 0, 0)
    
    DUP2 = cmds.duplicate(CTL[0], n='{}2'.format(o), rc=True)
    cmds.rename(cmds.listRelatives(DUP2[0], s=1), '{}Shape2'.format(o))
    cmds.select('{}.cv[0:10]'.format(DUP2[0]))
    cmds.rotate(0, 0, 90)
    
    DUP3 = cmds.duplicate(CTL[0], n='{}3'.format(o), rc=True)
    cmds.rename(cmds.listRelatives(DUP3[0], s=1), '{}Shape3'.format(o))
    cmds.select('{}.cv[0:10]'.format(DUP3[0]))
    cmds.rotate(90, 90, 0)
    
    DUP4 = cmds.duplicate(CTL[0], n='{}4'.format(o), rc=True)
    cmds.rename(cmds.listRelatives(DUP4[0], s=1), '{}Shape4'.format(o))
    cmds.select('{}.cv[0:10]'.format(DUP4[0]))
    cmds.rotate(0, 90, 0)
    
    DUP5 = cmds.duplicate(CTL[0], n='{}5'.format(o), rc=True)
    cmds.rename(cmds.listRelatives(DUP5[0], s=1), '{}Shape5'.format(o))
    cmds.select('{}.cv[0:10]'.format(DUP5[0]))
    cmds.rotate(90, 0, 90)
    
    cmds.delete(CTL[0], ch=1)
    cmds.parent('{}Shape'.format(o), o, add=1, s=1)
    cmds.delete(CTL[0])
    cmds.select(o)
    
    cmds.parent('{}Shape1'.format(o), o, add=1, s=1)
    cmds.delete(DUP1[0])
    
    cmds.parent('{}Shape2'.format(o), o, add=1, s=1)
    cmds.delete(DUP2[0])
    
    cmds.parent('{}Shape3'.format(o), o, add=1, s=1)
    cmds.delete(DUP3[0])
    
    cmds.parent('{}Shape4'.format(o), o, add=1, s=1)
    cmds.delete(DUP4[0])
    
    cmds.parent('{}Shape5'.format(o), o, add=1, s=1)
    cmds.delete(DUP5[0])
    
def shapeChange1_CL(o, shapeColor, shapeBold):
    shapeList = cmds.listRelatives(o, s=1)
    
    for i in shapeList:
        cmds.delete(i)
        
    CTL = cmds.circle(n='{}TEMP'.format(o), normalX=0, normalY=0, normalZ=0)
    cmds.rename(cmds.listRelatives(CTL[0], s=1), '{}Shape'.format(o))
    try:
        cmds.setAttr('{}Shape.overrideEnabled'.format(o), 1)
        cmds.setAttr('{}Shape.overrideColor'.format(o), shapeColor)
        cmds.setAttr('{}Shape.lineWidth'.format(o), shapeBold)
    except:
        pass
    
    cmds.setAttr('{}.sections'.format(CTL[1]), 7)
    cmds.setAttr('{}.degree'.format(CTL[1]), 1)
    cmds.addAttr(CTL[0], ln='radius', at='double', k=0, dv=1)
    cmds.setAttr('{}.radius'.format(CTL[0]), l=1)
    cmds.addAttr(CTL[0], ln='shapeType', dt='string')
    cmds.setAttr('{}.shapeType'.format(CTL[0]), 'arrow', type='string', l=1)
    
    cmds.select('{}.cv[0]'.format(CTL[0]))
    cmds.move(2.5, 0, 0.25)
    cmds.select('{}.cv[1]'.format(CTL[0]))
    cmds.move(2.5, 0, -0.25)
    cmds.select('{}.cv[2]'.format(CTL[0]))
    cmds.move(2, 0, -0.25)
    cmds.select('{}.cv[3]'.format(CTL[0]))
    cmds.move(2, 0, -0.5)
    cmds.select('{}.cv[4]'.format(CTL[0]))
    cmds.move(1.5, 0, 0)
    cmds.select('{}.cv[5]'.format(CTL[0]))
    cmds.move(2, 0, 0.5)
    cmds.select('{}.cv[6]'.format(CTL[0]))
    cmds.move(2, 0, 0.25)
    cmds.select('{}.cv[7]'.format(CTL[0]))
    cmds.move(2.5, 0, 0.25)
    
    DUP1 = cmds.duplicate(CTL[0], n='{}1'.format(o), rc=True)
    cmds.rename(cmds.listRelatives(DUP1[0], s=1), '{}Shape1'.format(o))
    cmds.select('{}.cv[0:10]'.format(DUP1[0]))
    cmds.rotate(0, 0, 90)
    
    DUP2 = cmds.duplicate(CTL[0], n='{}2'.format(o), rc=True)
    cmds.rename(cmds.listRelatives(DUP2[0], s=1), '{}Shape2'.format(o))
    cmds.select('{}.cv[0:10]'.format(DUP2[0]))
    cmds.rotate(0, 0, 180)
    
    DUP3 = cmds.duplicate(CTL[0], n='{}3'.format(o), rc=True)
    cmds.rename(cmds.listRelatives(DUP3[0], s=1), '{}Shape3'.format(o))
    cmds.select('{}.cv[0:10]'.format(DUP3[0]))
    cmds.rotate(0, 0, 270)
    
    cmds.delete(CTL[0], ch=1)
    cmds.parent('{}Shape'.format(o), o, add=1, s=1)
    cmds.delete(CTL[0])
    cmds.select(o)
    
    cmds.parent('{}Shape1'.format(o), o, add=1, s=1)
    cmds.delete(DUP1[0])
    
    cmds.parent('{}Shape2'.format(o), o, add=1, s=1)
    cmds.delete(DUP2[0])
    
    cmds.parent('{}Shape3'.format(o), o, add=1, s=1)
    cmds.delete(DUP3[0])
    
def shapeChange2_CL(o, shapeColor, shapeBold):
    shapeList = cmds.listRelatives(o, s=1)
    
    for i in shapeList:
        cmds.delete(i)
        
    CTL = cmds.circle(n='{}TEMP'.format(o), normalX=0, normalY=0, normalZ=0)
    cmds.rename(cmds.listRelatives(CTL[0], s=1), '{}Shape'.format(o))
    try:
        cmds.setAttr('{}Shape.overrideEnabled'.format(o), 1)
        cmds.setAttr('{}Shape.overrideColor'.format(o), shapeColor)
        cmds.setAttr('{}Shape.lineWidth'.format(o), shapeBold)
    except:
        pass
    
    cmds.setAttr('{}.sections'.format(CTL[1]), 7)
    cmds.setAttr('{}.degree'.format(CTL[1]), 1)
    cmds.addAttr(CTL[0], ln='radius', at='double', k=0, dv=1)
    cmds.setAttr('{}.radius'.format(CTL[0]), l=1)
    cmds.addAttr(CTL[0], ln='shapeType', dt='string')
    cmds.setAttr('{}.shapeType'.format(CTL[0]), 'flatArrow', type='string', l=1)
    
    cmds.select('{}.cv[0]'.format(CTL[0]))
    cmds.move(-2, 0, -1)
    cmds.select('{}.cv[1]'.format(CTL[0]))
    cmds.move(-2, 0, 1)
    cmds.select('{}.cv[2]'.format(CTL[0]))
    cmds.move(0, 0, 1)
    cmds.select('{}.cv[3]'.format(CTL[0]))
    cmds.move(0, 0, 2)
    cmds.select('{}.cv[4]'.format(CTL[0]))
    cmds.move(2, 0, 0)
    cmds.select('{}.cv[5]'.format(CTL[0]))
    cmds.move(0, 0, -2)
    cmds.select('{}.cv[6]'.format(CTL[0]))
    cmds.move(0, 0, -1)
    cmds.select('{}.cv[7]'.format(CTL[0]))
    cmds.move(-2, 0, -1)
    
    cmds.delete(CTL[0], ch=1)
    cmds.parent('{}Shape'.format(o), o, add=1, s=1)
    cmds.delete(CTL[0])
    cmds.select(o)
    
    for o in cmds.listRelatives(o, s=1):
        cmds.select(o+'.cv[*]')
        cmds.rotate(0, 0, 270)
    cmds.select(o)
        
def shapeChange3_CL(o, shapeColor, shapeBold):
    shapeList = cmds.listRelatives(o, s=1)
    
    for i in shapeList:
        cmds.delete(i)
        
    CTL = cmds.circle(n='{}TEMP'.format(o), normalX=0, normalY=0, normalZ=0)
    cmds.rename(cmds.listRelatives(CTL[0], s=1), '{}Shape'.format(o))
    try:
        cmds.setAttr('{}Shape.overrideEnabled'.format(o), 1)
        cmds.setAttr('{}Shape.overrideColor'.format(o), shapeColor)
        cmds.setAttr('{}Shape.lineWidth'.format(o), shapeBold)
    except:
        pass
    
    cmds.setAttr('{}.sections'.format(CTL[1]), 20)
    cmds.setAttr('{}.degree'.format(CTL[1]), 1)
    cmds.addAttr(CTL[0], ln='radius', at='double', k=0, dv=1)
    cmds.setAttr('{}.radius'.format(CTL[0]), l=1)
    cmds.addAttr(CTL[0], ln='shapeType', dt='string')
    cmds.setAttr('{}.shapeType'.format(CTL[0]), 'rotationArrow', type='string', l=1)
    
    cmds.select('{}.cv[0]'.format(CTL[0]))
    cmds.move(0.5, 0.7, 0)
    cmds.select('{}.cv[1]'.format(CTL[0]))
    cmds.move(0.5, 0.65, -0.5)
    cmds.select('{}.cv[2]'.format(CTL[0]))
    cmds.move(0.5, 0.45, -1)
    cmds.select('{}.cv[3]'.format(CTL[0]))
    cmds.move(1, 0.45, -1)
    cmds.select('{}.cv[4]'.format(CTL[0]))
    cmds.move(0.5, 0.25, -1.5)
    cmds.select('{}.cv[5]'.format(CTL[0]))
    cmds.move(0, 0, -2)
    cmds.select('{}.cv[6]'.format(CTL[0]))
    cmds.move(-0.5, 0.25, -1.5)
    cmds.select('{}.cv[7]'.format(CTL[0]))
    cmds.move(-1, 0.45, -1)
    cmds.select('{}.cv[8]'.format(CTL[0]))
    cmds.move(-0.5, 0.45, -1)
    cmds.select('{}.cv[9]'.format(CTL[0]))
    cmds.move(-0.5, 0.65, -0.5)
    cmds.select('{}.cv[10]'.format(CTL[0]))
    cmds.move(-0.5, 0.7, 0)
    cmds.select('{}.cv[11]'.format(CTL[0]))
    cmds.move(-0.5, 0.65, 0.5)
    cmds.select('{}.cv[12]'.format(CTL[0]))
    cmds.move(-0.5, 0.45, 1)
    cmds.select('{}.cv[13]'.format(CTL[0]))
    cmds.move(-1, 0.45, 1)
    cmds.select('{}.cv[14]'.format(CTL[0]))
    cmds.move(-0.5, 0.25, 1.5)
    cmds.select('{}.cv[15]'.format(CTL[0]))
    cmds.move(0, 0, 2)
    cmds.select('{}.cv[16]'.format(CTL[0]))
    cmds.move(0.5, 0.25, 1.5)
    cmds.select('{}.cv[17]'.format(CTL[0]))
    cmds.move(1, 0.45, 1)
    cmds.select('{}.cv[18]'.format(CTL[0]))
    cmds.move(0.5, 0.45, 1)
    cmds.select('{}.cv[19]'.format(CTL[0]))
    cmds.move(0.5, 0.65, 0.5)
    cmds.select('{}.cv[20]'.format(CTL[0]))
    cmds.move(0.5, 0.7, 0)
    
    cmds.delete(CTL[0], ch=1)
    cmds.parent('{}Shape'.format(o), o, add=1, s=1)
    cmds.delete(CTL[0])
    cmds.select(o)
    
def shapeChange4_CL(o, shapeColor, shapeBold):
    shapeList = cmds.listRelatives(o, s=1)
    
    for i in shapeList:
        cmds.delete(i)
        
    CTL = cmds.circle(n='{}TEMP'.format(o), normalX=0, normalY=0, normalZ=0)
    cmds.rename(cmds.listRelatives(CTL[0], s=1), '{}Shape'.format(o))
    try:
        cmds.setAttr('{}Shape.overrideEnabled'.format(o), 1)
        cmds.setAttr('{}Shape.overrideColor'.format(o), shapeColor)
        cmds.setAttr('{}Shape.lineWidth'.format(o), shapeBold)
    except:
        pass
    
    cmds.setAttr('{}.sections'.format(CTL[1]), 40)
    cmds.setAttr('{}.degree'.format(CTL[1]), 1)
    cmds.addAttr(CTL[0], ln='radius', at='double', k=0, dv=1)
    cmds.setAttr('{}.radius'.format(CTL[0]), l=1)
    cmds.addAttr(CTL[0], ln='shapeType', dt='string')
    cmds.setAttr('{}.shapeType'.format(CTL[0]), 'moveArrow', type='string', l=1)
    
    cmds.select('{}.cv[0]'.format(CTL[0]))
    cmds.move(0.5, 0.725, -0.5)
    cmds.select('{}.cv[1]'.format(CTL[0]))
    cmds.move(0.5, 0.65, -0.9)
    cmds.select('{}.cv[2]'.format(CTL[0]))
    cmds.move(0.5, 0.5, -1.25)
    cmds.select('{}.cv[3]'.format(CTL[0]))
    cmds.move(1, 0.5, -1.25)
    cmds.select('{}.cv[4]'.format(CTL[0]))
    cmds.move(0.5, 0.275, -1.625)
    cmds.select('{}.cv[5]'.format(CTL[0]))
    cmds.move(0, 0, -2)
    cmds.select('{}.cv[6]'.format(CTL[0]))
    cmds.move(-0.5, 0.275, -1.625)
    cmds.select('{}.cv[7]'.format(CTL[0]))
    cmds.move(-1, 0.5, -1.25)
    cmds.select('{}.cv[8]'.format(CTL[0]))
    cmds.move(-0.5, 0.5, -1.25)
    cmds.select('{}.cv[9]'.format(CTL[0]))
    cmds.move(-0.5, 0.65, -0.9)
    cmds.select('{}.cv[10]'.format(CTL[0]))
    cmds.move(-0.5, 0.725, -0.5)
    
    cmds.select('{}.cv[11]'.format(CTL[0]))
    cmds.move(-0.9, 0.65, -0.5)
    cmds.select('{}.cv[12]'.format(CTL[0]))
    cmds.move(-1.25, 0.5, -0.5)
    cmds.select('{}.cv[13]'.format(CTL[0]))
    cmds.move(-1.25, 0.5, -1)
    cmds.select('{}.cv[14]'.format(CTL[0]))
    cmds.move(-1.625, 0.275, -0.5)
    cmds.select('{}.cv[15]'.format(CTL[0]))
    cmds.move(-2, 0, 0)
    cmds.select('{}.cv[16]'.format(CTL[0]))
    cmds.move(-1.625, 0.275, 0.5)
    cmds.select('{}.cv[17]'.format(CTL[0]))
    cmds.move(-1.25, 0.5, 1)
    cmds.select('{}.cv[18]'.format(CTL[0]))
    cmds.move(-1.25, 0.5, 0.5)
    cmds.select('{}.cv[19]'.format(CTL[0]))
    cmds.move(-0.9, 0.65, 0.5)
    cmds.select('{}.cv[20]'.format(CTL[0]))
    cmds.move(-0.5, 0.725, 0.5)
    
    cmds.select('{}.cv[21]'.format(CTL[0]))
    cmds.move(-0.5, 0.65, 0.9)
    cmds.select('{}.cv[22]'.format(CTL[0]))
    cmds.move(-0.5, 0.5, 1.25)
    cmds.select('{}.cv[23]'.format(CTL[0]))
    cmds.move(-1, 0.5, 1.25)
    cmds.select('{}.cv[24]'.format(CTL[0]))
    cmds.move(-0.5, 0.275, 1.625)
    cmds.select('{}.cv[25]'.format(CTL[0]))
    cmds.move(0, 0, 2)
    cmds.select('{}.cv[26]'.format(CTL[0]))
    cmds.move(0.5, 0.275, 1.625)
    cmds.select('{}.cv[27]'.format(CTL[0]))
    cmds.move(1, 0.5, 1.25)
    cmds.select('{}.cv[28]'.format(CTL[0]))
    cmds.move(0.5, 0.5, 1.25)
    cmds.select('{}.cv[29]'.format(CTL[0]))
    cmds.move(0.5, 0.65, 0.9)
    cmds.select('{}.cv[30]'.format(CTL[0]))
    cmds.move(0.5, 0.725, 0.5)
    
    cmds.select('{}.cv[31]'.format(CTL[0]))
    cmds.move(0.9, 0.65, 0.5)
    cmds.select('{}.cv[32]'.format(CTL[0]))
    cmds.move(1.25, 0.5, 0.5)
    cmds.select('{}.cv[33]'.format(CTL[0]))
    cmds.move(1.25, 0.5, 1)
    cmds.select('{}.cv[34]'.format(CTL[0]))
    cmds.move(1.625, 0.275, 0.5)
    cmds.select('{}.cv[35]'.format(CTL[0]))
    cmds.move(2, 0, 0)
    cmds.select('{}.cv[36]'.format(CTL[0]))
    cmds.move(1.625, 0.275, -0.5)
    cmds.select('{}.cv[37]'.format(CTL[0]))
    cmds.move(1.25, 0.5, -1)
    cmds.select('{}.cv[38]'.format(CTL[0]))
    cmds.move(1.25, 0.5, -0.5)
    cmds.select('{}.cv[39]'.format(CTL[0]))
    cmds.move(0.9, 0.65, -0.5)
    cmds.select('{}.cv[40]'.format(CTL[0]))
    cmds.move(0.5, 0.725, -0.5)
    
    cmds.delete(CTL[0], ch=1)
    cmds.parent('{}Shape'.format(o), o, add=1, s=1)
    cmds.delete(CTL[0])
    cmds.select(o)
            
def shapeChange5_CL(o, shapeColor, shapeBold):
    shapeList = cmds.listRelatives(o, s=1)
    
    for i in shapeList:
        cmds.delete(i)
        
    CTL = cmds.circle(n='{}TEMP'.format(o), normalX=0, normalY=0, normalZ=0)
    cmds.rename(cmds.listRelatives(CTL[0], s=1), '{}Shape'.format(o))
    try:
        cmds.setAttr('{}Shape.overrideEnabled'.format(o), 1)
        cmds.setAttr('{}Shape.overrideColor'.format(o), shapeColor)
        cmds.setAttr('{}Shape.lineWidth'.format(o), shapeBold)
    except:
        pass
    
    cmds.setAttr('{}.sections'.format(CTL[1]), 8)
    cmds.setAttr('{}.degree'.format(CTL[1]), 3)
    cmds.addAttr(CTL[0], ln='radius', at='double', k=0, dv=1)
    cmds.setAttr('{}.radius'.format(CTL[0]), l=1)
    cmds.addAttr(CTL[0], ln='shapeType', dt='string')
    cmds.setAttr('{}.shapeType'.format(CTL[0]), 'sphere', type='string', l=1)
    
    cmds.select('{}.cv[0]'.format(CTL[0]))
    cmds.move(0, 0, 2)
    cmds.select('{}.cv[1]'.format(CTL[0]))
    cmds.move(1.4, 0, 1.4)
    cmds.select('{}.cv[2]'.format(CTL[0]))
    cmds.move(2, 0, 0)
    cmds.select('{}.cv[3]'.format(CTL[0]))
    cmds.move(1.4, 0, -1.4)
    cmds.select('{}.cv[4]'.format(CTL[0]))
    cmds.move(0, 0, -2)
    cmds.select('{}.cv[5]'.format(CTL[0]))
    cmds.move(-1.4, 0, -1.4)
    cmds.select('{}.cv[6]'.format(CTL[0]))
    cmds.move(-2, 0, 0)
    cmds.select('{}.cv[7]'.format(CTL[0]))
    cmds.move(-1.4, 0, 1.4)
    
    DUP1 = cmds.duplicate(CTL[0], n='{}1'.format(o), rc=True)
    cmds.rename(cmds.listRelatives(DUP1[0], s=1), '{}Shape1'.format(o))
    cmds.select('{}.cv[0:7]'.format(DUP1[0]))
    cmds.rotate(90, 0, 0)
    
    DUP2 = cmds.duplicate(CTL[0], n='{}2'.format(o), rc=True)
    cmds.rename(cmds.listRelatives(DUP2[0], s=1), '{}Shape2'.format(o))
    cmds.select('{}.cv[0:7]'.format(DUP2[0]))
    cmds.rotate(0, 90, 0)
    
    cmds.delete(CTL[0], ch=1)
    cmds.parent('{}Shape'.format(o), o, add=1, s=1)
    cmds.delete(CTL[0])
    cmds.select(o)
    
    cmds.parent('{}Shape1'.format(o), o, add=1, s=1)
    cmds.delete(DUP1[0])
    
    cmds.parent('{}Shape2'.format(o), o, add=1, s=1)
    cmds.delete(DUP2[0])
    
def shapeChange6_CL(o, shapeColor, shapeBold):
    shapeList = cmds.listRelatives(o, s=1)
    
    for i in shapeList:
        cmds.delete(i)
        
    CTL = cmds.circle(n='{}TEMP'.format(o), normalX=0, normalY=0, normalZ=0)
    cmds.rename(cmds.listRelatives(CTL[0], s=1), '{}Shape'.format(o))
    try:
        cmds.setAttr('{}Shape.overrideEnabled'.format(o), 1)
        cmds.setAttr('{}Shape.overrideColor'.format(o), shapeColor)
        cmds.setAttr('{}Shape.lineWidth'.format(o), shapeBold)
    except:
        pass
    
    cmds.setAttr('{}.sections'.format(CTL[1]), 16)
    cmds.setAttr('{}.degree'.format(CTL[1]), 1)
    cmds.addAttr(CTL[0], ln='radius', at='double', k=0, dv=1)
    cmds.setAttr('{}.radius'.format(CTL[0]), l=1)
    cmds.addAttr(CTL[0], ln='shapeType', dt='string')
    cmds.setAttr('{}.shapeType'.format(CTL[0]), 'cube', type='string', l=1)
    
    cmds.select('{}.cv[0]'.format(CTL[0]))
    cmds.move(-2, -2, -2)
    cmds.select('{}.cv[1]'.format(CTL[0]))
    cmds.move(-2, -2, 2)
    cmds.select('{}.cv[2]'.format(CTL[0]))
    cmds.move(2, -2, 2)
    cmds.select('{}.cv[3]'.format(CTL[0]))
    cmds.move(2, -2, -2)
    cmds.select('{}.cv[4]'.format(CTL[0]))
    cmds.move(-2, -2, -2)
    cmds.select('{}.cv[5]'.format(CTL[0]))
    cmds.move(-2, 2, -2)
    cmds.select('{}.cv[6]'.format(CTL[0]))
    cmds.move(-2, 2, 2)
    cmds.select('{}.cv[7]'.format(CTL[0]))
    cmds.move(-2, -2, 2)
    cmds.select('{}.cv[8]'.format(CTL[0]))
    cmds.move(-2, 2, 2)
    cmds.select('{}.cv[9]'.format(CTL[0]))
    cmds.move(2, 2, 2)
    cmds.select('{}.cv[10]'.format(CTL[0]))
    cmds.move(2, -2, 2)
    cmds.select('{}.cv[11]'.format(CTL[0]))
    cmds.move(2, 2, 2)
    cmds.select('{}.cv[12]'.format(CTL[0]))
    cmds.move(2, 2, -2)
    cmds.select('{}.cv[13]'.format(CTL[0]))
    cmds.move(2, -2, -2)
    cmds.select('{}.cv[14]'.format(CTL[0]))
    cmds.move(2, 2, -2)
    cmds.select('{}.cv[15]'.format(CTL[0]))
    cmds.move(-2, 2, -2)
    cmds.select('{}.cv[16]'.format(CTL[0]))
    cmds.move(-2, -2, -2)
    
    cmds.delete(CTL[0], ch=1)
    cmds.parent('{}Shape'.format(o), o, add=1, s=1)
    cmds.delete(CTL[0])
    cmds.select(o)
    
def shapeChange7_CL(o, shapeColor, shapeBold):
    shapeList = cmds.listRelatives(o, s=1)
    
    if shapeList != None:
        for i in shapeList:
            cmds.delete(i)
        
    CTL = cmds.circle(n='{}TEMP'.format(o), normalX=0, normalY=0, normalZ=0)
    cmds.rename(cmds.listRelatives(CTL[0], s=1), '{}Shape'.format(o))
    try:
        cmds.setAttr('{}Shape.overrideEnabled'.format(o), 1)
        cmds.setAttr('{}Shape.overrideColor'.format(o), shapeColor)
        cmds.setAttr('{}Shape.lineWidth'.format(o), shapeBold)
    except:
        pass
    
    cmds.setAttr('{}.sections'.format(CTL[1]), 12)
    cmds.setAttr('{}.degree'.format(CTL[1]), 1)
    cmds.addAttr(CTL[0], ln='radius', at='double', k=0, dv=1)
    cmds.setAttr('{}.radius'.format(CTL[0]), l=1)
    cmds.addAttr(CTL[0], ln='shapeType', dt='string')
    cmds.setAttr('{}.shapeType'.format(CTL[0]), 'square', type='string', l=1)
    cmds.select('{}.cv[0]'.format(CTL[0]))
    cmds.move(1.8, 0, -2)
    cmds.select('{}.cv[1]'.format(CTL[0]))
    cmds.move(1.95, 0, -1.95)
    cmds.select('{}.cv[2]'.format(CTL[0]))
    cmds.move(2, 0, -1.8)
    cmds.select('{}.cv[3]'.format(CTL[0]))
    cmds.move(2, 0, 1.8)
    cmds.select('{}.cv[4]'.format(CTL[0]))
    cmds.move(1.95, 0, 1.95)
    cmds.select('{}.cv[5]'.format(CTL[0]))
    cmds.move(1.8, 0, 2)
    cmds.select('{}.cv[6]'.format(CTL[0]))
    cmds.move(-1.8, 0, 2)
    cmds.select('{}.cv[7]'.format(CTL[0]))
    cmds.move(-1.95, 0, 1.95)
    cmds.select('{}.cv[8]'.format(CTL[0]))
    cmds.move(-2, 0, 1.8)
    cmds.select('{}.cv[9]'.format(CTL[0]))
    cmds.move(-2, 0, -1.8)
    cmds.select('{}.cv[10]'.format(CTL[0]))
    cmds.move(-1.95, 0, -1.95)
    cmds.select('{}.cv[11]'.format(CTL[0]))
    cmds.move(-1.8, 0, -2)
    cmds.select('{}.cv[12]'.format(CTL[0]))
    cmds.move(1.8, 0, -2)
    
    cmds.delete(CTL[0], ch=1)
    cmds.parent('{}Shape'.format(o), o, add=1, s=1)
    cmds.delete(CTL[0])
    cmds.select(o)

def shapeChange8_CL(o, shapeColor, shapeBold):
    shapeList = cmds.listRelatives(o, s=1)
    
    if shapeList != None:
        for i in shapeList:
            cmds.delete(i)
        
    CTL = cmds.circle(n='{}TEMP'.format(o), normalX=0, normalY=0, normalZ=0)
    cmds.rename(cmds.listRelatives(CTL[0], s=1), '{}Shape'.format(o))
    try:
        cmds.setAttr('{}Shape.overrideEnabled'.format(o), 1)
        cmds.setAttr('{}Shape.overrideColor'.format(o), shapeColor)
        cmds.setAttr('{}Shape.lineWidth'.format(o), shapeBold)
    except:
        pass
    
    cmds.setAttr('{}.sections'.format(CTL[1]), 8)
    cmds.setAttr('{}.degree'.format(CTL[1]), 3)
    cmds.addAttr(CTL[0], ln='radius', at='double', k=0, dv=1)
    cmds.setAttr('{}.radius'.format(CTL[0]), l=1)
    cmds.addAttr(CTL[0], ln='shapeType', dt='string')
    cmds.setAttr('{}.shapeType'.format(CTL[0]), 'circle', type='string', l=1)
    
    cmds.select('{}.cv[0]'.format(CTL[0]))
    cmds.move(0, 0, 2)
    cmds.select('{}.cv[1]'.format(CTL[0]))
    cmds.move(1.4, 0, 1.4)
    cmds.select('{}.cv[2]'.format(CTL[0]))
    cmds.move(2, 0, 0)
    cmds.select('{}.cv[3]'.format(CTL[0]))
    cmds.move(1.4, 0, -1.4)
    cmds.select('{}.cv[4]'.format(CTL[0]))
    cmds.move(0, 0, -2)
    cmds.select('{}.cv[5]'.format(CTL[0]))
    cmds.move(-1.4, 0, -1.4)
    cmds.select('{}.cv[6]'.format(CTL[0]))
    cmds.move(-2, 0, 0)
    cmds.select('{}.cv[7]'.format(CTL[0]))
    cmds.move(-1.4, 0, 1.4)
    
    cmds.delete(CTL[0], ch=1)
    cmds.parent('{}Shape'.format(o), o, add=1, s=1)
    cmds.delete(CTL[0])
    cmds.select(o)
    
def shapeChange9_CL(o, shapeColor, shapeBold):
    shapeList = cmds.listRelatives(o, s=1)
    
    for i in shapeList:
        cmds.delete(i)
        
    CTL = cmds.circle(n='{}TEMP'.format(o), normalX=0, normalY=0, normalZ=0)
    cmds.rename(cmds.listRelatives(CTL[0], s=1), '{}Shape'.format(o))
    try:
        cmds.setAttr('{}Shape.overrideEnabled'.format(o), 1)
        cmds.setAttr('{}Shape.overrideColor'.format(o), shapeColor)
        cmds.setAttr('{}Shape.lineWidth'.format(o), shapeBold)
    except:
        pass
    
    cmds.setAttr('{}.sections'.format(CTL[1]), 4)
    cmds.setAttr('{}.degree'.format(CTL[1]), 1)
    cmds.addAttr(CTL[0], ln='radius', at='double', k=0, dv=1)
    cmds.setAttr('{}.radius'.format(CTL[0]), l=1)
    cmds.addAttr(CTL[0], ln='shapeType', dt='string')
    cmds.setAttr('{}.shapeType'.format(CTL[0]), 'wheel', type='string', l=1)
    
    cmds.select('{}.cv[0]'.format(CTL[0]))
    cmds.move(2.15, 0, 0.3)
    cmds.select('{}.cv[1]'.format(CTL[0]))
    cmds.move(2.15, 0, -0.3)
    cmds.select('{}.cv[2]'.format(CTL[0]))
    cmds.move(1.86, 0, -0.3)
    cmds.select('{}.cv[3]'.format(CTL[0]))
    cmds.move(1.85, 0, 0.3)
    cmds.select('{}.cv[4]'.format(CTL[0]))
    cmds.move(2.15, 0, 0.3)
    
    cmds.delete(CTL[0], ch=1)
    cmds.parent('{}Shape'.format(o), o, add=1, s=1)
    
    for i in range(1, 12):
        DUP = cmds.duplicate(CTL[0], n='{}{}'.format(o, i), rc=True)
        cmds.rename(cmds.listRelatives(DUP[0], s=1), '{}Shape{}'.format(o, i))
        cmds.select('{}.cv[0:4]'.format(DUP[0]))
        cmds.rotate(0, 0, 30*i)
        
        cmds.select(DUP[0])
        cmds.parent('{}Shape{}'.format(o, i), o, add=1, s=1)
        cmds.delete(DUP[0])
    
    cmds.delete(CTL[0])
    cmds.select(o)
            
def shapeChange10_CL(o, shapeColor, shapeBold):
    shapeList = cmds.listRelatives(o, s=1)
    
    for i in shapeList:
        cmds.delete(i)
        
    CTL = cmds.circle(n='{}TEMP'.format(o), normalX=0, normalY=0, normalZ=0)
    cmds.rename(cmds.listRelatives(CTL[0], s=1), '{}Shape'.format(o))
    try:
        cmds.setAttr('{}Shape.overrideEnabled'.format(o), 1)
        cmds.setAttr('{}Shape.overrideColor'.format(o), shapeColor)
        cmds.setAttr('{}Shape.lineWidth'.format(o), shapeBold)
    except:
        pass
    
    cmds.setAttr('{}.sections'.format(CTL[1]), 8)
    cmds.setAttr('{}.degree'.format(CTL[1]), 3)
    cmds.addAttr(CTL[0], ln='radius', at='double', k=0, dv=1)
    cmds.setAttr('{}.radius'.format(CTL[0]), l=1)
    cmds.addAttr(CTL[0], ln='shapeType', dt='string')
    cmds.setAttr('{}.shapeType'.format(CTL[0]), 'arrowedSphere', type='string', l=1)
    
    cmds.select('{}.cv[0]'.format(CTL[0]))
    cmds.move(0, 0, 2)
    cmds.select('{}.cv[1]'.format(CTL[0]))
    cmds.move(1.4, 0, 1.4)
    cmds.select('{}.cv[2]'.format(CTL[0]))
    cmds.move(2, 0, 0)
    cmds.select('{}.cv[3]'.format(CTL[0]))
    cmds.move(1.4, 0, -1.4)
    cmds.select('{}.cv[4]'.format(CTL[0]))
    cmds.move(0, 0, -2)
    cmds.select('{}.cv[5]'.format(CTL[0]))
    cmds.move(-1.4, 0, -1.4)
    cmds.select('{}.cv[6]'.format(CTL[0]))
    cmds.move(-2, 0, 0)
    cmds.select('{}.cv[7]'.format(CTL[0]))
    cmds.move(-1.4, 0, 1.4)
    
    DUP1 = cmds.duplicate(CTL[0], n='{}1'.format(o), rc=True)
    cmds.rename(cmds.listRelatives(DUP1[0], s=1), '{}Shape1'.format(o))
    cmds.select('{}.cv[0:7]'.format(DUP1[0]))
    cmds.rotate(90, 0, 0)
    
    DUP2 = cmds.duplicate(CTL[0], n='{}2'.format(o), rc=True)
    cmds.rename(cmds.listRelatives(DUP2[0], s=1), '{}Shape2'.format(o))
    cmds.select('{}.cv[0:7]'.format(DUP2[0]))
    cmds.rotate(0, 90, 0)
    
    cmds.delete(CTL[0], ch=1)
    cmds.parent('{}Shape'.format(o), o, add=1, s=1)
    cmds.delete(CTL[0])
    cmds.select(o)
    
    cmds.parent('{}Shape1'.format(o), o, add=1, s=1)
    cmds.delete(DUP1[0])
    
    cmds.parent('{}Shape2'.format(o), o, add=1, s=1)
    cmds.delete(DUP2[0])
    
    CTL1 = cmds.circle(n='{}4'.format(o), normalX=0, normalY=0, normalZ=0)
    cmds.rename(cmds.listRelatives(CTL1[0], s=1), '{}Shape4'.format(o))
    cmds.setAttr('{}Shape4.overrideEnabled'.format(o), 1)
    cmds.setAttr('{}Shape4.overrideColor'.format(o), shapeColor)
    cmds.setAttr('{}Shape4.lineWidth'.format(o), shapeBold)

    cmds.setAttr('{}.sections'.format(CTL1[1]), 9)
    cmds.setAttr('{}.degree'.format(CTL1[1]), 1)
    cmds.addAttr(CTL1[0], ln='radius', at='double', k=0, dv=1)
    cmds.setAttr('{}.radius'.format(CTL1[0]), l=1)
    cmds.addAttr(CTL1[0], ln='shapeType', dt='string')
    cmds.setAttr('{}.shapeType'.format(CTL1[0]), 'arrowedSquare', type='string', l=1)
    
    cmds.select('{}.cv[0]'.format(CTL1[0]))
    cmds.move(2.2, 0, -0.7)
    cmds.select('{}.cv[1]'.format(CTL1[0]))
    cmds.move(2.8, 0, 0)
    cmds.select('{}.cv[2]'.format(CTL1[0]))
    cmds.move(2.2, 0, 0.7)
    cmds.select('{}.cv[3]'.format(CTL1[0]))
    cmds.move(2.2, -0.7, 0)
    cmds.select('{}.cv[4]'.format(CTL1[0]))
    cmds.move(2.8, 0, 0)
    cmds.select('{}.cv[5]'.format(CTL1[0]))
    cmds.move(2.2, 0.7, 0)
    cmds.select('{}.cv[6]'.format(CTL1[0]))
    cmds.move(2.2, 0, -0.7)
    cmds.select('{}.cv[7]'.format(CTL1[0]))
    cmds.move(2.2, -0.7, 0)
    cmds.select('{}.cv[8]'.format(CTL1[0]))
    cmds.move(2.2, 0, 0.7)
    cmds.select('{}.cv[9]'.format(CTL1[0]))
    cmds.move(2.2, 0.7, 0)
    
    cmds.delete(CTL1[0], ch=1)
    cmds.parent('{}Shape4'.format(o), o, add=1, s=1)
    cmds.delete(CTL1[0])
    cmds.select(o)
    
    for o in cmds.listRelatives(o, s=1):
        cmds.select(o+'.cv[*]')
        cmds.rotate(0, 0, 270)
    cmds.select(o)
    
def shapeChange11_CL(o, shapeColor, shapeBold):
    shapeList = cmds.listRelatives(o, s=1)
    
    for i in shapeList:
        cmds.delete(i)
        
    CTL = cmds.circle(n='{}TEMP'.format(o), normalX=0, normalY=0, normalZ=0)
    cmds.rename(cmds.listRelatives(CTL[0], s=1), '{}Shape'.format(o))
    try:
        cmds.setAttr('{}Shape.overrideEnabled'.format(o), 1)
        cmds.setAttr('{}Shape.overrideColor'.format(o), shapeColor)
        cmds.setAttr('{}Shape.lineWidth'.format(o), shapeBold)
    except:
        pass
    
    cmds.setAttr('{}.sections'.format(CTL[1]), 12)
    cmds.setAttr('{}.degree'.format(CTL[1]), 1)
    cmds.addAttr(CTL[0], ln='radius', at='double', k=0, dv=1)
    cmds.setAttr('{}.radius'.format(CTL[0]), l=1)
    cmds.addAttr(CTL[0], ln='shapeType', dt='string')
    cmds.setAttr('{}.shapeType'.format(CTL[0]), 'arrowedSquare', type='string', l=1)
    
    cmds.select('{}.cv[0]'.format(CTL[0]))
    cmds.move(1.8, 0, -2)
    cmds.select('{}.cv[1]'.format(CTL[0]))
    cmds.move(1.95, 0, -1.95)
    cmds.select('{}.cv[2]'.format(CTL[0]))
    cmds.move(2, 0, -1.8)
    cmds.select('{}.cv[3]'.format(CTL[0]))
    cmds.move(2, 0, 1.8)
    cmds.select('{}.cv[4]'.format(CTL[0]))
    cmds.move(1.95, 0, 1.95)
    cmds.select('{}.cv[5]'.format(CTL[0]))
    cmds.move(1.8, 0, 2)
    cmds.select('{}.cv[6]'.format(CTL[0]))
    cmds.move(-1.8, 0, 2)
    cmds.select('{}.cv[7]'.format(CTL[0]))
    cmds.move(-1.95, 0, 1.95)
    cmds.select('{}.cv[8]'.format(CTL[0]))
    cmds.move(-2, 0, 1.8)
    cmds.select('{}.cv[9]'.format(CTL[0]))
    cmds.move(-2, 0, -1.8)
    cmds.select('{}.cv[10]'.format(CTL[0]))
    cmds.move(-1.95, 0, -1.95)
    cmds.select('{}.cv[11]'.format(CTL[0]))
    cmds.move(-1.8, 0, -2)
    cmds.select('{}.cv[12]'.format(CTL[0]))
    cmds.move(1.8, 0, -2)
    
    cmds.delete(CTL[0], ch=1)
    cmds.parent('{}Shape'.format(o), o, add=1, s=1)
    cmds.delete(CTL[0])
    cmds.select(o)
    
    CTL1 = cmds.circle(n='{}1'.format(o), normalX=0, normalY=0, normalZ=0)
    cmds.rename(cmds.listRelatives(CTL1[0], s=1), '{}Shape1'.format(o))
    cmds.setAttr('{}Shape1.overrideEnabled'.format(o), 1)
    cmds.setAttr('{}Shape1.overrideColor'.format(o), shapeColor)
    cmds.setAttr('{}Shape1.lineWidth'.format(o), shapeBold)
    
    cmds.setAttr('{}.sections'.format(CTL1[1]), 3)
    cmds.setAttr('{}.degree'.format(CTL1[1]), 1)
    cmds.addAttr(CTL1[0], ln='radius', at='double', k=0, dv=1)
    cmds.setAttr('{}.radius'.format(CTL1[0]), l=1)
    cmds.addAttr(CTL1[0], ln='shapeType', dt='string')
    cmds.setAttr('{}.shapeType'.format(CTL1[0]), 'arrowedSquare', type='string', l=1)
    
    cmds.select('{}.cv[0]'.format(CTL1[0]))
    cmds.move(2.8, 0, 0)
    cmds.select('{}.cv[1]'.format(CTL1[0]))
    cmds.move(2.2, 0, -0.7)
    cmds.select('{}.cv[2]'.format(CTL1[0]))
    cmds.move(2.2, 0, 0.7)
    cmds.select('{}.cv[3]'.format(CTL1[0]))
    cmds.move(2.8, 0, 0)
    
    cmds.delete(CTL1[0], ch=1)
    cmds.parent('{}Shape1'.format(o), o, add=1, s=1)
    cmds.delete(CTL1[0])
    cmds.select(o)
    
    for o in cmds.listRelatives(o, s=1):
        cmds.select(o+'.cv[*]')
        cmds.rotate(0, 0, 270)
    cmds.select(o)
    
def shapeChange12_CL(o, shapeColor, shapeBold):
    shapeList = cmds.listRelatives(o, s=1)
    
    if shapeList != None:
        for i in shapeList:
            cmds.delete(i)
        
    CTL = cmds.circle(n='{}TEMP'.format(o), normalX=0, normalY=0, normalZ=0)
    cmds.rename(cmds.listRelatives(CTL[0], s=1), '{}Shape'.format(o))
    try:
        cmds.setAttr('{}Shape.overrideEnabled'.format(o), 1)
        cmds.setAttr('{}Shape.overrideColor'.format(o), shapeColor)
        cmds.setAttr('{}Shape.lineWidth'.format(o), shapeBold)
    except:
        pass
    
    cmds.setAttr('{}.sections'.format(CTL[1]), 8)
    cmds.setAttr('{}.degree'.format(CTL[1]), 3)
    cmds.addAttr(CTL[0], ln='radius', at='double', k=0, dv=1)
    cmds.setAttr('{}.radius'.format(CTL[0]), l=1)
    cmds.addAttr(CTL[0], ln='shapeType', dt='string')
    cmds.setAttr('{}.shapeType'.format(CTL[0]), 'arrowedCircle', type='string', l=1)
    
    cmds.select('{}.cv[0]'.format(CTL[0]))
    cmds.move(0, 0, 2)
    cmds.select('{}.cv[1]'.format(CTL[0]))
    cmds.move(1.4, 0, 1.4)
    cmds.select('{}.cv[2]'.format(CTL[0]))
    cmds.move(2, 0, 0)
    cmds.select('{}.cv[3]'.format(CTL[0]))
    cmds.move(1.4, 0, -1.4)
    cmds.select('{}.cv[4]'.format(CTL[0]))
    cmds.move(0, 0, -2)
    cmds.select('{}.cv[5]'.format(CTL[0]))
    cmds.move(-1.4, 0, -1.4)
    cmds.select('{}.cv[6]'.format(CTL[0]))
    cmds.move(-2, 0, 0)
    cmds.select('{}.cv[7]'.format(CTL[0]))
    cmds.move(-1.4, 0, 1.4)
    
    cmds.delete(CTL[0], ch=1)
    cmds.parent('{}Shape'.format(o), o, add=1, s=1)
    cmds.delete(CTL[0])
    cmds.select(o)
    
    CTL1 = cmds.circle(n='{}1'.format(o), normalX=0, normalY=0, normalZ=0)
    cmds.rename(cmds.listRelatives(CTL1[0], s=1), '{}Shape1'.format(o))
    cmds.setAttr('{}Shape1.overrideEnabled'.format(o), 1)
    cmds.setAttr('{}Shape1.overrideColor'.format(o), shapeColor)
    cmds.setAttr('{}Shape1.lineWidth'.format(o), shapeBold)
    
    cmds.setAttr('{}.sections'.format(CTL1[1]), 3)
    cmds.setAttr('{}.degree'.format(CTL1[1]), 1)
    cmds.addAttr(CTL1[0], ln='radius', at='double', k=0, dv=1)
    cmds.setAttr('{}.radius'.format(CTL1[0]), l=1)
    cmds.addAttr(CTL1[0], ln='shapeType', dt='string')
    cmds.setAttr('{}.shapeType'.format(CTL1[0]), 'arrowedCircle', type='string', l=1)
    
    cmds.select('{}.cv[0]'.format(CTL1[0]))
    cmds.move(2.5, 0, 0)
    cmds.select('{}.cv[1]'.format(CTL1[0]))
    cmds.move(2, 0, -0.5)
    cmds.select('{}.cv[2]'.format(CTL1[0]))
    cmds.move(2, 0, 0.5)
    cmds.select('{}.cv[3]'.format(CTL1[0]))
    cmds.move(2.5, 0, 0)
    
    cmds.delete(CTL1[0], ch=1)
    cmds.parent('{}Shape1'.format(o), o, add=1, s=1)
    cmds.delete(CTL1[0])
    cmds.select(o)
    
    for o in cmds.listRelatives(o, s=1):
        cmds.select(o+'.cv[*]')
        cmds.rotate(0, 0, 270)
    cmds.select(o)
    
def shapeChange13_CL(o, shapeColor, shapeBold):
    shapeList = cmds.listRelatives(o, s=1)
    
    for i in shapeList:
        cmds.delete(i)
        
    CTL = cmds.circle(n='{}TEMP'.format(o), normalX=0, normalY=0, normalZ=0)
    cmds.rename(cmds.listRelatives(CTL[0], s=1), '{}Shape'.format(o))
    try:
        cmds.setAttr('{}Shape.overrideEnabled'.format(o), 1)
        cmds.setAttr('{}Shape.overrideColor'.format(o), shapeColor)
        cmds.setAttr('{}Shape.lineWidth'.format(o), shapeBold)
    except:
        pass
    
    cmds.setAttr('{}.sections'.format(CTL[1]), 4)
    cmds.setAttr('{}.degree'.format(CTL[1]), 1)
    cmds.addAttr(CTL[0], ln='radius', at='double', k=0, dv=1)
    cmds.setAttr('{}.radius'.format(CTL[0]), l=1)
    cmds.addAttr(CTL[0], ln='shapeType', dt='string')
    cmds.setAttr('{}.shapeType'.format(CTL[0]), 'arrowedWheel', type='string', l=1)
    
    cmds.select('{}.cv[0]'.format(CTL[0]))
    cmds.move(2.15, 0, 0.3)
    cmds.select('{}.cv[1]'.format(CTL[0]))
    cmds.move(2.15, 0, -0.3)
    cmds.select('{}.cv[2]'.format(CTL[0]))
    cmds.move(1.86, 0, -0.3)
    cmds.select('{}.cv[3]'.format(CTL[0]))
    cmds.move(1.85, 0, 0.3)
    cmds.select('{}.cv[4]'.format(CTL[0]))
    cmds.move(2.15, 0, 0.3)
    
    cmds.delete(CTL[0], ch=1)
    cmds.parent('{}Shape'.format(o), o, add=1, s=1)
    
    for i in range(1, 12):
        DUP = cmds.duplicate(CTL[0], n='{}{}'.format(o, i), rc=True)
        cmds.rename(cmds.listRelatives(DUP[0], s=1), '{}Shape{}'.format(o, i))
        cmds.select('{}.cv[0:4]'.format(DUP[0]))
        cmds.rotate(0, 0, 30*i)
        
        cmds.select(DUP[0])
        cmds.parent('{}Shape{}'.format(o, i), o, add=1, s=1)
        cmds.delete(DUP[0])
    
    cmds.delete(CTL[0])
    cmds.select(o)
    
    CTL1 = cmds.circle(n='{}12'.format(o), normalX=0, normalY=0, normalZ=0)
    cmds.rename(cmds.listRelatives(CTL1[0], s=1), '{}Shape12'.format(o))
    cmds.setAttr('{}Shape12.overrideEnabled'.format(o), 1)
    cmds.setAttr('{}Shape12.overrideColor'.format(o), shapeColor)
    cmds.setAttr('{}Shape12.lineWidth'.format(o), shapeBold)
    
    cmds.setAttr('{}.sections'.format(CTL1[1]), 3)
    cmds.setAttr('{}.degree'.format(CTL1[1]), 1)
    cmds.addAttr(CTL1[0], ln='radius', at='double', k=0, dv=1)
    cmds.setAttr('{}.radius'.format(CTL1[0]), l=1)
    cmds.addAttr(CTL1[0], ln='shapeType', dt='string')
    cmds.setAttr('{}.shapeType'.format(CTL1[0]), 'arrowedCircle', type='string', l=1)
    
    cmds.select('{}.cv[0]'.format(CTL1[0]))
    cmds.move(2.6, 0, 0)
    cmds.select('{}.cv[1]'.format(CTL1[0]))
    cmds.move(2.3, 0, -0.3)
    cmds.select('{}.cv[2]'.format(CTL1[0]))
    cmds.move(2.3, 0, 0.3)
    cmds.select('{}.cv[3]'.format(CTL1[0]))
    cmds.move(2.6, 0, 0)
    
    cmds.delete(CTL1[0], ch=1)
    cmds.parent('{}Shape12'.format(o), o, add=1, s=1)
    cmds.delete(CTL1[0])
    cmds.select(o)
    
    for o in cmds.listRelatives(o, s=1):
        cmds.select(o+'.cv[*]')
        cmds.rotate(0, 0, 270)
    cmds.select(o)
    
def shapeChange14_CL(o, shapeColor, shapeBold):
    shapeList = cmds.listRelatives(o, s=1)
    
    for i in shapeList:
        cmds.delete(i)
        
    CTL = cmds.circle(n='{}TEMP'.format(o), normalX=0, normalY=0, normalZ=0)
    cmds.rename(cmds.listRelatives(CTL[0], s=1), '{}Shape'.format(o))
    try:
        cmds.setAttr('{}Shape.overrideEnabled'.format(o), 1)
        cmds.setAttr('{}Shape.overrideColor'.format(o), shapeColor)
        cmds.setAttr('{}Shape.lineWidth'.format(o), shapeBold)
    except:
        pass
    
    cmds.setAttr('{}.sections'.format(CTL[1]), 12)
    cmds.setAttr('{}.degree'.format(CTL[1]), 3)
    cmds.addAttr(CTL[0], ln='radius', at='double', k=0, dv=1)
    cmds.setAttr('{}.radius'.format(CTL[0]), l=1)
    cmds.addAttr(CTL[0], ln='shapeType', dt='string')
    cmds.setAttr('{}.shapeType'.format(CTL[0]), 'foot', type='string', l=1)
    
    cmds.select('{}.cv[0]'.format(CTL[0]))
    cmds.move(2.175, 0, 0)
    cmds.select('{}.cv[1]'.format(CTL[0]))
    cmds.move(1.65, 0, -0.8)
    cmds.select('{}.cv[2]'.format(CTL[0]))
    cmds.move(0.7, 0, -1)
    cmds.select('{}.cv[3]'.format(CTL[0]))
    cmds.move(-0.2, 0.5, -0.4)
    cmds.select('{}.cv[4]'.format(CTL[0]))
    cmds.move(-0.6, 0, -0.6)
    cmds.select('{}.cv[5]'.format(CTL[0]))
    cmds.move(-1.6, 0, -0.9)
    cmds.select('{}.cv[6]'.format(CTL[0]))
    cmds.move(-2.2, 0, 0)
    cmds.select('{}.cv[7]'.format(CTL[0]))
    cmds.move(-1.6, 0, 0.9)
    cmds.select('{}.cv[8]'.format(CTL[0]))
    cmds.move(-0.6, 0, 0.6)
    cmds.select('{}.cv[9]'.format(CTL[0]))
    cmds.move(-0.2, 0.5, 0.4)
    cmds.select('{}.cv[10]'.format(CTL[0]))
    cmds.move(0.7, 0, 1)
    cmds.select('{}.cv[11]'.format(CTL[0]))
    cmds.move(1.65, 0, 0.8)
    
    cmds.delete(CTL[0], ch=1)
    cmds.parent('{}Shape'.format(o), o, add=1, s=1)
    cmds.delete(CTL[0])
    cmds.select(o)
    
    CTL1 = cmds.circle(n='{}1'.format(o), normalX=0, normalY=0, normalZ=0)
    cmds.rename(cmds.listRelatives(CTL1[0], s=1), '{}Shape1'.format(o))
    cmds.setAttr('{}Shape1.overrideEnabled'.format(o), 1)
    cmds.setAttr('{}Shape1.overrideColor'.format(o), shapeColor)
    cmds.setAttr('{}Shape1.lineWidth'.format(o), shapeBold)
    
    cmds.setAttr('{}.sections'.format(CTL1[1]), 3)
    cmds.setAttr('{}.degree'.format(CTL1[1]), 3)
    cmds.addAttr(CTL1[0], ln='radius', at='double', k=0, dv=1)
    cmds.setAttr('{}.radius'.format(CTL1[0]), l=1)
    cmds.addAttr(CTL1[0], ln='shapeType', dt='string')
    cmds.setAttr('{}.shapeType'.format(CTL1[0]), 'arrowedCircle', type='string', l=1)
    
    cmds.select('{}.cv[0]'.format(CTL1[0]))
    cmds.move(-2, -0.165, 0)
    cmds.select('{}.cv[1]'.format(CTL1[0]))
    cmds.move(-2.5, 0.335, 0)
    cmds.select('{}.cv[2]'.format(CTL1[0]))
    cmds.move(-2, 0.835, 0)
    cmds.select('{}.cv[3]'.format(CTL1[0]))
    cmds.move(-1.5, 0.335, 0)
    
    cmds.delete(CTL1[0], ch=1)
    cmds.parent('{}Shape1'.format(o), o, add=1, s=1)
    cmds.delete(CTL1[0])
    cmds.select(o)
    
    for o in cmds.listRelatives(o, s=1):
        cmds.select(o+'.cv[*]')
        cmds.rotate(0, 0, 270)
    cmds.select(o)
    
def shapeChange15_CL(o, shapeColor, shapeBold):
    shapeList = cmds.listRelatives(o, s=1)
    
    for i in shapeList:
        cmds.delete(i)
        
    CTL = cmds.circle(n='{}TEMP'.format(o), normalX=0, normalY=0, normalZ=0)
    cmds.rename(cmds.listRelatives(CTL[0], s=1), '{}Shape'.format(o))
    try:
        cmds.setAttr('{}Shape.overrideEnabled'.format(o), 1)
        cmds.setAttr('{}Shape.overrideColor'.format(o), shapeColor)
        cmds.setAttr('{}Shape.lineWidth'.format(o), shapeBold)
    except:
        pass
    
    cmds.setAttr('{}.sections'.format(CTL[1]), 8)
    cmds.setAttr('{}.degree'.format(CTL[1]), 3)
    cmds.addAttr(CTL[0], ln='radius', at='double', k=0, dv=1)
    cmds.setAttr('{}.radius'.format(CTL[0]), l=1)
    cmds.addAttr(CTL[0], ln='shapeType', dt='string')
    cmds.setAttr('{}.shapeType'.format(CTL[0]), 'googles', type='string', l=1)
    
    cmds.select('{}.cv[0]'.format(CTL[0]))
    cmds.move(0, 0, 0.25)
    cmds.select('{}.cv[1]'.format(CTL[0]))
    cmds.move(1, 0, 1.45)
    cmds.select('{}.cv[2]'.format(CTL[0]))
    cmds.move(2.5, 0, 0)
    cmds.select('{}.cv[3]'.format(CTL[0]))
    cmds.move(1, 0, -1.45)
    cmds.select('{}.cv[4]'.format(CTL[0]))
    cmds.move(0, 0, -0.25)
    cmds.select('{}.cv[5]'.format(CTL[0]))
    cmds.move(-1, 0, -1.45)
    cmds.select('{}.cv[6]'.format(CTL[0]))
    cmds.move(-2.5, 0, 0)
    cmds.select('{}.cv[7]'.format(CTL[0]))
    cmds.move(-1, 0, 1.45)
    
    cmds.delete(CTL[0], ch=1)
    cmds.parent('{}Shape'.format(o), o, add=1, s=1)
    cmds.delete(CTL[0])
    cmds.select(o)
    
    for o in cmds.listRelatives(o, s=1):
        cmds.select(o+'.cv[*]')
        cmds.rotate(0, 270, 0)
    cmds.select(o)
    
def shapeChange16_CL(o, shapeColor, shapeBold):
    shapeList = cmds.listRelatives(o, s=1)
    
    for i in shapeList:
        cmds.delete(i)
        
    CTL = cmds.circle(n='{}TEMP'.format(o), normalX=0, normalY=0, normalZ=0)
    cmds.rename(cmds.listRelatives(CTL[0], s=1), '{}Shape'.format(o))
    try:
        cmds.setAttr('{}Shape.overrideEnabled'.format(o), 1)
        cmds.setAttr('{}Shape.overrideColor'.format(o), shapeColor)
        cmds.setAttr('{}Shape.lineWidth'.format(o), shapeBold)
    except:
        pass
    
    cmds.setAttr('{}.sections'.format(CTL[1]), 8)
    cmds.setAttr('{}.degree'.format(CTL[1]), 3)
    cmds.addAttr(CTL[0], ln='radius', at='double', k=0, dv=1)
    cmds.setAttr('{}.radius'.format(CTL[0]), l=1)
    cmds.addAttr(CTL[0], ln='shapeType', dt='string')
    cmds.setAttr('{}.shapeType'.format(CTL[0]), 'neck', type='string', l=1)
    
    cmds.select('{}.cv[0]'.format(CTL[0]))
    cmds.move(0, 0, 0.25)
    cmds.select('{}.cv[1]'.format(CTL[0]))
    cmds.move(1.9, 0, 1)
    cmds.select('{}.cv[2]'.format(CTL[0]))
    cmds.move(2, 0, 0)
    cmds.select('{}.cv[3]'.format(CTL[0]))
    cmds.move(1.9, 0, -1)
    cmds.select('{}.cv[4]'.format(CTL[0]))
    cmds.move(0, 0, -0.25)
    cmds.select('{}.cv[5]'.format(CTL[0]))
    cmds.move(-1.9, 0, -1)
    cmds.select('{}.cv[6]'.format(CTL[0]))
    cmds.move(-2, 0, 0)
    cmds.select('{}.cv[7]'.format(CTL[0]))
    cmds.move(-1.9, 0, 1)
    
    cmds.delete(CTL[0], ch=1)
    cmds.parent('{}Shape'.format(o), o, add=1, s=1)
    cmds.delete(CTL[0])
    cmds.select(o)
    
    CTL1 = cmds.circle(n='{}1'.format(o), normalX=0, normalY=0, normalZ=0)
    cmds.rename(cmds.listRelatives(CTL1[0], s=1), '{}Shape1'.format(o))
    cmds.setAttr('{}Shape1.overrideEnabled'.format(o), 1)
    cmds.setAttr('{}Shape1.overrideColor'.format(o), shapeColor)
    cmds.setAttr('{}Shape1.lineWidth'.format(o), shapeBold)
    
    cmds.setAttr('{}.sections'.format(CTL1[1]), 3)
    cmds.setAttr('{}.degree'.format(CTL1[1]), 1)
    cmds.addAttr(CTL1[0], ln='radius', at='double', k=0, dv=1)
    cmds.setAttr('{}.radius'.format(CTL1[0]), l=1)
    cmds.addAttr(CTL1[0], ln='shapeType', dt='string')
    cmds.setAttr('{}.shapeType'.format(CTL1[0]), 'neck', type='string', l=1)
    
    cmds.select('{}.cv[0]'.format(CTL1[0]))
    cmds.move(2.7, 0, 0)
    cmds.select('{}.cv[1]'.format(CTL1[0]))
    cmds.move(2.1, 0, -0.3)
    cmds.select('{}.cv[2]'.format(CTL1[0]))
    cmds.move(2.1, 0, 0.3)
    cmds.select('{}.cv[3]'.format(CTL1[0]))
    cmds.move(2.7, 0, 0)
    
    cmds.delete(CTL1[0], ch=1)
    cmds.parent('{}Shape1'.format(o), o, add=1, s=1)
    cmds.delete(CTL1[0])
    cmds.select(o)
    
    for o in cmds.listRelatives(o, s=1):
        cmds.select(o+'.cv[*]')
        cmds.rotate(0, 0, 270)
    cmds.select(o)
    
def shapeChange17_CL(o, shapeColor, shapeBold):
    shapeList = cmds.listRelatives(o, s=1)
    
    for i in shapeList:
        cmds.delete(i)
        
    CTL = cmds.circle(n='{}TEMP'.format(o), normalX=0, normalY=0, normalZ=0)
    cmds.rename(cmds.listRelatives(CTL[0], s=1), '{}Shape'.format(o))
    try:
        cmds.setAttr('{}Shape.overrideEnabled'.format(o), 1)
        cmds.setAttr('{}Shape.overrideColor'.format(o), shapeColor)
        cmds.setAttr('{}Shape.lineWidth'.format(o), shapeBold)
    except:
        pass
    
    cmds.setAttr('{}.sections'.format(CTL[1]), 24)
    cmds.setAttr('{}.degree'.format(CTL[1]), 1)
    cmds.addAttr(CTL[0], ln='radius', at='double', k=0, dv=1)
    cmds.setAttr('{}.radius'.format(CTL[0]), l=1)
    cmds.addAttr(CTL[0], ln='shapeType', dt='string')
    cmds.setAttr('{}.shapeType'.format(CTL[0]), 'castle', type='string', l=1)
    
    cmds.select('{}.cv[0]'.format(CTL[0]))
    cmds.move(2, -0.25, 0)
    cmds.select('{}.cv[1]'.format(CTL[0]))
    cmds.move(1.75, -0.25, -1)
    cmds.select('{}.cv[2]'.format(CTL[0]))
    cmds.move(1.75, 0.25, -1)
    cmds.select('{}.cv[3]'.format(CTL[0]))
    cmds.move(1, 0.25, -1.75)
    cmds.select('{}.cv[4]'.format(CTL[0]))
    cmds.move(1, -0.25, -1.75)
    cmds.select('{}.cv[5]'.format(CTL[0]))
    cmds.move(0, -0.25, -2)
    cmds.select('{}.cv[6]'.format(CTL[0]))
    cmds.move(0, 0.25, -2)
    cmds.select('{}.cv[7]'.format(CTL[0]))
    cmds.move(-1, 0.25, -1.75)
    cmds.select('{}.cv[8]'.format(CTL[0]))
    cmds.move(-1, -0.25, -1.75)
    cmds.select('{}.cv[9]'.format(CTL[0]))
    cmds.move(-1.75, -0.25, -1)
    cmds.select('{}.cv[10]'.format(CTL[0]))
    cmds.move(-1.75, 0.25, -1)
    cmds.select('{}.cv[11]'.format(CTL[0]))
    cmds.move(-2, 0.25, 0)
    cmds.select('{}.cv[12]'.format(CTL[0]))
    cmds.move(-2, -0.25, 0)
    cmds.select('{}.cv[13]'.format(CTL[0]))
    cmds.move(-1.75, -0.25, 1)
    cmds.select('{}.cv[14]'.format(CTL[0]))
    cmds.move(-1.75, 0.25, 1)
    cmds.select('{}.cv[15]'.format(CTL[0]))
    cmds.move(-1, 0.25, 1.75)
    cmds.select('{}.cv[16]'.format(CTL[0]))
    cmds.move(-1, -0.25, 1.75)
    cmds.select('{}.cv[17]'.format(CTL[0]))
    cmds.move(0, -0.25, 2)
    cmds.select('{}.cv[18]'.format(CTL[0]))
    cmds.move(0, 0.25, 2)
    cmds.select('{}.cv[19]'.format(CTL[0]))
    cmds.move(1, 0.25, 1.75)
    cmds.select('{}.cv[20]'.format(CTL[0]))
    cmds.move(1, -0.25, 1.75)
    cmds.select('{}.cv[21]'.format(CTL[0]))
    cmds.move(1.75, -0.25, 1)
    cmds.select('{}.cv[22]'.format(CTL[0]))
    cmds.move(1.75, 0.25, 1)
    cmds.select('{}.cv[23]'.format(CTL[0]))
    cmds.move(2, 0.25, 0)
    cmds.select('{}.cv[24]'.format(CTL[0]))
    cmds.move(2, -0.25, 0)
    
    cmds.delete(CTL[0], ch=1)
    cmds.parent('{}Shape'.format(o), o, add=1, s=1)
    cmds.delete(CTL[0])
    cmds.select(o)
    
def shapeChange18_CL(o, shapeColor, shapeBold):
    shapeList = cmds.listRelatives(o, s=1)
    
    for i in shapeList:
        cmds.delete(i)
        
    CTL = cmds.circle(n='{}TEMP'.format(o), normalX=0, normalY=0, normalZ=0)
    cmds.rename(cmds.listRelatives(CTL[0], s=1), '{}Shape'.format(o))
    try:
        cmds.setAttr('{}Shape.overrideEnabled'.format(o), 1)
        cmds.setAttr('{}Shape.overrideColor'.format(o), shapeColor)
        cmds.setAttr('{}Shape.lineWidth'.format(o), shapeBold)
    except:
        pass
    
    cmds.setAttr('{}.sections'.format(CTL[1]), 3)
    cmds.setAttr('{}.degree'.format(CTL[1]), 1)
    cmds.addAttr(CTL[0], ln='radius', at='double', k=0, dv=1)
    cmds.setAttr('{}.radius'.format(CTL[0]), l=1)
    cmds.addAttr(CTL[0], ln='shapeType', dt='string')
    cmds.setAttr('{}.shapeType'.format(CTL[0]), 'fingerPlate', type='string', l=1)
    
    cmds.select('{}.cv[0]'.format(CTL[0]))
    cmds.move(0, 0, -0.25)
    cmds.select('{}.cv[1]'.format(CTL[0]))
    cmds.move(3, 0, -0.25)
    cmds.select('{}.cv[2]'.format(CTL[0]))
    cmds.move(3, 0, 0.25)
    cmds.select('{}.cv[3]'.format(CTL[0]))
    cmds.move(0, 0, 0.25)
    
    cmds.select('{}.cv[0:3]'.format(CTL[0]))
    cmds.rotate(90, 0, 0)
    
    cmds.delete(CTL[0], ch=1)
    cmds.parent('{}Shape'.format(o), o, add=1, s=1)
    cmds.delete(CTL[0])
    cmds.select(o)
    
    for o in cmds.listRelatives(o, s=1):
        cmds.select(o+'.cv[*]')
        cmds.rotate(0, 0, 270)
    cmds.select(o)
    
def shapeChange19_CL(o, shapeColor, shapeBold):
    shapeList = cmds.listRelatives(o, s=1)
    
    for i in shapeList:
        cmds.delete(i)
        
    CTL = cmds.circle(n='{}TEMP'.format(o), normalX=0, normalY=0, normalZ=0)
    cmds.rename(cmds.listRelatives(CTL[0], s=1), '{}Shape'.format(o))
    try:
        cmds.setAttr('{}Shape.overrideEnabled'.format(o), 1)
        cmds.setAttr('{}Shape.overrideColor'.format(o), shapeColor)
        cmds.setAttr('{}Shape.lineWidth'.format(o), shapeBold)
    except:
        pass
    
    cmds.setAttr('{}.sections'.format(CTL[1]), 6)
    cmds.setAttr('{}.degree'.format(CTL[1]), 1)
    cmds.addAttr(CTL[0], ln='radius', at='double', k=0, dv=1)
    cmds.setAttr('{}.radius'.format(CTL[0]), l=1)
    cmds.addAttr(CTL[0], ln='shapeType', dt='string')
    cmds.setAttr('{}.shapeType'.format(CTL[0]), 'pinPlate', type='string', l=1)
    
    cmds.select('{}.cv[0]'.format(CTL[0]))
    cmds.move(0, 0, 0)
    cmds.select('{}.cv[1]'.format(CTL[0]))
    cmds.move(2.2, 0, 0)
    cmds.select('{}.cv[2]'.format(CTL[0]))
    cmds.move(2.6, 0, -0.4)
    cmds.select('{}.cv[3]'.format(CTL[0]))
    cmds.move(3, 0, 0)
    cmds.select('{}.cv[4]'.format(CTL[0]))
    cmds.move(2.6, 0, 0.4)
    cmds.select('{}.cv[5]'.format(CTL[0]))
    cmds.move(2.2, 0, 0)
    cmds.select('{}.cv[6]'.format(CTL[0]))
    cmds.move(0, 0, 0)
    
    cmds.select('{}.cv[0:6]'.format(CTL[0]))
    cmds.rotate(90, 0, 0)
    
    cmds.delete(CTL[0], ch=1)
    cmds.parent('{}Shape'.format(o), o, add=1, s=1)
    cmds.delete(CTL[0])
    cmds.select(o)
    
    for o in cmds.listRelatives(o, s=1):
        cmds.select(o+'.cv[*]')
        cmds.rotate(0, 0, 270)
    cmds.select(o)
    
def shapeChange20_CL(o, shapeColor, shapeBold):
    shapeList = cmds.listRelatives(o, s=1)
    
    for i in shapeList:
        cmds.delete(i)
        
    CTL = cmds.circle(n='{}TEMP'.format(o), normalX=0, normalY=0, normalZ=0)
    cmds.rename(cmds.listRelatives(CTL[0], s=1), '{}Shape'.format(o))
    try:
        cmds.setAttr('{}Shape.overrideEnabled'.format(o), 1)
        cmds.setAttr('{}Shape.overrideColor'.format(o), shapeColor)
        cmds.setAttr('{}Shape.lineWidth'.format(o), shapeBold)
    except:
        pass
    
    cmds.setAttr('{}.sections'.format(CTL[1]), 10)
    cmds.setAttr('{}.degree'.format(CTL[1]), 1)
    cmds.addAttr(CTL[0], ln='radius', at='double', k=0, dv=1)
    cmds.setAttr('{}.radius'.format(CTL[0]), l=1)
    cmds.addAttr(CTL[0], ln='shapeType', dt='string')
    cmds.setAttr('{}.shapeType'.format(CTL[0]), 'locator', type='string', l=1)
    
    cmds.select('{}.cv[0]'.format(CTL[0]))
    cmds.move(0, 2, 0)
    cmds.select('{}.cv[1]'.format(CTL[0]))
    cmds.move(0, 0, 0)
    cmds.select('{}.cv[2]'.format(CTL[0]))
    cmds.move(2, 0, 0)
    cmds.select('{}.cv[3]'.format(CTL[0]))
    cmds.move(0, 0, 0)
    cmds.select('{}.cv[4]'.format(CTL[0]))
    cmds.move(0, 0, 2)
    cmds.select('{}.cv[5]'.format(CTL[0]))
    cmds.move(0, 0, 0)
    cmds.select('{}.cv[6]'.format(CTL[0]))
    cmds.move(-2, 0, 0)
    cmds.select('{}.cv[7]'.format(CTL[0]))
    cmds.move(0, 0, 0)
    cmds.select('{}.cv[8]'.format(CTL[0]))
    cmds.move(0, 0, -2)
    cmds.select('{}.cv[9]'.format(CTL[0]))
    cmds.move(0, 0, 0)
    cmds.select('{}.cv[10]'.format(CTL[0]))
    cmds.move(0, -2, 0)
    
    cmds.delete(CTL[0], ch=1)
    cmds.parent('{}Shape'.format(o), o, add=1, s=1)
    cmds.delete(CTL[0])
    cmds.select(o)
    
def shapeChange21_CL(o, shapeColor, shapeBold):
    shapeList = cmds.listRelatives(o, s=1)
    
    for i in shapeList:
        cmds.delete(i)
        
    CTL = cmds.circle(n='{}TEMP'.format(o), normalX=0, normalY=0, normalZ=0)
    cmds.rename(cmds.listRelatives(CTL[0], s=1), '{}Shape'.format(o))
    try:
        cmds.setAttr('{}Shape.overrideEnabled'.format(o), 1)
        cmds.setAttr('{}Shape.overrideColor'.format(o), shapeColor)
        cmds.setAttr('{}Shape.lineWidth'.format(o), shapeBold)
    except:
        pass
    
    cmds.setAttr('{}.sections'.format(CTL[1]), 10)
    cmds.setAttr('{}.degree'.format(CTL[1]), 1)
    cmds.addAttr(CTL[0], ln='radius', at='double', k=0, dv=1)
    cmds.setAttr('{}.radius'.format(CTL[0]), l=1)
    cmds.addAttr(CTL[0], ln='shapeType', dt='string')
    cmds.setAttr('{}.shapeType'.format(CTL[0]), 'pyramid', type='string', l=1)
    
    cmds.select('{}.cv[0]'.format(CTL[0]))
    cmds.move(1.5, 0, 1.5)
    cmds.select('{}.cv[1]'.format(CTL[0]))
    cmds.move(0, 2, 0)
    cmds.select('{}.cv[2]'.format(CTL[0]))
    cmds.move(-1.5, 0, 1.5)
    cmds.select('{}.cv[3]'.format(CTL[0]))
    cmds.move(1.5, 0, 1.5)
    cmds.select('{}.cv[4]'.format(CTL[0]))
    cmds.move(1.5, 0, -1.5)
    cmds.select('{}.cv[5]'.format(CTL[0]))
    cmds.move(0, 2, 0)
    cmds.select('{}.cv[6]'.format(CTL[0]))
    cmds.move(-1.5, 0, -1.5)
    cmds.select('{}.cv[7]'.format(CTL[0]))
    cmds.move(1.5, 0, -1.5)
    cmds.select('{}.cv[8]'.format(CTL[0]))
    cmds.move(-1.5, 0, 1.5)
    cmds.select('{}.cv[9]'.format(CTL[0]))
    cmds.move(-1.5, 0, -1.5)
    cmds.select('{}.cv[10]'.format(CTL[0]))
    cmds.move(1.5, 0, 1.5)
    
    cmds.delete(CTL[0], ch=1)
    cmds.parent('{}Shape'.format(o), o, add=1, s=1)
    cmds.delete(CTL[0])
    cmds.select(o)

def shapeChange22_CL(o, shapeColor, shapeBold):
    shapeList = cmds.listRelatives(o, s=1)
    
    for i in shapeList:
        cmds.delete(i)
        
    CTL = cmds.circle(n='{}TEMP'.format(o), normalX=0, normalY=0, normalZ=0)
    cmds.rename(cmds.listRelatives(CTL[0], s=1), '{}Shape'.format(o))
    try:
        cmds.setAttr('{}Shape.overrideEnabled'.format(o), 1)
        cmds.setAttr('{}Shape.overrideColor'.format(o), shapeColor)
        cmds.setAttr('{}Shape.lineWidth'.format(o), shapeBold)
    except:
        pass
    
    cmds.setAttr('{}.sections'.format(CTL[1]), 25)
    cmds.setAttr('{}.degree'.format(CTL[1]), 1)
    cmds.addAttr(CTL[0], ln='radius', at='double', k=0, dv=1)
    cmds.setAttr('{}.radius'.format(CTL[0]), l=1)
    cmds.addAttr(CTL[0], ln='shapeType', dt='string')
    cmds.setAttr('{}.shapeType'.format(CTL[0]), 'sims', type='string', l=1)
    
    cmds.select('{}.cv[0]'.format(CTL[0]))
    cmds.move(0, 5, 0)
    cmds.select('{}.cv[1]'.format(CTL[0]))
    cmds.move(2, 0, 2)
    cmds.select('{}.cv[2]'.format(CTL[0]))
    cmds.move(0, -5, 0)
    cmds.select('{}.cv[3]'.format(CTL[0]))
    cmds.move(0, 0, 3)
    cmds.select('{}.cv[4]'.format(CTL[0]))
    cmds.move(0, 5, 0)
    cmds.select('{}.cv[5]'.format(CTL[0]))
    cmds.move(-2, 0, 2)
    cmds.select('{}.cv[6]'.format(CTL[0]))
    cmds.move(0, -5, 0)
    cmds.select('{}.cv[7]'.format(CTL[0]))
    cmds.move(-3, 0, 0)
    cmds.select('{}.cv[8]'.format(CTL[0]))
    cmds.move(0, 5, 0)
    cmds.select('{}.cv[9]'.format(CTL[0]))
    cmds.move(-2, 0, -2)
    cmds.select('{}.cv[10]'.format(CTL[0]))
    cmds.move(0, -5, 0)
    cmds.select('{}.cv[11]'.format(CTL[0]))
    cmds.move(0, 0, -3)
    cmds.select('{}.cv[12]'.format(CTL[0]))
    cmds.move(0, 5, 0)
    cmds.select('{}.cv[13]'.format(CTL[0]))
    cmds.move(2, 0, -2)
    cmds.select('{}.cv[14]'.format(CTL[0]))
    cmds.move(0, -5, 0)
    cmds.select('{}.cv[15]'.format(CTL[0]))
    cmds.move(3, 0, 0)
    cmds.select('{}.cv[16]'.format(CTL[0]))
    cmds.move(0, 5, 0)
    cmds.select('{}.cv[17]'.format(CTL[0]))
    cmds.move(2, 0, 2)
    cmds.select('{}.cv[18]'.format(CTL[0]))
    cmds.move(0, 0, 3)
    cmds.select('{}.cv[19]'.format(CTL[0]))
    cmds.move(-2, 0, 2)
    cmds.select('{}.cv[20]'.format(CTL[0]))
    cmds.move(-3, 0, 0)
    cmds.select('{}.cv[21]'.format(CTL[0]))
    cmds.move(-2, 0, -2)
    cmds.select('{}.cv[22]'.format(CTL[0]))
    cmds.move(0, 0, -3)
    cmds.select('{}.cv[23]'.format(CTL[0]))
    cmds.move(2, 0, -2)
    cmds.select('{}.cv[24]'.format(CTL[0]))
    cmds.move(3, 0, 0)
    cmds.select('{}.cv[25]'.format(CTL[0]))
    cmds.move(2, 0, 2)
    
    cmds.delete(CTL[0], ch=1)
    cmds.parent('{}Shape'.format(o), o, add=1, s=1)
    cmds.delete(CTL[0])
    cmds.select(o)

def shapeChange23_CL(o, shapeColor, shapeBold):
    shapeList = cmds.listRelatives(o, s=1)
    
    for i in shapeList:
        cmds.delete(i)
        
    CTL = cmds.circle(n='{}TEMP'.format(o), normalX=0, normalY=0, normalZ=0)
    cmds.rename(cmds.listRelatives(CTL[0], s=1), '{}Shape'.format(o))
    try:
        cmds.setAttr('{}Shape.overrideEnabled'.format(o), 1)
        cmds.setAttr('{}Shape.overrideColor'.format(o), shapeColor)
        cmds.setAttr('{}Shape.lineWidth'.format(o), shapeBold)
    except:
        pass
    
    cmds.setAttr('{}.sections'.format(CTL[1]), 13)
    cmds.setAttr('{}.degree'.format(CTL[1]), 1)
    cmds.addAttr(CTL[0], ln='radius', at='double', k=0, dv=1)
    cmds.setAttr('{}.radius'.format(CTL[0]), l=1)
    cmds.addAttr(CTL[0], ln='shapeType', dt='string')
    cmds.setAttr('{}.shapeType'.format(CTL[0]), 'pingpong', type='string', l=1)
    
    cmds.select('{}.cv[0]'.format(CTL[0]))
    cmds.move(0, 0, 0)
    cmds.select('{}.cv[1]'.format(CTL[0]))
    cmds.move(0, 2.25, 0)
    cmds.select('{}.cv[2]'.format(CTL[0]))
    cmds.move(-0.5, 2.5, 0)
    cmds.select('{}.cv[3]'.format(CTL[0]))
    cmds.move(0.5, 3.5, 0)
    cmds.select('{}.cv[4]'.format(CTL[0]))
    cmds.move(-0.5, 2.5, 0)
    cmds.select('{}.cv[5]'.format(CTL[0]))
    cmds.move(-0.75, 3, 0)
    cmds.select('{}.cv[6]'.format(CTL[0]))
    cmds.move(-0.5, 3.5, 0)
    cmds.select('{}.cv[7]'.format(CTL[0]))
    cmds.move(0.5, 2.5, 0)
    cmds.select('{}.cv[8]'.format(CTL[0]))
    cmds.move(-0.5, 3.5, 0)
    cmds.select('{}.cv[9]'.format(CTL[0]))
    cmds.move(0, 3.75, 0)
    cmds.select('{}.cv[10]'.format(CTL[0]))
    cmds.move(0.5, 3.5, 0)
    cmds.select('{}.cv[11]'.format(CTL[0]))
    cmds.move(0.75, 3, 0)
    cmds.select('{}.cv[12]'.format(CTL[0]))
    cmds.move(0.5, 2.5, 0)
    cmds.select('{}.cv[13]'.format(CTL[0]))
    cmds.move(0, 2.25, 0)
    
    cmds.delete(CTL[0], ch=1)
    cmds.parent('{}Shape'.format(o), o, add=1, s=1)
    cmds.delete(CTL[0])
    cmds.select(o)

def shapeChange24_CL(o, shapeColor, shapeBold):
    shapeList = cmds.listRelatives(o, s=1)
    
    for i in shapeList:
        cmds.delete(i)
        
    CTL = cmds.circle(n='{}TEMP'.format(o), normalX=0, normalY=0, normalZ=0)
    cmds.rename(cmds.listRelatives(CTL[0], s=1), '{}Shape'.format(o))
    try:
        cmds.setAttr('{}Shape.overrideEnabled'.format(o), 1)
        cmds.setAttr('{}Shape.overrideColor'.format(o), shapeColor)
        cmds.setAttr('{}Shape.lineWidth'.format(o), shapeBold)
    except:
        pass
    
    cmds.setAttr('{}.sections'.format(CTL[1]), 17)
    cmds.setAttr('{}.degree'.format(CTL[1]), 1)
    cmds.addAttr(CTL[0], ln='radius', at='double', k=0, dv=1)
    cmds.setAttr('{}.radius'.format(CTL[0]), l=1)
    cmds.addAttr(CTL[0], ln='shapeType', dt='string')
    cmds.setAttr('{}.shapeType'.format(CTL[0]), 'inbetween', type='string', l=1)
    
    cmds.select('{}.cv[0]'.format(CTL[0]))
    cmds.move(2, 0, 0)
    cmds.select('{}.cv[1]'.format(CTL[0]))
    cmds.move(2.15, 0.35, 0)
    cmds.select('{}.cv[2]'.format(CTL[0]))
    cmds.move(2.5, 0.5, 0)
    cmds.select('{}.cv[3]'.format(CTL[0]))
    cmds.move(2.85, 0.35, 0)
    cmds.select('{}.cv[4]'.format(CTL[0]))
    cmds.move(3, 0, 0)
    cmds.select('{}.cv[5]'.format(CTL[0]))
    cmds.move(2.85, -0.35, 0)
    cmds.select('{}.cv[6]'.format(CTL[0]))
    cmds.move(2.5, -0.5, 0)
    cmds.select('{}.cv[7]'.format(CTL[0]))
    cmds.move(2.15, -0.35, 0)
    cmds.select('{}.cv[8]'.format(CTL[0]))
    cmds.move(2, 0, 0)
    cmds.select('{}.cv[9]'.format(CTL[0]))
    cmds.move(-2, 0, 0)
    cmds.select('{}.cv[10]'.format(CTL[0]))
    cmds.move(-2.15, 0.35, 0)
    cmds.select('{}.cv[11]'.format(CTL[0]))
    cmds.move(-2.5, 0.5, 0)
    cmds.select('{}.cv[12]'.format(CTL[0]))
    cmds.move(-2.85, 0.35, 0)
    cmds.select('{}.cv[13]'.format(CTL[0]))
    cmds.move(-3, 0, 0)
    cmds.select('{}.cv[14]'.format(CTL[0]))
    cmds.move(-2.85, -0.35, 0)
    cmds.select('{}.cv[15]'.format(CTL[0]))
    cmds.move(-2.5, -0.5, 0)
    cmds.select('{}.cv[16]'.format(CTL[0]))
    cmds.move(-2.15, -0.35, 0)
    cmds.select('{}.cv[17]'.format(CTL[0]))
    cmds.move(-2, 0, 0)
    
    cmds.delete(CTL[0], ch=1)
    cmds.parent('{}Shape'.format(o), o, add=1, s=1)
    cmds.delete(CTL[0])
    cmds.select(o)

def shapeChange25_CL(o, shapeColor, shapeBold):
    shapeList = cmds.listRelatives(o, s=1)
    
    for i in shapeList:
        cmds.delete(i)
        
    CTL = cmds.circle(n='{}TEMP'.format(o), normalX=0, normalY=0, normalZ=0)
    cmds.rename(cmds.listRelatives(CTL[0], s=1), '{}Shape'.format(o))
    try:
        cmds.setAttr('{}Shape.overrideEnabled'.format(o), 1)
        cmds.setAttr('{}Shape.overrideColor'.format(o), shapeColor)
        cmds.setAttr('{}Shape.lineWidth'.format(o), shapeBold)
    except:
        pass
    
    cmds.setAttr('{}.sections'.format(CTL[1]), 24)
    cmds.setAttr('{}.degree'.format(CTL[1]), 1)
    cmds.addAttr(CTL[0], ln='radius', at='double', k=0, dv=1)
    cmds.setAttr('{}.radius'.format(CTL[0]), l=1)
    cmds.addAttr(CTL[0], ln='shapeType', dt='string')
    cmds.setAttr('{}.shapeType'.format(CTL[0]), 'setting', type='string', l=1)
    
    cmds.select('{}.cv[0]'.format(CTL[0]))
    cmds.move(0, 4, 0)
    cmds.select('{}.cv[1]'.format(CTL[0]))
    cmds.move(0, 5.5, 0)
    cmds.select('{}.cv[2]'.format(CTL[0]))
    cmds.move(2.75, 4.75, 0)
    cmds.select('{}.cv[3]'.format(CTL[0]))
    cmds.move(2, 3.5, 0)
    cmds.select('{}.cv[4]'.format(CTL[0]))
    cmds.move(3.5, 2, 0)
    cmds.select('{}.cv[5]'.format(CTL[0]))
    cmds.move(4.75, 2.75, 0)
    cmds.select('{}.cv[6]'.format(CTL[0]))
    cmds.move(5.5, 0, 0)
    cmds.select('{}.cv[7]'.format(CTL[0]))
    cmds.move(4, 0, 0)
    cmds.select('{}.cv[8]'.format(CTL[0]))
    cmds.move(3.5, -2, 0)
    cmds.select('{}.cv[9]'.format(CTL[0]))
    cmds.move(4.75, -2.75, 0)
    cmds.select('{}.cv[10]'.format(CTL[0]))
    cmds.move(2.75, -4.75, 0)
    cmds.select('{}.cv[11]'.format(CTL[0]))
    cmds.move(2, -3.5, 0)
    cmds.select('{}.cv[12]'.format(CTL[0]))
    cmds.move(0, -4, 0)
    cmds.select('{}.cv[13]'.format(CTL[0]))
    cmds.move(0, -5.5, 0)
    cmds.select('{}.cv[14]'.format(CTL[0]))
    cmds.move(-2.75, -4.75, 0)
    cmds.select('{}.cv[15]'.format(CTL[0]))
    cmds.move(-2, -3.5, 0)
    cmds.select('{}.cv[16]'.format(CTL[0]))
    cmds.move(-3.5, -2, 0)
    cmds.select('{}.cv[17]'.format(CTL[0]))
    cmds.move(-4.75, -2.75, 0)
    cmds.select('{}.cv[18]'.format(CTL[0]))
    cmds.move(-5.5, 0, 0)
    cmds.select('{}.cv[19]'.format(CTL[0]))
    cmds.move(-4, 0, 0)
    cmds.select('{}.cv[20]'.format(CTL[0]))
    cmds.move(-3.5, 2, 0)
    cmds.select('{}.cv[21]'.format(CTL[0]))
    cmds.move(-4.75, 2.75, 0)
    cmds.select('{}.cv[22]'.format(CTL[0]))
    cmds.move(-2.75, 4.75, 0)
    cmds.select('{}.cv[23]'.format(CTL[0]))
    cmds.move(-2, 3.5, 0)
    cmds.select('{}.cv[24]'.format(CTL[0]))
    cmds.move(0, 4, 0)
    
    cmds.delete(CTL[0], ch=1)
    cmds.parent('{}Shape'.format(o), o, add=1, s=1)
    cmds.delete(CTL[0])
    cmds.select(o)
    
    CTL1 = cmds.circle(n='{}1'.format(o), normalX=0, normalY=0, normalZ=0)
    cmds.rename(cmds.listRelatives(CTL1[0], s=1), '{}Shape1'.format(o))
    cmds.setAttr('{}Shape1.overrideEnabled'.format(o), 1)
    cmds.setAttr('{}Shape1.overrideColor'.format(o), shapeColor)
    cmds.setAttr('{}Shape1.lineWidth'.format(o), shapeBold)
    
    cmds.setAttr('{}.sections'.format(CTL1[1]), 12)
    cmds.setAttr('{}.degree'.format(CTL1[1]), 1)
    cmds.addAttr(CTL1[0], ln='radius', at='double', k=0, dv=1)
    cmds.setAttr('{}.radius'.format(CTL1[0]), l=1)
    cmds.addAttr(CTL1[0], ln='shapeType', dt='string')
    cmds.setAttr('{}.shapeType'.format(CTL1[0]), 'settingCircle', type='string', l=1)
    
    cmds.select('{}.cv[0]'.format(CTL1[0]))
    cmds.move(0, 2.5, 0)
    cmds.select('{}.cv[1]'.format(CTL1[0]))
    cmds.move(1.25, 2.25, 0)
    cmds.select('{}.cv[2]'.format(CTL1[0]))
    cmds.move(2.25, 1.25, 0)
    cmds.select('{}.cv[3]'.format(CTL1[0]))
    cmds.move(2.5, 0, 0)
    cmds.select('{}.cv[4]'.format(CTL1[0]))
    cmds.move(2.25, -1.25, 0)
    cmds.select('{}.cv[5]'.format(CTL1[0]))
    cmds.move(1.25, -2.25, 0)
    cmds.select('{}.cv[6]'.format(CTL1[0]))
    cmds.move(0, -2.5, 0)
    cmds.select('{}.cv[7]'.format(CTL1[0]))
    cmds.move(-1.25, -2.25, 0)
    cmds.select('{}.cv[8]'.format(CTL1[0]))
    cmds.move(-2.25, -1.25, 0)
    cmds.select('{}.cv[9]'.format(CTL1[0]))
    cmds.move(-2.5, 0, 0)
    cmds.select('{}.cv[10]'.format(CTL1[0]))
    cmds.move(-2.25, 1.25, 0)
    cmds.select('{}.cv[11]'.format(CTL1[0]))
    cmds.move(-1.25, 2.25, 0)
    cmds.select('{}.cv[12]'.format(CTL1[0]))
    cmds.move(0, 2.5, 0)
    
    cmds.delete(CTL1[0], ch=1)
    cmds.parent('{}Shape1'.format(o), o, add=1, s=1)
    cmds.delete(CTL1[0])
    cmds.select(o)
    
    cmds.select(o+'Shape1.cv[*]')
    cmds.scale(0.7, 0.7, 0.7)
    cmds.select(o)

###

def importController_CL():
    selected = cmds.ls(os=1)
    selectList = []
    
    if selected == []:
        name = '{}default0{}'.format(C_side, CTL_name)
        list = cmds.ls('{}default*{}'.format(C_side, CTL_name), type='transform')
        
        if not list == []:
            name = '{}default{}{}'.format(C_side, len(list), CTL_name)
        
        selectList.append(name)
        CTL = cmds.circle(n=name, normalX=0, normalY=0, normalZ=0)
        shapeList = cmds.listRelatives(CTL[0], s=1)
        
        for i in shapeList:
            cmds.delete(i)
        cmds.delete(CTL[0], ch=1)
        
        shapeChange0_CL(CTL[0], 21, 1)
        
        shapeList = cmds.listRelatives(CTL[0], s=1)
        for a in shapeList:
            for i in ['aiRenderCurve', 'aiCurveWidth', 'aiSampleRate', 'aiCurveShaderR', 'aiCurveShaderG', 'aiCurveShaderB']:
                try:
                    cmds.setAttr('{}.{}'.format(a, i), l=1, k=0)
                except:
                    pass
    else:
        for o in range(len(selected)):
            findName(selected[o])
            name = findNameResult + CTL_name
            list = cmds.ls('{}default*{}'. format(C_side, CTL_name), type='transform')
            
            if not list == []:
                name = '{}default{}{}'.format(C_side, len(list), CTL_name)
            
            search = cmds.ls('*'+name+'*', type='transform')
            
            if search == []:
                selectList.append(name)
            else:
                selectList.append(name + str(len(search)))
            
            CTL = cmds.circle(n=name, normalX=0, normalY=0, normalZ=0)
            shapeList = cmds.listRelatives(CTL[0], s=1)
            
            #for i in shapeList:
            #    cmds.delete(i)
            
            cmds.delete(CTL[0], ch=1)
            
            shapeChange0_CL(CTL[0], 21, 1)
            
            shapeList = cmds.listRelatives(CTL[0], s=1)
            for a in shapeList:
                for i in ['aiRenderCurve', 'aiCurveWidth', 'aiSampleRate', 'aiCurveShaderR', 'aiCurveShaderG', 'aiCurveShaderB']:
                    try:
                        cmds.setAttr('{}.{}'.format(a, i), l=1, k=0)
                    except:
                        pass
            
            cmds.delete(cmds.parentConstraint(selected[o], selectList[-1], mo=False))
        
    cmds.select(selectList)
    
def importSuper_CL():
    super_Name = 'super'
    main_Name = 'Main'
    sub_Name = 'Sub'
    cog_Name = 'Cog'
    C_side = ''
    rig_Name = 'rig'
    root_Name = 'root'
    pacscn_Name = 'pacscn_grp'
    
    cmds.select(d=True)
    if not cmds.objExists(root_Name):
        cmds.joint(n=root_Name)
    if not cmds.objExists(rig_Name):
        cmds.group(empty=True, n=rig_Name)
    if not cmds.objExists(pacscn_Name):
        cmds.group(empty=True, n=pacscn_Name)
        cmds.parent(pacscn_Name, rig_Name)
    
    name = '{}{}{}'.format(C_side, main_Name, CTL_name)
    list = cmds.ls('{}{}*{}'.format(C_side, main_Name, CTL_name), type='transform')
    if not list == []: name = '{}{}{}{}'.format(C_side, main_Name, len(list), CTL_name)
    CTLMain = cmds.circle(n=name, normalX=0, normalY=0, normalZ=0)
    shapeList = cmds.listRelatives(CTLMain[0], s=1)
    for i in shapeList: cmds.delete(i)
    cmds.delete(CTLMain[0], ch=1)
    shapeChange7_CL(CTLMain[0], 17, 1.5)
    shapeList = cmds.listRelatives(CTLMain[0], s=1)
    for a in shapeList:
        for i in ['aiRenderCurve', 'aiCurveWidth', 'aiSampleRate', 'aiCurveShaderR', 'aiCurveShaderG', 'aiCurveShaderB']:
            try: cmds.setAttr('{}.{}'.format(a, i), l=1, k=0)
            except: pass
    cmds.select(CTLMain[0])
    scaleValueButtonPlusBit_CL()
    scaleValueButtonPlusBit_CL()
    scaleValueButtonPlusBit_CL()
    scaleValueButtonPlusBit_CL()
    scaleValueButtonPlusBit_CL()
    
    name = '{}{}{}'.format(C_side, sub_Name, CTL_name)
    list = cmds.ls('{}{}*{}'.format(C_side, sub_Name, CTL_name), type='transform')
    if not list == []: name = '{}{}{}{}'.format(C_side, sub_Name, len(list), CTL_name)
    CTLSub = cmds.circle(n=name, normalX=0, normalY=0, normalZ=0)
    shapeList = cmds.listRelatives(CTLSub[0], s=1)
    for i in shapeList: cmds.delete(i)
    cmds.delete(CTLSub[0], ch=1)
    shapeChange12_CL(CTLSub[0], 18, 1)
    shapeList = cmds.listRelatives(CTLSub[0], s=1)
    for a in shapeList:
        for i in ['aiRenderCurve', 'aiCurveWidth', 'aiSampleRate', 'aiCurveShaderR', 'aiCurveShaderG', 'aiCurveShaderB']:
            try: cmds.setAttr('{}.{}'.format(a, i), l=1, k=0)
            except: pass
    
    name = '{}{}{}'.format(C_side, cog_Name, CTL_name)
    list = cmds.ls('{}{}*{}'.format(C_side, cog_Name, CTL_name), type='transform')
    if not list == []: name = '{}{}{}{}'.format(C_side, cog_Name, len(list), CTL_name)
    CTLCog = cmds.circle(n=name, normalX=0, normalY=0, normalZ=0)
    shapeList = cmds.listRelatives(CTLCog[0], s=1)
    for i in shapeList: cmds.delete(i)
    cmds.delete(CTLCog[0], ch=1)
    shapeChange8_CL(CTLCog[0], 21, 1)
    shapeList = cmds.listRelatives(CTLCog[0], s=1)
    for a in shapeList:
        for i in ['aiRenderCurve', 'aiCurveWidth', 'aiSampleRate', 'aiCurveShaderR', 'aiCurveShaderG', 'aiCurveShaderB']:
            try: cmds.setAttr('{}.{}'.format(a, i), l=1, k=0)
            except: pass
    cmds.select(CTLCog[0])
    scaleValueButtonMinus_CL()
    scaleValueButtonMinus_CL()
    
    cmds.setAttr('{}.scaleX'.format(CTLCog[0]), 0.8)
    cmds.setAttr('{}.scaleY'.format(CTLCog[0]), 0.8)
    cmds.setAttr('{}.scaleZ'.format(CTLCog[0]), 0.8)
    cmds.makeIdentity(CTLCog[0], apply=True, scale=True)
    
    superName = '{}{}{}'.format(C_side, super_Name, GRP_name)
    list = cmds.ls('{}{}*{}'.format(C_side, super_Name, GRP_name), type='transform')
    if not list == []: superName = '{}{}{}{}'.format(C_side, super_Name, len(list), GRP_name)
    
    bodyName = '{}{}{}'.format(C_side, main_Name, GRP_name)
    list = cmds.ls('{}{}*{}'.format(C_side, main_Name, GRP_name), type='transform')
    if not list == []: bodyName = '{}{}{}{}'.format(C_side, main_Name, len(list), GRP_name)
    
    subName = '{}{}{}'.format(C_side, sub_Name, GRP_name)
    list = cmds.ls('{}{}*{}'.format(C_side, sub_Name, GRP_name), type='transform')
    if not list == []: bodyName = '{}{}{}{}'.format(C_side, sub_Name, len(list), GRP_name)
    
    cogName = '{}{}{}'.format(C_side, cog_Name, GRP_name)
    list = cmds.ls('{}{}*{}'.format(C_side, cog_Name, GRP_name), type='transform')
    if not list == []: cogName = '{}{}{}{}'.format(C_side, cog_Name, len(list), GRP_name)
    
    superGRP = cmds.group(empty=True, n=superName)
    mainGRP = cmds.group(empty=True, n=bodyName)
    subGRP = cmds.group(empty=True, n=subName)
    cogGRP = cmds.group(empty=True, n=cogName)
    
    cmds.parent(superGRP, rig_Name)
    cmds.parent(mainGRP, superGRP)
    cmds.parent(CTLMain[0], mainGRP)
    cmds.parent(subGRP, CTLMain[0])
    cmds.parent(CTLSub[0], subGRP)
    cmds.parent(cogGRP, CTLMain[0])
    cmds.parent(CTLCog[0], cogGRP)
    
    cmds.setAttr(CTLSub[0]+'.scaleX', l=True, k=False, cb=False)
    cmds.setAttr(CTLSub[0]+'.scaleY', l=True, k=False, cb=False)
    cmds.setAttr(CTLSub[0]+'.scaleZ', l=True, k=False, cb=False)
    cmds.connectAttr('{}.translate.translateX'.format(CTLCog[0]), '{}.rotatePivot.rotatePivotX.'.format(CTLSub[0]))
    cmds.connectAttr('{}.translate.translateY'.format(CTLCog[0]), '{}.rotatePivot.rotatePivotY.'.format(CTLSub[0]))
    cmds.connectAttr('{}.translate.translateZ'.format(CTLCog[0]), '{}.rotatePivot.rotatePivotZ.'.format(CTLSub[0]))
    
    cmds.select(d=True)
    subJNT = cmds.joint(n=sub_Name+JNT_name)
    cmds.parent(subJNT, root_Name)
    cmds.setAttr(subJNT+'.segmentScaleCompensate', 0)
    pac = cmds.parentConstraint(CTLSub[0], subJNT, mo=True, n=subJNT+'_PAC')
    scn = cmds.scaleConstraint(CTLSub[0], subJNT, mo=True, n=subJNT+'_SCN')
    cmds.parent(pac, pacscn_Name)
    cmds.parent(scn, pacscn_Name)
    cmds.select(superGRP)
    
###

def groupController_CL():
    selected = cmds.ls(os=1)
    
    for sel in selected:
        i = str(sel)
        iSplit = i.split('_')
        iTotalNumber = len(i)
        iSplitLast = len(iSplit[-1])
        iNumber = iTotalNumber - iSplitLast-1
        iName = i[:iNumber]
        
        checkParent = []
        try:
            checkParent = cmds.listRelatives(sel, parent=True)
        except:
            pass
        
        if len(iSplit) <= 1:
            createGroup = cmds.group(empty=True, n=sel+GRP_name)
        else:
            createGroup = cmds.group(empty=True, n=iName+GRP_name)
        
        cmds.delete(cmds.parentConstraint(i, createGroup))
        cmds.delete(cmds.scaleConstraint(i, createGroup))
        cmds.parent(i, createGroup)
        
        if checkParent != None:
            cmds.parent(createGroup, checkParent[0])
        
        cmds.select(selected)

def groupJoint_CL():
    selected = cmds.ls(os=1)
    
    for sel in selected:
        i = str(sel)
        iSplit = i.split('_')
        iTotalNumber = len(i)
        iSplitLast = len(iSplit[-1])
        iNumber = iTotalNumber - iSplitLast-1
        iName = i[:iNumber]
        
        checkParent = []
        try:
            checkParent = cmds.listRelatives(sel, parent=True)
        except:
            pass
        
        if len(iSplit) <= 1:
            createGroup = cmds.group(empty=True, n=sel+TRN_name)
        else:
            createGroup = cmds.group(empty=True, n=iName+TRN_name)
        
        cmds.delete(cmds.parentConstraint(i, createGroup))
        cmds.delete(cmds.scaleConstraint(i, createGroup))
        cmds.parent(i, createGroup)
        
        if checkParent != None:
            cmds.parent(createGroup, checkParent[0])
        
        cmds.select(selected)

def selectAllControl_CL():
    sec = cmds.ls('*{}'.format(CTL_name))
    cmds.select(sec)

###

def createJoint_CL():
    sel = cmds.ls(os=1)
    jntList = []
    
    if sel != []:
        for o in sel:
            i = str(o)
            iSplit = i.split('_')
            iTotalNumber = len(i)
            iSplitLast = len(iSplit[-1])
            iNumber = iTotalNumber - iSplitLast
            iName = i[:iNumber-1]
            jnt = cmds.joint(o, n=iName+JNT_name)
            jntList.append(jnt)
        cmds.select(jntList)
    else:
        jnt = cmds.joint(n='Go_Back_Couple')
        cmds.parent(jnt, world=1)

def convertToCurve_CL():
    sel = cmds.ls(os=1)
    jntList = []
    
    for o in sel:
        findName(o)
        findNameLast(o)
        cmds.select(o)
        importController_CL()
        importController = cmds.ls(os=1)[0]
        _newName = findNameResult+CTL_name+JNT_name
        cmds.rename(importController, findNameResult+CTL_name+JNT_name)
        importController = _newName
        oShape = cmds.listRelatives(importController, s=1)
        
        for i in oShape:
            cmds.parent(i, o, add=1, s=1)
            cmds.rename(i, i.replace(CTL_name+JNT_name, findNameLastResult))
        
        try:
            oParent = cmds.listRelatives(o, parent=True)[0]
            cmds.parent(importController, oParent)
        except:
            #cmds.parent(importController, w=True)
            pass
        
        cmds.delete(importController)
        
        if cmds.checkBox('deleteOldList', query=True, value=True):
            cmds.setAttr(o+'.drawStyle', 2)

def deleteOldList_CL():
    print ('')
    print ('Delete old joint/curve list')

def convertToJoint_CL():
    sel = cmds.ls(os=1)
    jntList = []
    
    for o in sel:
        findName(o)
        cmds.select(o)
        jnt = cmds.joint(n=findNameResult+JNT_name+CTL_name)
        oShape = cmds.listRelatives(o, s=1)
        
        for i in oShape:
            cmds.parent(i, jnt, add=1, s=1)
            
        try:
            oParent = cmds.listRelatives(o, parent=True)[0]
            cmds.parent(jnt, oParent)
        except:
            cmds.parent(jnt, w=True)
    
        if cmds.checkBox('deleteOldList', query=True, value=True):
            cmds.delete(o)
            cmds.rename(jnt, str(o))
    
def createDummy_CL():
    sel = cmds.ls(os=1)
    selected = []
    
    for i in sel:
        latticeList = []
        clusterList = []
        locatorList = []
        bbox = cmds.exactWorldBoundingBox(i)
        cube = cmds.polyCube(n=i+"_cube", w=(-bbox[0]+bbox[3]), h=(-bbox[1]+bbox[4]), d=(-bbox[2]+bbox[5]))
        selected.append(cube[0])
        cls = cmds.cluster(i)
        cmds.parentConstraint(cls, cube[0], mo=0)
        cmds.delete(cn=1)
        cmds.delete(cls)
        cmds.select(selected)

###

def changeDrawStyle_CL():
    sel = cmds.ls(os=True, ap=True)
    
    for o in sel:
        shapeChange = cmds.optionMenu("changeDrawStyle", query=True, select=True)-1
        shapeColor = cmds.getAttr('{}Shape.overrideColor'.format(o))
        shapeBold = cmds.getAttr('{}Shape.lineWidth'.format(o))
        shapeList = cmds.listRelatives(o, s=1)
        
        if shapeChange == 0:
            shapeChange0_CL(o, shapeColor, shapeBold)
            
        if shapeChange == 1:
            shapeChange1_CL(o, shapeColor, shapeBold)
            
        if shapeChange == 2:
            shapeChange2_CL(o, shapeColor, shapeBold)
            
        if shapeChange == 3:
            shapeChange3_CL(o, shapeColor, shapeBold)
            
        if shapeChange == 4:
            shapeChange4_CL(o, shapeColor, shapeBold)
            
        if shapeChange == 5:
            shapeChange5_CL(o, shapeColor, shapeBold)
            
        if shapeChange == 6:
            shapeChange6_CL(o, shapeColor, shapeBold)
            
        if shapeChange == 7:
            shapeChange7_CL(o, shapeColor, shapeBold)
            
        if shapeChange == 8:
            shapeChange8_CL(o, shapeColor, shapeBold)
        
        if shapeChange == 9:
            shapeChange9_CL(o, shapeColor, shapeBold)
        
        if shapeChange == 10:
            shapeChange10_CL(o, shapeColor, shapeBold)
            
        if shapeChange == 11:
            shapeChange11_CL(o, shapeColor, shapeBold)
        
        if shapeChange == 12:
            shapeChange12_CL(o, shapeColor, shapeBold)
        
        if shapeChange == 13:
            shapeChange13_CL(o, shapeColor, shapeBold)
        
        if shapeChange == 14:
            shapeChange14_CL(o, shapeColor, shapeBold)
        
        if shapeChange == 15:
            shapeChange15_CL(o, shapeColor, shapeBold)
        
        if shapeChange == 16:
            shapeChange16_CL(o, shapeColor, shapeBold)
        
        if shapeChange == 17:
            shapeChange17_CL(o, shapeColor, shapeBold)
        
        if shapeChange == 18:
            shapeChange18_CL(o, shapeColor, shapeBold)
        
        if shapeChange == 19:
            shapeChange19_CL(o, shapeColor, shapeBold)
        
        if shapeChange == 20:
            shapeChange20_CL(o, shapeColor, shapeBold)
        
        if shapeChange == 21:
            shapeChange21_CL(o, shapeColor, shapeBold)
        
        if shapeChange == 22:
            shapeChange22_CL(o, shapeColor, shapeBold)
        
        if shapeChange == 23:
            shapeChange23_CL(o, shapeColor, shapeBold)
        
        if shapeChange == 24:
            shapeChange24_CL(o, shapeColor, shapeBold)
        
        if shapeChange == 25:
            shapeChange25_CL(o, shapeColor, shapeBold)
        
        shapeList = cmds.listRelatives(o, s=1)

        for a in shapeList:
            for i in ['aiRenderCurve', 'aiCurveWidth', 'aiSampleRate', 'aiCurveShaderR', 'aiCurveShaderG', 'aiCurveShaderB']:
                try:
                    cmds.setAttr('{}.{}'.format(a, i), l=1, k=0)
                except:
                    pass
        '''
        cmds.delete(CTL[0], ch=1)
        cmds.parent('{}Shape'.format(o), o, add=1, s=1)
        cmds.delete(CTL[0])
        cmds.select(o)
        '''
    cmds.select(sel)

###

def changeColor_CL(selected, number):
    for o in selected:
        shapeList = cmds.listRelatives(o, s=1)
        if shapeList != []:
            for i in shapeList:
                try:
                    cmds.setAttr('{}.overrideEnabled'.format(i), 1)
                    cmds.setAttr('{}.overrideColor'.format(i), number)
                except:
                    pass
        else:
            try:
                cmds.setAttr('{}.overrideEnabled'.format(o), 1)
                cmds.setAttr('{}.overrideColor'.format(o), number)
            except:
                pass

def changeColorYellow_CL():
    selected = cmds.ls(os=1)
    changeColor_CL(selected, 17)

def changeColorRed_CL():
    selected = cmds.ls(os=1)
    changeColor_CL(selected, 13)

def changeColorBlue_CL():
    selected = cmds.ls(os=1)
    changeColor_CL(selected, 6)

def changeColorCherry_CL():
    selected = cmds.ls(os=1)
    changeColor_CL(selected, 20)
    
def changeColorBlueSea_CL():
    selected = cmds.ls(os=1)
    changeColor_CL(selected, 18)
    
def changeColorOrange_CL():
    selected = cmds.ls(os=1)
    changeColor_CL(selected, 21)
    
def changeColorGreen_CL():
    selected = cmds.ls(os=1)
    changeColor_CL(selected, 14)
    
def changeColorGreenSoft_CL():
    selected = cmds.ls(os=1)
    changeColor_CL(selected, 19)
    
def changeColorBlack_CL():
    selected = cmds.ls(os=1)
    changeColor_CL(selected, 1)
    
def changeColorWhite_CL():
    selected = cmds.ls(os=1)
    changeColor_CL(selected, 16)

###

def changeBoldRead_CL():
    sel = cmds.ls(os=True)
    selRange = len(sel)
    selValue = 0
    for i in sel:
        p = cmds.getAttr(i+"Shape.lineWidth")
        selValue = p+selValue
    selectedValue = selValue/selRange
    if not sel == []:
        cmds.floatField("valueFieldBold", edit=True, value=selectedValue)

def changeBoldRun_CL():
    selected = cmds.ls(os=True)
    for o in selected:
        theValue = cmds.floatField("valueFieldBold", query=True, value=True)
        for i in cmds.ls(o+"Shape*"):
            cmds.setAttr(i+".lineWidth", theValue)
        
def boldValueButtonMinus_CL():
    selected = cmds.ls(os=True)
    for o in selected:
        for i in cmds.ls(o+"Shape*"):
            value = cmds.getAttr(i+".lineWidth")
            cmds.setAttr(i+".lineWidth", value*0.5)
        
def boldValueButtonMinusBit_CL():
    selected = cmds.ls(os=True)
    for o in selected:
        for i in cmds.ls(o+"Shape*"):
            value = cmds.getAttr(i+".lineWidth")
            cmds.setAttr(i+".lineWidth", value*0.9)
        
def boldValueButtonPlusBit_CL():
    selected = cmds.ls(os=True)
    for o in selected:
        for i in cmds.ls(o+"Shape*"):
            value = cmds.getAttr(i+".lineWidth")
            cmds.setAttr(i+".lineWidth", value*1.1)
        
def boldValueButtonPlus_CL():
    selected = cmds.ls(os=True)
    for o in selected:
        for i in cmds.ls(o+"Shape*"):
            value = cmds.getAttr(i+".lineWidth")
            cmds.setAttr(i+".lineWidth", value*2)

def changeRotationX_CL():
    selected = cmds.ls(os=1)
    for o in cmds.listRelatives(selected, s=1):
        cmds.select(o+'.cv[*]')
        cmds.rotate(90, 0, 0)
    cmds.select(selected)

def changeRotationY_CL():
    selected = cmds.ls(os=1)
    for o in cmds.listRelatives(selected, s=1):
        cmds.select(o+'.cv[*]')
        cmds.rotate(0, 90, 0)
    cmds.select(selected)

def changeRotationZ_CL():
    selected = cmds.ls(os=1)
    for o in cmds.listRelatives(selected, s=1):
        cmds.select(o+'.cv[*]')
        cmds.rotate(0, 0, 90)
    cmds.select(selected)

def scaleValueButton_CL():
    selected = cmds.ls(os=1)
    
    for o in cmds.listRelatives(selected, s=1):
        cmds.select(o+'.cv[*]')
        valueScaleX = cmds.checkBox('scaleX', query=True, value=True)
        valueScaleY = cmds.checkBox('scaleY', query=True, value=True)
        valueScaleZ = cmds.checkBox('scaleZ', query=True, value=True)
        valueScale = cmds.floatField("scaleValueField", value=True, query=True)
        
        if valueScaleX == True:
            cmds.scale(valueScale, 1, 1)
        if valueScaleY == True:
            cmds.scale(1, valueScale, 1)
        if valueScaleZ == True:
            cmds.scale(1, 1, valueScale)
    
    cmds.select(selected)

def scaleValueButtonMinus_CL():
    selected = cmds.ls(os=1)
    valueScaleX = cmds.checkBox('scaleX', query=True, value=True)
    valueScaleY = cmds.checkBox('scaleY', query=True, value=True)
    valueScaleZ = cmds.checkBox('scaleZ', query=True, value=True)
    
    for o in cmds.listRelatives(selected, s=1):
        cmds.select(o+'.cv[*]')
        
        if valueScaleX == True:
            cmds.scale(0.5, 1, 1)
        if valueScaleY == True:
            cmds.scale(1, 0.5, 1)
        if valueScaleZ == True:
            cmds.scale(1, 1, 0.5)
    
    cmds.select(selected)

def scaleValueButtonMinusBit_CL():
    selected = cmds.ls(os=1)
    valueScaleX = cmds.checkBox('scaleX', query=True, value=True)
    valueScaleY = cmds.checkBox('scaleY', query=True, value=True)
    valueScaleZ = cmds.checkBox('scaleZ', query=True, value=True)
    
    for o in cmds.listRelatives(selected, s=1):
        cmds.select(o+'.cv[*]')
        
        if valueScaleX == True:
            cmds.scale(0.9, 1, 1)
        if valueScaleY == True:
            cmds.scale(1, 0.9, 1)
        if valueScaleZ == True:
            cmds.scale(1, 1, 0.9)
    
    cmds.select(selected)

def scaleValueButtonPlusBit_CL():
    selected = cmds.ls(os=1)
    valueScaleX = cmds.checkBox('scaleX', query=True, value=True)
    valueScaleY = cmds.checkBox('scaleY', query=True, value=True)
    valueScaleZ = cmds.checkBox('scaleZ', query=True, value=True)
    
    for o in cmds.listRelatives(selected, s=1):
        cmds.select(o+'.cv[*]')
        
        if valueScaleX == True:
            cmds.scale(1.1, 1, 1)
        if valueScaleY == True:
            cmds.scale(1, 1.1, 1)
        if valueScaleZ == True:
            cmds.scale(1, 1, 1.1)
    
    cmds.select(selected)

def scaleValueButtonPlus_CL():
    selected = cmds.ls(os=1)
    valueScaleX = cmds.checkBox('scaleX', query=True, value=True)
    valueScaleY = cmds.checkBox('scaleY', query=True, value=True)
    valueScaleZ = cmds.checkBox('scaleZ', query=True, value=True)
    
    for o in cmds.listRelatives(selected, s=1):
        cmds.select(o+'.cv[*]')
        
        if valueScaleX == True:
            cmds.scale(2, 1, 1)
        if valueScaleY == True:
            cmds.scale(1, 2, 1)
        if valueScaleZ == True:
            cmds.scale(1, 1, 2)
    
    cmds.select(selected)

# --- Windows Setting ---

def resizeMainWindow_CL():
    pass
    
if (cmds.window(windowName_CL, exists=True)):
    cmds.deleteUI(windowName_CL)

cmds.window(windowName_CL, title=windowTitle_CL, iconName=windowName_CL, resizeToFitChildren=1, h=sizeHeight_CL, w=sizeWidth_CL)

windowWidth = cmds.window(windowName_CL, query=True, width=True)
windowHeight = cmds.window(windowName_CL, query=True, height=True)

cmds.columnLayout('mainWindowColumnLayout', adjustableColumn=1, w=windowWidth)
cmds.scrollLayout('mainWindowScrollLayout', rc='resizeMainWindow_CL()', minChildWidth=sizeWidth_CL, hst=0, vst=0, h=windowHeight, w=windowWidth)

mWS1m = windowWidth/2.5-holderSize_CL/2
mWS2m = (windowWidth-mWS1m)/1-(holderSize_CL/1+1)
mWS3m = (windowWidth-mWS1m)/2-(holderSize_CL/2+1)
mWS4m = (windowWidth-mWS1m)/3-(holderSize_CL/3+1)
mWS5m = (windowWidth-mWS1m)/4-(holderSize_CL/4+1.5)
mWS6m = (windowWidth-mWS1m)/5-(holderSize_CL/5+2)

menuWidthSize1 = mWS1m
menuWidthSize2 = mWS1m, mWS2m+1
menuWidthSize3 = mWS1m, mWS3m, mWS3m
menuWidthSize4 = mWS1m, mWS4m, mWS4m, mWS4m
menuWidthSize5 = mWS1m, mWS5m, mWS5m, mWS5m, mWS5m+1.5
menuWidthSize6 = mWS1m, mWS6m, mWS6m, mWS6m, mWS6m, mWS6m+2

cWS1m = (windowWidth/1)-(holderSize_CL/1+2)
cWS2m = (windowWidth/2)-(holderSize_CL/2+2)
cWS3m = (windowWidth/3)-(holderSize_CL/3+2)
cWS4m = (windowWidth/4)-(holderSize_CL/4+2)
cWS5m = (windowWidth/5)-(holderSize_CL/5+2)
cWS6m = (windowWidth/6)-(holderSize_CL/6+2)

colomnWidthSize1 = cWS1m+4
colomnWidthSize2 = cWS2m, cWS2m+4
colomnWidthSize3 = cWS3m, cWS3m, cWS3m+4
colomnWidthSize4 = cWS4m, cWS4m, cWS4m, cWS4m+2
colomnWidthSize5 = cWS5m, cWS5m, cWS5m, cWS5m, cWS5m+4
colomnWidthSize6 = cWS6m, cWS6m, cWS6m, cWS6m, cWS6m, cWS6m

# cmds.rowLayout(numberOfColumns=1, columnWidth1=(colomnWidthSize1), columnAttach=[(1, 'both', 0)])
# cmds.rowLayout(numberOfColumns=2, columnWidth2=(menuWidthSize2), columnAttach=[(1, 'both', 0), (2, 'both', 0)])
# cmds.rowLayout(numberOfColumns=3, columnWidth3=(menuWidthSize3), columnAttach=[(1, 'both', 0), (2, 'both', 0), (3, 'both', 0)])
# cmds.rowLayout(numberOfColumns=4, columnWidth4=(menuWidthSize4), columnAttach=[(1, 'both', 0), (2, 'both', 0), (3, 'both', 0), (4, 'both', 0)])
# cmds.rowLayout(numberOfColumns=5, columnWidth5=(menuWidthSize5), columnAttach=[(1, 'both', 0), (2, 'both', 0), (3, 'both', 0), (4, 'both', 0), (5, 'both', 0)])
# cmds.rowLayout(numberOfColumns=6, columnWidth6=(menuWidthSize6), columnAttach=[(1, 'both', 0), (2, 'both', 0), (3, 'both', 0), (4, 'both', 0), (5, 'both', 0), (6, 'both', 0)])

# --- Windows Tool(s) ---

cmds.rowLayout(numberOfColumns=1, columnWidth1=(300), columnAttach=[(1, "both", 0)])
cmds.text(label=sliceText_CL, align="center")
cmds.setParent('..')

cmds.rowLayout(numberOfColumns=2, columnWidth2=(colomnWidthSize2), columnAttach=[(1, 'both', 0), (2, 'both', 0)])
cmds.button("importController", label="Import Controller", command="importController_CL()")
cmds.button("importSuper", label="Import Super", command="importSuper_CL()")
cmds.setParent('..')

cmds.rowLayout(numberOfColumns=3, columnWidth3=(colomnWidthSize3), columnAttach=[(1, 'both', 0), (2, 'both', 0), (3, 'both', 0)])
cmds.button("groupController", label="Group Controller", command="groupController_CL()")
cmds.button("groupJoint", label="Group Joint", command="groupJoint_CL()")
#cmds.button("groupToSKEL", label="Group To SKEL", command="groupToSKEL_CL()")
cmds.button("createJoint", label="Create Joint", command="createJoint_CL()")
cmds.setParent('..')

colomnWidthSize3SP = cWS2m-7, 14, cWS2m-3

cmds.rowLayout(numberOfColumns=3, columnWidth3=(colomnWidthSize3SP), columnAttach=[(1, 'both', 0), (2, 'both', 0), (3, 'both', 0)])
cmds.button("convertToCurve", label="Joint to Curve", command="convertToCurve_CL()")
cmds.checkBox('deleteOldList', label='', enable=True, value=False, align='center', cc='deleteOldList_CL()')
cmds.button("convertToJoint", label="Curve to Joint", command="convertToJoint_CL()")
cmds.setParent('..')

###

cmds.rowLayout(numberOfColumns=2, columnWidth2=(menuWidthSize2), columnAttach=[(1, 'both', 0), (2, 'both', 0)])
cmds.text(label="Change Shape", align="left")
cmds.optionMenu("changeDrawStyle", changeCommand="changeDrawStyle_CL()")
cmds.menuItem('0', label='00 - Star')
cmds.menuItem('1', label='01 - Arrow')
cmds.menuItem('2', label='02 - Flat Arrow')
cmds.menuItem('3', label='03 - Rotation Arrow')
cmds.menuItem('4', label='04 - Move Arrow')
cmds.menuItem('5', label='05 - Sphere')
cmds.menuItem('6', label='06 - Cube')
cmds.menuItem('7', label='07 - Square')
cmds.menuItem('8', label='08 - Circle')
cmds.menuItem('9', label='09 - Wheel')
cmds.menuItem('10', label='10 - Arrowed Sphere')
cmds.menuItem('11', label='11 - Arrowed Square')
cmds.menuItem('12', label='12 - Arrowed Circle')
cmds.menuItem('13', label='13 - Arrowed Wheel')
cmds.menuItem('14', label='14 - Foot')
cmds.menuItem('15', label='15 - Googles')
cmds.menuItem('16', label='16 - Neck')
cmds.menuItem('17', label='17 - Castle')
cmds.menuItem('18', label='18 - Finger Plate')
cmds.menuItem('19', label='19 - Pin Plate')
cmds.menuItem('20', label='20 - Locator')
cmds.menuItem('21', label='21 - Pyramid')
cmds.menuItem('22', label='22 - Sims')
cmds.menuItem('23', label='23 - Pingpong')
cmds.menuItem('24', label='24 - Inbetween')
cmds.menuItem('25', label='25 - Setting')
cmds.optionMenu('changeDrawStyle', edit=True, sl=8)
cmds.setParent('..')

cmds.rowLayout(numberOfColumns=6, columnWidth6=(menuWidthSize6), columnAttach=[(1, 'both', 0), (2, 'both', 0), (3, 'both', 0), (4, 'both', 0), (5, 'both', 0), (6, 'both', 0)])
cmds.text(label="Change Color", align="left")
cmds.button("changeColorYellow", label="", bgc=[1, 1, 0.2], command="changeColorYellow_CL()")
cmds.button("changeColorRed", label="", bgc=[1, 0.1, 0.1], command="changeColorRed_CL()")
cmds.button("changeColorBlue", label="", bgc=[0.1, 0.1, 1], command="changeColorBlue_CL()")
cmds.button("changeColorCherry", label="", bgc=[1, 0.5, 0.7], command="changeColorCherry_CL()")
cmds.button("changeColorBlueSea", label="", bgc=[0, 1, 1], command="changeColorBlueSea_CL()")
cmds.setParent('..')

cmds.rowLayout(numberOfColumns=6, columnWidth6=(menuWidthSize6), columnAttach=[(1, 'both', 0), (2, 'both', 0), (3, 'both', 0), (4, 'both', 0), (5, 'both', 0), (6, 'both', 0)])
cmds.text(label="", align="left")
cmds.button("changeColorOrange", label="", bgc=[1, 0.8, 0.5], command="changeColorOrange_CL()")
cmds.button("changeColorGreen", label="", bgc=[0, 1, 0], command="changeColorGreen_CL()")
cmds.button("changeColorGreenSoft", label="", bgc=[0, 1, 0.5], command="changeColorGreenSoft_CL()")
cmds.button("changeColorBlack", label="", bgc=[0, 0, 0], command="changeColorBlack_CL()")
cmds.button("changeColorWhite", label="", bgc=[1, 1, 1], command="changeColorWhite_CL()")
cmds.setParent('..')

menuWidthSize4SP = mWS1m, mWS4m-35, mWS4m+70, mWS4m-35
menuWidthSize6 = mWS1m, mWS6m-9, mWS6m-22, mWS6m+65, mWS6m-22, mWS6m-9

cmds.rowLayout(numberOfColumns=6, columnWidth6=(menuWidthSize6), columnAttach=[(1, 'both', 0), (2, 'both', 0), (3, 'both', 0), (4, 'both', 0), (5, 'both', 0), (6, 'both', 0)])
cmds.text(label="Change Bold", align="left")
cmds.button('boldValueButtonMinus', label='<', command='boldValueButtonMinus_CL()')
cmds.button('boldValueButtonMinusBit', label='', command='boldValueButtonMinusBit_CL()')
cmds.floatField("valueFieldBold", value=1, pre=2, rfc="changeBoldRead_CL()" , cc="changeBoldRun_CL()")
cmds.button('boldValueButtonPlusBit', label='', command='boldValueButtonPlusBit_CL()')
cmds.button('boldValueButtonPlus', label='>', command='boldValueButtonPlus_CL()')
cmds.setParent('..')

cmds.rowLayout(numberOfColumns=4, columnWidth4=(menuWidthSize4), columnAttach=[(1, 'both', 0), (2, 'both', 0), (3, 'both', 0), (4, 'both', 0)])
cmds.text(label='Change Rotation', align='left')
cmds.button('changeRotationX', label='X', command='changeRotationX_CL()')
cmds.button('changeRotationY', label='Y', command='changeRotationY_CL()')
cmds.button('changeRotationZ', label='Z', command='changeRotationZ_CL()')
cmds.setParent('..')

cmds.rowLayout(numberOfColumns=4, columnWidth4=(menuWidthSize4), columnAttach=[(1, 'both', 0), (2, 'both', 0), (3, 'both', 0), (4, 'both', 0)])
cmds.text(label='Change Scale', align='left')
cmds.checkBox('scaleX', label='X', enable=True, value=True, align='center')
cmds.checkBox('scaleY', label='Y', enable=True, value=True, align='center')
cmds.checkBox('scaleZ', label='Z', enable=True, value=True, align='center')
cmds.setParent('..')

menuWidthSize5 = mWS1m, mWS5m+15, mWS5m-20, mWS5m+23, mWS5m-20

cmds.rowLayout(numberOfColumns=6, columnWidth6=(menuWidthSize6), columnAttach=[(1, 'both', 0), (2, 'both', 0), (3, 'both', 0), (4, 'both', 0), (5, 'both', 0), (6, 'both', 0)])
#cmds.text(label='', align='left')
cmds.floatField("scaleValueField", value=1, pre=2)
cmds.button('scaleValueButtonMinus', label='<', command='scaleValueButtonMinus_CL()')
cmds.button('scaleValueButtonMinusBit', label='', command='scaleValueButtonMinusBit_CL()')
cmds.button('scaleValueButton', label='', command='scaleValueButton_CL()')
cmds.button('scaleValueButtonPlusBit', label='', command='scaleValueButtonPlusBit_CL()')
cmds.button('scaleValueButtonPlus', label='>', command='scaleValueButtonPlus_CL()')
cmds.setParent('..')

cmds.rowLayout(numberOfColumns=1, columnWidth1=(300), columnAttach=[(1, "both", 0)])
cmds.text(label=sliceText_CL, align="center")
cmds.setParent('..')

# --- Run Script ---

cmds.showWindow()
