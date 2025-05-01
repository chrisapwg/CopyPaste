# Create FKIK Tools
# By Chris Gultom
# How to Use

# ---Reverse FKIK---
# Create the Guides like you want
# Make Sure the value of rig you want to make is add by 1
# Because of script needed
# Just Run It

# ---Switch FKIK---
# Create the Guides like you want
# No need additional value of rig
# Just Run It

# ---Squash---
# Just work with 2 Guide
# First be top, last be bot
# Just Run It

#import pymel.core as pm
import maya.cmds as cmds

windowName_GT = 'guideTools'
windowTitle_GT = 'Guide Tools'
titleText_GT = 'Guide Tools'
sizeHeight_GT = 530
sizeWidth_GT = 210
holderSize_GT = 10
sliceText_GT = '# ------------------------------------------------------------------ #'

MSH_name = '_ply'
CTL_name = '_ctl'
GRP_name = '_pos'
TRN_name = '_trn'
JNT_name = '_jnt'
LOC_name = '_loc'
PAC_name = '_pac'
SCN_name = '_scn'
CRV_name = '_crv'
IKH_name = '_ikh'
EFF_name = '_eff'
DIS_name = '_dis'
MD_name = '_mdv'
RVS_name = '_rvs'
PMA_name = '_pma'
CON_name = '_con'
PAC_name = '_pac'
SCN_name = '_scn'
C_side = 'M_'
L_side = 'L_'
R_side = 'R_'

###

findNameResult = []
def findName(sel):
    global findNameResult
    i = str(sel)
    iSplit = i.split('_')
    iTotalNumber = len(i)
    iSplitLast = len(iSplit[-1])
    iNumber = iTotalNumber-iSplitLast
    ina = i[:iNumber-1]
    findNameResult = ina

findNameLastResult = []
def findNameLast(sel):
    global findNameLastResult
    i = str(sel)
    iSplit = i.split('_')
    iTotalNumber = len(i)
    iSplitLast = len(iSplit[-1])
    iNumber = iTotalNumber-iSplitLast
    ina = i[iNumber-1:]
    findNameLastResult = ina
    
def importController(nameS, typeS):
    name = '{}{}0{}'.format(nameS, typeS, CTL_name)
    list = cmds.ls('{}{}*{}'.format(nameS, typeS, CTL_name), type='transform')
    
    if not list == []:
        name = '{}{}{}{}'.format(nameS, typeS, len(list), CTL_name)
        
    CTL = cmds.circle(n=name, normalX=0, normalY=0, normalZ=0)
    shapeList = cmds.listRelatives(CTL[0], s=1)
    
    for i in shapeList:
        cmds.delete(i)
    cmds.delete(CTL[0], ch=1)
    
    shapeChange8_CL(CTL[0], 21, 1)
    
    shapeList = cmds.listRelatives(CTL[0], s=1)
    for a in shapeList:
        for i in ['aiRenderCurve', 'aiCurveWidth', 'aiSampleRate', 'aiCurveShaderR', 'aiCurveShaderG', 'aiCurveShaderB']:
            try:
                cmds.setAttr('{}.{}'.format(a, i), l=1, k=0)
            except:
                pass

def importControllerMultiple(nameS, typeS, totalNumberS):
    for a in range(len(totalNumberS)):
        name = '{}{}{}{}'.format(nameS, typeS, a, CTL_name)
        list = cmds.ls('{}{}*{}'.format(nameS, typeS, CTL_name), type='transform')
        
        if not list == []:
            name = '{}{}{}{}'.format(nameS, typeS, len(list), CTL_name)
            
        CTL = cmds.circle(n=name, normalX=0, normalY=0, normalZ=0)
        shapeList = cmds.listRelatives(CTL[0], s=1)
        
        for i in shapeList:
            cmds.delete(i)
        cmds.delete(CTL[0], ch=1)
        
        shapeChange8_CL(CTL[0], 21, 1)
        
        shapeList = cmds.listRelatives(CTL[0], s=1)
        for a in shapeList:
            for i in ['aiRenderCurve', 'aiCurveWidth', 'aiSampleRate', 'aiCurveShaderR', 'aiCurveShaderG', 'aiCurveShaderB']:
                try:
                    cmds.setAttr('{}.{}'.format(a, i), l=1, k=0)
                except:
                    pass

def groupCTL(i):
    createGroup = cmds.group(i, n=i.replace(CTL_name, GRP_name))
    cmds.copyAttr(i, createGroup, v=1)
    cmds.setAttr(i+'.translateX', 0)
    cmds.setAttr(i+'.translateY', 0)
    cmds.setAttr(i+'.translateZ', 0)
    cmds.setAttr(i+'.rotateX', 0)
    cmds.setAttr(i+'.rotateY', 0)
    cmds.setAttr(i+'.rotateZ', 0)
    return createGroup

def groupOffset(i):
    createGroup = cmds.group(i, n=i.replace(CTL_name, 'Offset'+GRP_name))
    cmds.copyAttr(i, createGroup, v=1)
    cmds.setAttr(i+'.translateX', 0)
    cmds.setAttr(i+'.translateY', 0)
    cmds.setAttr(i+'.translateZ', 0)
    cmds.setAttr(i+'.rotateX', 0)
    cmds.setAttr(i+'.rotateY', 0)
    cmds.setAttr(i+'.rotateZ', 0)
    return str(createGroup)

def groupJNT(i):
    createGroup = cmds.group(i, n=i.replace(JNT_name, TRN_name))
    cmds.copyAttr(i, createGroup, v=1)
    cmds.setAttr(i+'.translateX', 0)
    cmds.setAttr(i+'.translateY', 0)
    cmds.setAttr(i+'.translateZ', 0)
    cmds.setAttr(i+'.rotateX', 0)
    cmds.setAttr(i+'.rotateY', 0)
    cmds.setAttr(i+'.rotateZ', 0)
    
def groupOther(sel):
    i = str(sel)
    iSplit = i.split('_')
    iTotalNumber = len(i)
    iSplitLast = len(iSplit[-1])
    iNumber = iTotalNumber-iSplitLast
    iName = i[:iNumber]
    createGroup = cmds.group(i, n=iName+GRP_name)
    cmds.copyAttr(i, createGroup, v=1)
    cmds.setAttr(i+'.translateX', 0)
    cmds.setAttr(i+'.translateY', 0)
    cmds.setAttr(i+'.translateZ', 0)
    cmds.setAttr(i+'.rotateX', 0)
    cmds.setAttr(i+'.rotateY', 0)
    cmds.setAttr(i+'.rotateZ', 0)

def showVisibility(item):
    if "visibility" in cmds.listAttr(item):
        cmds.setAttr(item+'.visibility', l=False, k=True, ch=False)

def parentSystem(object, number):
    for something in range(len(number)):
        if something == 0:
            print ("Ok")
        else:
            cmds.parent(object[something], object[something-1])

def getLocation(base, target):
    PC = cmds.parentConstraint(target, base, mo=False)
    cmds.delete(PC)

def getLocation0(base, target):
    PC = cmds.parentConstraint(target, base, sr={"x", "y", "z"}, mo=False)
    cmds.delete(PC)

def getLocationMultiple(base, target, totalNumber):
    for a in range(len(totalNumber)):
        PC = cmds.parentConstraint(target[a], base[a], mo=False)
        cmds.delete(PC)

def getLocationMultiple0(base, target, totalNumber):
    for a in range(len(totalNumber)):
        PC = cmds.parentConstraint(target[a], base[a], sr={"x", "y", "z"}, mo=False)
        cmds.delete(PC)

def orientJoint(afirstJoint, lastJoint):
    firstJoint = cmds.ls(afirstJoint)
    cmds.joint(firstJoint, e=True, oj="xyz", sao="yup", ch=True, zso=True)
    rPointX = cmds.getAttr(lastJoint+'.rotateX')[0]
    rPointY = cmds.getAttr(lastJoint+'.rotateY')[0]
    rPointZ = cmds.getAttr(lastJoint+'.rotateZ')[0]
    cmds.setAttr(lastJoint+'.jointOrientX', rPointX)
    cmds.setAttr(lastJoint+'.jointOrientY', rPointY)
    cmds.setAttr(lastJoint+'.jointOrientZ', rPointZ)
    cmds.setAttr(lastJoint+'.rotateX', 0)
    cmds.setAttr(lastJoint+'.rotateY', 0)
    cmds.setAttr(lastJoint+'.rotateZ', 0)

def createIKHandle(firstJoint, lastJoint):
    cmds.ikHandle(sj=firstJoint, ee=lastJoint, n=firstJoint.replace(JNT_name, IKH_name))
    effectorSelect = cmds.listRelatives(firstJoint, ad=1, typ="ikEffector")
    effectorSelect = cmds.rename(effectorSelect, lastJoint.replace(JNT_name, EFF_name))

def lockAttribute(object):
    cmds.setAttr(object+".tx", l=1, k=0, ch=0)
    cmds.setAttr(object+".ty", l=1, k=0, ch=0)
    cmds.setAttr(object+".tz", l=1, k=0, ch=0)
    cmds.setAttr(object+".rx", l=1, k=0, ch=0)
    cmds.setAttr(object+".ry", l=1, k=0, ch=0)
    cmds.setAttr(object+".rz", l=1, k=0, ch=0)

def scaleValueButton(sel, vScale):
    selected = cmds.ls(sel)
    for o in cmds.listRelatives(selected, s=1):
        cmds.select(o+'.cv[*]')
        cmds.scale(vScale, vScale, vScale)
    cmds.select(selected)

def changeRotation(sel, rotateTo):
    selected = cmds.ls(sel)
    for o in cmds.listRelatives(selected, s=1):
        cmds.select(o+'.cv[*]')
        if rotateTo == 'X': cmds.rotate(90, 0, 0)
        elif rotateTo == 'Y': cmds.rotate(0, 90, 0)
        elif rotateTo == 'Z': cmds.rotate(0, 0, 90)
    cmds.select(selected)

###

def createGuide():
    nameGuide = cmds.textField("guideNameField", query=True, text=True)
    numberGuide = cmds.intField("guideNumberField", query=True, value=True)
    startFrom = 1
    next = 0
    allGuide = []
    guidesGroup = cmds.group(empty=True, n='{}_GUIDES'.format(nameGuide))
    
    for a in range(numberGuide):
        loc = cmds.spaceLocator(n='{}Fk{}{}'.format(nameGuide, a+startFrom, LOC_name))[0]
        cmds.setAttr(loc+'.translateX', 0)
        cmds.setAttr(loc+'.translateY', 0)
        cmds.setAttr(loc+'.translateZ', a*5)
        cmds.setAttr(loc+'.rotateX', 0)
        cmds.setAttr(loc+'.rotateY', 0)
        cmds.setAttr(loc+'.rotateZ', 0)
        cmds.parent(loc, guidesGroup)
        allGuide.append(loc)
        cmds.setAttr(loc+".displayLocalAxis", 1)
        
    for b in range(len(allGuide)):
        if b == 0:
            print ("Ok")
        else:
            cmds.parent(allGuide[b] , allGuide[b-1])
            
    cmds.select(guidesGroup)

###

def createReverseFKIK_GT():
    selectedGuide = cmds.ls(os=1,ap=1)[0]
    guideSplit = selectedGuide.split("_GUIDES")
    nameGuide = guideSplit[0]
    totalLocator = cmds.listRelatives(selectedGuide, ad=True ,type="transform")
    totalLocator.reverse()
    
    # Create Controller
    
    importControllerMultiple(nameGuide, "fwdFk", totalLocator)
    importControllerMultiple(nameGuide, "rvsFk", totalLocator)
    
    groupFK = cmds.group(empty=True, n=nameGuide+"Fk"+GRP_name)
    listFWD = cmds.ls(nameGuide+"fwdFk*"+CTL_name)
    listRVS = cmds.ls(nameGuide+"rvsFk*"+CTL_name)
    
    cmds.parent(listFWD[0], groupFK)
    parentSystem(listFWD, totalLocator)
    getLocationMultiple(listFWD, totalLocator, totalLocator)
    
    for c in listFWD:
        shapeChange8_CL(c, 13, 1)
        changeRotation(c, 'X')
        groupCTL(c)
    
    listFWD.reverse()
    getLocationMultiple(listRVS, listFWD, totalLocator)
    parentSystem(listRVS, totalLocator)
    
    cmds.parent(listRVS[0], listFWD[0])
    
    for f in listRVS:
        shapeChange8_CL(f, 18, 1)
        changeRotation(f, 'X')
        scaleValueButton(f, 0.7)
        groupCTL(f)
    
    # Create System
    
    listFWD.reverse()
    groupRVS = cmds.ls(nameGuide+"rvsFk*"+GRP_name)
    
    for g in listFWD:
        loc = cmds.spaceLocator(n=g.replace(CTL_name, LOC_name))[0]
        cmds.parent(loc, g)
        cmds.parentConstraint(g, loc, mo=False)
        cmds.delete(cn=True)
    
    for h in groupRVS:
        cn = cmds.createNode("parentConstraint", n=h.replace(GRP_name, PAC_name))
        cmds.parent(cn, h)
    
    alistFWD = cmds.ls(nameGuide+"fwdFk*"+CTL_name)
    alistRVS = cmds.ls(nameGuide+"rvsFk*"+CTL_name)
    alistgroupFWD = cmds.ls(nameGuide+"fwdFk*"+GRP_name)
    alistgroupRVS = cmds.ls(nameGuide+"rvsFk*"+GRP_name)
    alistLOC = cmds.ls(nameGuide+"fwdFk*"+LOC_name)
    alistPAC = cmds.ls(nameGuide+"rvsFk*"+PAC_name)
    alistLOC.reverse()
    alistPAC.reverse()
    
    for i in range(len(alistLOC)):
        cmds.setAttr(alistLOC[i]+'.visibility', 0)
        cmds.connectAttr(alistLOC[i]+".worldInverseMatrix[0]", alistPAC[i]+".constraintParentInverseMatrix")
        cmds.connectAttr(alistLOC[i]+".worldMatrix[0]", alistPAC[i-1]+".target[0].targetParentMatrix")
        cmds.connectAttr(alistPAC[i]+".constraintTranslate", alistgroupRVS[i]+".translate")
        cmds.connectAttr(alistPAC[i]+".constraintRotate", alistgroupRVS[i]+".rotate")
    
    showVisibility(alistFWD[-1])
    shp = cmds.listRelatives(alistFWD[-1], ad=True, type='nurbsCurve')[0]
    cmds.setAttr(shp+".visibility", 0)
    showVisibility(alistRVS[-1])
    shp = cmds.listRelatives(alistRVS[-1], ad=True, type='nurbsCurve')[0]
    cmds.setAttr(shp+".visibility", 0)
    
    # Create IK
    
    importControllerMultiple(nameGuide, "Ik", totalLocator)
    
    alistIK = cmds.ls(nameGuide+"Ik*"+CTL_name)
    print(alistIK, alistLOC, totalLocator)
    getLocationMultiple(alistIK, alistLOC, totalLocator)
    print("b")
    groupIK = cmds.group(empty=True, n=nameGuide+"Ik"+GRP_name)
    
    for m in alistIK:
        shapeChange8_CL(m, 21, 1)
        changeRotation(m, 'X')
        scaleValueButton(m, 0.4)
        cmds.parent(m, groupIK)
        jnt = cmds.joint(m, n=m.replace(CTL_name, JNT_name))
        cmds.setAttr(jnt+'.visibility', 0)
        groupCTL(m)
    
    alistGroup = cmds.ls(nameGuide+"Ik*"+GRP_name)
    
    for n in range(len(alistLOC)):
        cmds.parentConstraint(alistRVS[n], alistGroup[n+1], n=alistGroup[n].replace(GRP_name, PAC_name), mo=True)
    
    alistPAC = cmds.ls(nameGuide+"Ik*"+PAC_name)
    
    ###
    
    mainGRP = cmds.group(empty=True, n=nameGuide+'ReverseMain'+GRP_name)
    
    cmds.parent(groupFK, mainGRP)
    cmds.parent(groupIK, mainGRP)
    cmds.delete(alistGroup[0])
    cmds.delete(alistPAC[-1])
    cmds.select(d=True)
    cmds.setAttr(selectedGuide+'.visibility', 0)
    
    cmds.rename(alistFWD[-1], nameGuide+"fwdFkEND"+CTL_name)
    cmds.rename(alistgroupFWD[-1], nameGuide+"fwdFkEND"+GRP_name)
    cmds.rename(alistLOC[0], nameGuide+"fwdFkEND"+LOC_name)
    cmds.rename(alistRVS[-1], nameGuide+"rvsFkEND"+CTL_name)
    cmds.rename(alistgroupRVS[-1], nameGuide+"rvsFkEND"+GRP_name)
    cmds.rename(alistPAC[0], nameGuide+"fwdFkEND"+PAC_name)
    
    ### Adding Offset Group
    
    #for a in listFWD:
    #    groupOffset(a)
    #
    #for b in listRVS:
    #    groupOffset(b)

def createReverseFKIKInfo_GT():
    print ('')
    print ('--- Create Reverse FKIK ---')
    print ('')
    print ('Function: Create Double Direction CTRL')
    print ('How to Use:')
    print ('    -Please Tools [Control Library]')
    print ('    -Please Create Guide')
    print ("    -Last Guide Doesn't Count")
    print ('    -Run the System')

###

def createSwitchFKIK_GT():
    selectedGuide = cmds.ls(os=1,ap=1)[0]
    guideSplit = selectedGuide.split("_GUIDES")
    nameGuide = guideSplit[0]
    totalLocator = cmds.listRelatives(selectedGuide, ad=True, f=True, type="transform")
    totalLocator.reverse()
    c = 0
    
    # Create Joint
    
    for a in totalLocator:
        cmds.select(a)
        popon = cmds.joint(n="{}Skin{}{}".format(nameGuide, str(c), JNT_name))
        cmds.setAttr(popon+".displayLocalAxis", 1)
        cmds.joint(n="{}Fk{}{}".format(nameGuide, str(c), JNT_name))
        cmds.joint(n="{}Ik{}{}".format(nameGuide, str(c), JNT_name))
        c += 1
    
    jointSkin = cmds.ls(nameGuide+"Skin*"+JNT_name)
    jointFk = cmds.ls(nameGuide+"Fk*"+JNT_name)
    jointIk = cmds.ls(nameGuide+"Ik*"+JNT_name)
    
    cmds.parent(jointSkin[0], world=True)
    cmds.parent(jointFk[0], world=True)
    cmds.parent(jointIk[0], world=True)
    
    parentSystem(jointSkin, totalLocator)
    parentSystem(jointFk, totalLocator)
    parentSystem(jointIk, totalLocator)
    
    jointSkinChild = cmds.listRelatives(jointSkin, ad=True)
    jointFkChild = cmds.listRelatives(jointFk, ad=True)
    jointIkChild = cmds.listRelatives(jointIk, ad=True)
    
    orientJoint(jointSkin[0], jointSkinChild[0])
    orientJoint(jointFk[0], jointFkChild[0])
    orientJoint(jointIk[0], jointIkChild[0])
    
    # Create IK
    
    createIKHandle(jointIk[0], jointIkChild[0])
    
    ikHandleSelect = cmds.ls("{}Ik0{}".format(nameGuide, IKH_name))
    
    importController(nameGuide, "FirstIk")
    importController(nameGuide, "AIMIk")
    importController(nameGuide, "LastIk")
    
    CTLFirstIk = cmds.ls(nameGuide+"FirstIk0"+CTL_name)
    CTLAIMIk = cmds.ls(nameGuide+"AIMIk0"+CTL_name)
    CTLLastIk = cmds.ls(nameGuide+"LastIk0"+CTL_name)
    
    shapeChange8_CL(CTLFirstIk[0], 18, 1)
    shapeChange8_CL(CTLAIMIk[0], 18, 1)
    shapeChange8_CL(CTLLastIk[0], 18, 1)
    
    changeRotation(CTLFirstIk[0], 'X')
    changeRotation(CTLAIMIk[0], 'X')
    changeRotation(CTLLastIk[0], 'X')
    
    getLocation0(CTLFirstIk[0], jointIk[0])
    getLocation0(CTLAIMIk[0], jointIk[1])
    getLocation0(CTLLastIk[0], jointIkChild[0])
    
    cmds.parentConstraint(CTLFirstIk[0], jointIk[0], n=jointIk[0].replace(JNT_name, PAC_name), mo=True)
    cmds.parentConstraint(CTLLastIk[0], ikHandleSelect[0], n=ikHandleSelect[0].replace(IKH_name, PAC_name), mo=True)
    
    groupJNT(jointSkin[0])
    groupJNT(jointIk[0])
    groupJNT(jointFk[0])
    
    # Create Fk
    
    importControllerMultiple(nameGuide, "Fk", totalLocator)
    
    CTLFk = cmds.ls(nameGuide+"Fk*"+CTL_name)
    
    getLocationMultiple0(CTLFk, jointFk, totalLocator)
    parentSystem(CTLFk, totalLocator)
    
    for d in range(len(totalLocator)):
        shapeChange8_CL(CTLFk[d], 20, 1)
        changeRotation(CTLFk[d], 'X')
        cmds.parentConstraint(CTLFk[d], jointFk[d], n=jointFk[d].replace(JNT_name, PAC_name), mo=True)
    
    # Create System
    
    importController(nameGuide, "Switch")
    
    CTLSwitch = cmds.ls(nameGuide+"Switch0"+CTL_name)
    
    getLocation0(CTLSwitch[0], jointSkin[0])
    
    cmds.addAttr(CTLSwitch[0], ln="Switch_FKIK", keyable=True, at="double", min=0, max=1, dv=1)
    cmds.addAttr(CTLSwitch[0], ln="Ik_Squash_Stretch", keyable=True, at="double", min=0, max=1, dv=1)
    cmds.addAttr(CTLSwitch[0], ln="Ik_Distance", keyable=True, at="double", dv=0)
    shapeChange7_CL(CTLSwitch[0], 17, 1)
    changeRotation(CTLSwitch[0], 'X')
    scaleValueButton(CTLSwitch[0], 1.5)
    
    for e in range(len(totalLocator)):
        blendTranslate = cmds.createNode("blendColors", n=nameGuide+str(e+1)+"Translate_blend")
        cmds.connectAttr(jointFk[e]+".t", blendTranslate+".color2.")
        cmds.connectAttr(jointIk[e]+".t", blendTranslate+".color1.")
        
        blendRotate = cmds.createNode("blendColors", n=nameGuide+str(e+1)+"Rotate_blend")
        cmds.connectAttr(jointFk[e]+".r", blendRotate+".color2.")
        cmds.connectAttr(jointIk[e]+".r", blendRotate+".color1.")
        
        blendScale = cmds.createNode("blendColors", n=nameGuide+str(e+1)+"Scale_blend")
        cmds.connectAttr(jointFk[e]+".s", blendScale+".color2.")
        cmds.connectAttr(jointIk[e]+".s", blendScale+".color1.")
        
        cmds.connectAttr(blendTranslate+".output", jointSkin[e]+".t.")
        cmds.connectAttr(blendRotate+".output", jointSkin[e]+".r.")
        cmds.connectAttr(blendScale+".output", jointSkin[e]+".s.")
        
        cmds.connectAttr(CTLSwitch[0]+".Switch_FKIK", blendTranslate+".blender.")
        cmds.connectAttr(CTLSwitch[0]+".Switch_FKIK", blendRotate+".blender.")
        cmds.connectAttr(CTLSwitch[0]+".Switch_FKIK", blendScale+".blender.")
    
    groupJoint = cmds.group(empty=True , n=nameGuide+"Switch"+TRN_name)
    groupFk = cmds.group(empty=True, n=nameGuide+"Fk"+GRP_name)
    groupIk = cmds.group(empty=True, n=nameGuide+"Ik"+GRP_name)
    groupMisc = cmds.group(empty=True, n=nameGuide+"Misc"+TRN_name)
    groupCTL(CTLSwitch[0])
    groupSwitch = cmds.ls(nameGuide+"Switch0"+GRP_name)
    
    startLOC = cmds.spaceLocator(n=nameGuide+"IkStartDistance"+LOC_name)[0]
    endLOC = cmds.spaceLocator(n=nameGuide+"IkEndDistance"+LOC_name)[0]
    getLocation0(startLOC, jointFk[0])
    getLocation0(endLOC, jointFkChild[0])
    startLOCPoint = cmds.getAttr(startLOC+".t")[0]
    endLOCPoint = cmds.getAttr(endLOC+".t")[0]
    nodeDistance = cmds.distanceDimension(sp=(startLOCPoint), ep=(endLOCPoint))
    nodeDistanceParent = cmds.listRelatives(nodeDistance, p=1)
    cmds.parentConstraint(CTLFirstIk[0], startLOC, n=startLOC.replace(LOC_name, PAC_name), mo=True)
    cmds.parentConstraint(CTLLastIk[0], endLOC, n=endLOC.replace(LOC_name, PAC_name), mo=True)
    
    distanceStartPAC = cmds.ls(nameGuide+"IkStartDistance"+PAC_name)
    distanceEndPAC = cmds.ls(nameGuide+"IkEndDistance"+PAC_name)
    nodeFreeze = cmds.createNode("multiplyDivide", n=nameGuide+"Freeze"+MD_name)
    nodeReverse = cmds.createNode("reverse", n=nameGuide+"Reverse"+RVS_name)
    nodeAverage = cmds.createNode("plusMinusAverage", n=nameGuide+"Average_AVG")
    nodeScale = cmds.createNode("multiplyDivide", n=nameGuide+"Scale"+MD_name)
    cmds.setAttr(nodeScale+".operation", 2)
    nodeCondition = cmds.createNode("condition", n=nameGuide+"Condition"+CON_name)
    cmds.setAttr(nodeCondition+".operation", 2)
    
    #for f in range(len(totalLocator)):
    #    cmds.connectAttr(nodeCondition+".outColor.outColorR", jointIk[f]+".scale.scaleX.")
    
    totalDistance = -1
    rangeTotal = range(len(jointIk))
    rangeLast = rangeTotal[-1]
    
    for a in range(len(jointIk)):
        b = a
        c = a+1
        if b == rangeLast:
            pass
        else:
            loc1 = cmds.spaceLocator()[0]
            loc2 = cmds.spaceLocator()[0]
            getLocation(loc1, jointIk[b])
            getLocation(loc2, jointIk[c])
            loc1Point = cmds.getAttr(loc1+".t")[0]
            loc2Point = cmds.getAttr(loc2+".t")[0]
            distance = cmds.distanceDimension(sp=(loc1Point), ep=(loc2Point))
            distanceRange = cmds.getAttr(distance+".distance")[0]
            totalDistance = totalDistance+distanceRange
            cmds.delete(loc1)
            cmds.delete(loc2)
    
    cmds.setAttr(nodeAverage+".input1D[0]", totalDistance)
    cmds.connectAttr(CTLSwitch[0]+".Ik_Distance", nodeReverse+".input.inputX.")
    cmds.connectAttr(nodeReverse+".output.outputX", nodeAverage+".input1D[1].")
    cmds.connectAttr(nodeAverage+".output1D", nodeFreeze+".input2.input2X.")
    cmds.connectAttr(groupSwitch[0]+".scale.scaleX", nodeFreeze+".input1.input1X.")
    cmds.connectAttr(nodeFreeze+".output.outputX", nodeScale+".input2.input2X.")
    cmds.connectAttr(nodeFreeze+".output.outputX", nodeCondition+".secondTerm.")
    cmds.connectAttr(nodeDistance+".distance", nodeScale+".input1.input1X.")
    cmds.connectAttr(nodeDistance+".distance", nodeCondition+".firstTerm.")
    #cmds.connectAttr(nodeScale+".output.outputX", nodeCondition+".colorIfTrue.colorIfTrueR.")
    
    for f in range(len(totalLocator)):
        cmds.connectAttr(nodeScale+".output.outputX", jointIk[f]+".scale.scaleX.")
    
    jointSkinGroup = cmds.ls(nameGuide+"Skin*"+TRN_name)
    jointFkGroup = cmds.ls(nameGuide+"Fk*"+TRN_name)
    jointIkGroup = cmds.ls(nameGuide+"Ik*"+TRN_name)
    
    cmds.setDrivenKeyframe(groupFk+".visibility", cd=CTLSwitch[0]+".Switch_FKIK", dv=0, v=1)
    cmds.setDrivenKeyframe(groupFk+".visibility", cd=CTLSwitch[0]+".Switch_FKIK", dv=1, v=0)
    cmds.setDrivenKeyframe(groupIk+".visibility", cd=CTLSwitch[0]+".Switch_FKIK", dv=0, v=0)
    cmds.setDrivenKeyframe(groupIk+".visibility", cd=CTLSwitch[0]+".Switch_FKIK", dv=1, v=1)
    cmds.setDrivenKeyframe(jointFkGroup[0]+".visibility", cd=CTLSwitch[0]+".Switch_FKIK", dv=0, v=1)
    cmds.setDrivenKeyframe(jointFkGroup[0]+".visibility", cd=CTLSwitch[0]+".Switch_FKIK", dv=1, v=0)
    cmds.setDrivenKeyframe(jointIkGroup[0]+".visibility", cd=CTLSwitch[0]+".Switch_FKIK", dv=0, v=0)
    cmds.setDrivenKeyframe(jointIkGroup[0]+".visibility", cd=CTLSwitch[0]+".Switch_FKIK", dv=1, v=1)
    
    cmds.connectAttr(CTLSwitch[0]+".Ik_Squash_Stretch", distanceStartPAC[0]+"."+nameGuide+"FirstIk0"+CTL_name+"W0.")
    cmds.connectAttr(CTLSwitch[0]+".Ik_Squash_Stretch", distanceEndPAC[0]+"."+nameGuide+"LastIk0"+CTL_name+"W0.")
    
    # Clean Up
    
    groupMain = cmds.group(empty=True, n=nameGuide+'SwitchFKIKMain'+GRP_name)
    
    cmds.parent(jointSkinGroup[0], groupJoint)
    cmds.parent(jointFkGroup[0], groupJoint)
    cmds.parent(jointIkGroup[0], groupJoint)
    cmds.parent(ikHandleSelect[0], groupMisc)
    cmds.parent(CTLFk[0], groupFk)
    cmds.parent(CTLFirstIk[0], groupIk)
    cmds.parent(CTLLastIk[0], groupIk)
    cmds.parent(groupFk, CTLSwitch[0])
    cmds.parent(groupIk, CTLSwitch[0])
    cmds.parent(nodeDistanceParent, groupMisc)
    cmds.parent(startLOC, groupMisc)
    cmds.parent(endLOC, groupMisc)
    cmds.parent(groupMisc, groupJoint)
    cmds.parent(groupJoint, groupMain)
    cmds.parent(groupSwitch, groupMain)
    
    groupCTL(CTLFirstIk[0])
    groupCTL(CTLLastIk[0])
    
    for f in range(len(totalLocator)):
        groupCTL(CTLFk[f])
    
    lockAttribute(CTLSwitch[0])
    cmds.setAttr(groupJoint+".visibility", 0)
    cmds.setAttr(groupMisc+".visibility", 0)
    getLocation(jointIkGroup, CTLSwitch[0])
    getLocation(groupMisc, groupSwitch[0])
    
    cmds.scaleConstraint(groupSwitch[0], groupJoint, n=groupJoint.replace(TRN_name, SCN_name))
    cmds.select(d=True)
    cmds.setAttr(selectedGuide+'.visibility', 0)
    
    ###
    
    cmds.parent(CTLAIMIk[0], groupIk)
    aimGRPName = groupCTL(CTLAIMIk[0])
    cmds.setDrivenKeyframe(aimGRPName+".visibility", cd=CTLSwitch[0]+".Switch_FKIK", dv=0, v=0)
    cmds.setDrivenKeyframe(aimGRPName+".visibility", cd=CTLSwitch[0]+".Switch_FKIK", dv=1, v=1)
    cmds.rename(nodeDistanceParent, nameGuide+"Distance"+DIS_name)

def createSwitchFKIKInfo_GT():
    print ('')
    print ('--- Create Switch FKIK ---')
    print ('')
    print ('Function: Create Basic FKIK CTRL')
    print ('How to Use:')
    print ('    -Please Tools [Control Library]')
    print ('    -Please Create Guide')
    print ('    -Run the System')

###

def createSwitchSpline_GT():
    global ctrlSwitch
    selectedGuide = cmds.ls(os=1,ap=1)[0]
    guideSplit = selectedGuide.split("_GUIDES")
    nameGuide = guideSplit[0]
    totalLocator = cmds.listRelatives(selectedGuide, ad=True, f=True ,type="transform")
    totalLocator.reverse()
    c = 0
    
    # Create Joint
    
    for a in totalLocator:
        cmds.select(a)
        popon = cmds.joint(n="{}Skin{}{}".format(nameGuide, str(c), JNT_name))
        cmds.setAttr(popon+".displayLocalAxis", 1)
        cmds.select(a)
        cmds.joint(n="{}IK{}{}".format(nameGuide, str(c), JNT_name))
        cmds.select(a)
        cmds.joint(n="{}FK{}{}".format(nameGuide, str(c), JNT_name))
        c += 1
    
    jointSkin = cmds.ls(nameGuide+"Skin*"+JNT_name)
    jointIK = cmds.ls(nameGuide+"IK*"+JNT_name)
    jointFK = cmds.ls(nameGuide+"FK*"+JNT_name)
    
    cmds.parent(jointSkin[0], world=True)
    cmds.parent(jointIK[0], world=True)
    cmds.parent(jointFK[0], world=True)
    
    parentSystem(jointSkin, totalLocator)
    parentSystem(jointIK, totalLocator)
    parentSystem(jointFK, totalLocator)
    
    jointSkinChild = cmds.listRelatives(jointSkin, ad=True)
    jointIKChild = cmds.listRelatives(jointIK, ad=True)
    jointFKChild = cmds.listRelatives(jointFK, ad=True)
    
    orientJoint(jointSkin[0], jointSkinChild[0])
    orientJoint(jointIK[0], jointIKChild[0])
    orientJoint(jointFK[0], jointFKChild[0])
    
    curvePosition = []
    
    for b in totalLocator:
        locTemp = cmds.spaceLocator(n='C_locTemp'+LOC_name)[0]
        cmds.delete(cmds.pointConstraint(b, locTemp, mo=False))
        locPosition = cmds.getAttr(locTemp+'.t')[0]
        curvePosition.append(locPosition)
        cmds.delete(locTemp)
    
    curveIK = cmds.curve(p=curvePosition, n="{}IK_CRV".format(nameGuide))
    
    cmds.select(jointIK[0], jointIKChild[0], curveIK)
    ikHandleIK = cmds.ikHandle(sol='ikSplineSolver', ccv=False, n="{}IK{}".format(nameGuide, IKH_name))
    ikHandleIK[1] = cmds.rename(ikHandleIK[1], "{}IK{}".format(nameGuide, EFF_name))
    
    #
    
    importController(nameGuide, 'Switch')
    
    for c in totalLocator:
        importController(nameGuide, 'FK')
        importController(nameGuide, 'IK')
        importController(nameGuide, 'Part')
    
    cmds.select(totalLocator[0])
    ctrlSwitch = cmds.ls(nameGuide+'Switch*'+CTL_name)[0]
    ctrlFK = cmds.ls(nameGuide+'FK*'+CTL_name)
    ctrlIK = cmds.ls(nameGuide+'IK*'+CTL_name)
    ctrlPart = cmds.ls(nameGuide+'Part*'+CTL_name)
    
    cmds.select(ctrlSwitch)
    getLocation(ctrlSwitch, totalLocator[0])
    changeColorYellow_CL()
    shapeChange7_CL(ctrlSwitch, 17, 1)
    changeRotation(ctrlSwitch, 'X')
    scaleValueButton(ctrlSwitch, 1.5)
    
    for d in range(len(totalLocator)):
        cmds.select(ctrlFK[d])
        changeColorCherry_CL()
        getLocation(ctrlFK[d], totalLocator[d])
        changeRotation(ctrlFK[d], 'X')
        
        cmds.select(ctrlIK[d])
        changeColorBlueSea_CL()
        getLocation(ctrlIK[d], totalLocator[d])
        changeRotation(ctrlIK[d], 'X')
        
        cmds.select(ctrlPart[d])
        changeColorOrange_CL()
        getLocation(ctrlPart[d], totalLocator[d])
        shapeChange19_CL(ctrlPart[d], 21, 1)
        changeRotation(ctrlPart[d], 'Z')
    
    ###
    
    groupMain = cmds.group(empty=True, n=nameGuide+'SplineFKIKMain'+GRP_name)
    groupTRN = cmds.group(empty=True, n=nameGuide+TRN_name)
    groupRIG = cmds.group(empty=True, n=nameGuide+GRP_name)
    groupMisc = cmds.group(empty=True, n=nameGuide+'Misc'+TRN_name)
    groupFK = cmds.group(empty=True, n=nameGuide+'FK'+GRP_name)
    groupIK = cmds.group(empty=True, n=nameGuide+'IK'+GRP_name)
    groupPart = cmds.group(empty=True, n=nameGuide+'Part'+GRP_name)
    groupTRNSkin = cmds.group(empty=True, n=nameGuide+'Skin'+TRN_name)
    groupTRNFK = cmds.group(empty=True, n=nameGuide+'FK'+TRN_name)
    groupTRNIK = cmds.group(empty=True, n=nameGuide+'IK'+TRN_name)
    
    cmds.parent(jointSkin[0], groupTRNSkin)
    cmds.parent(jointFK[0], groupTRNFK)
    cmds.parent(jointIK[0], groupTRNIK)
    cmds.parent(groupTRNSkin, groupTRN)
    cmds.parent(groupTRNFK, groupTRN)
    cmds.parent(groupTRNIK, groupTRN)
    cmds.parent(curveIK, groupMisc)
    cmds.parent(ikHandleIK[0], groupMisc)
    cmds.parent(groupMisc, groupTRN)
    cmds.parent(ctrlSwitch, groupRIG)
    cmds.parent(ctrlFK, groupFK)
    cmds.parent(ctrlIK, groupIK)
    cmds.parent(ctrlPart, groupPart)
    cmds.parent(groupFK, ctrlSwitch)
    cmds.parent(groupIK, ctrlSwitch)
    cmds.parent(groupPart, ctrlSwitch)
    cmds.parent(groupTRN, groupMain)
    cmds.parent(groupRIG, groupMain)
    cmds.setAttr(groupTRN+'.visibility', 0)
    
    parentSystem(ctrlFK, totalLocator)
    parentSystem(ctrlIK, totalLocator)
    groupCTL(ctrlSwitch)
    
    for e in range(len(totalLocator)):
        groupCTL(ctrlFK[e])
        groupCTL(ctrlIK[e])
        groupCTL(ctrlPart[e])
    
    #
    
    cmds.addAttr(ctrlSwitch, ln="FKIK_Attr", keyable=True, at="enum", en='---:')
    cmds.addAttr(ctrlSwitch, ln="Switch_FKIK", keyable=True, at="double", min=0, max=1, dv=1)
    cmds.addAttr(ctrlSwitch, ln="IK_Stretch", keyable=True, at="double", min=0, max=1, dv=0)
    
    # special
    cmds.addAttr(ctrlSwitch, ln="ShowFK", keyable=True, at="double", min=0, max=1, dv=0)
    cmds.addAttr(ctrlSwitch, ln="ShowIK", keyable=True, at="double", min=0, max=1, dv=0)
    cmds.addAttr(ctrlSwitch, ln="Show_Part", keyable=True, at="double", min=0, max=1, dv=0)
    
    cmds.addAttr(ctrlSwitch, ln="Wave_Attr", keyable=True, at="enum", en='---:')
    cmds.addAttr(ctrlSwitch, ln="Wave_Enable", keyable=True, at="double", min=0, max=1, dv=1)
    cmds.addAttr(ctrlSwitch, ln="Wave_Amplitude", keyable=True, at="double", min=-5, max=5, dv=0)
    cmds.addAttr(ctrlSwitch, ln="Wave_Length", keyable=True, at="double", min=0.1, max=10, dv=2)
    cmds.addAttr(ctrlSwitch, ln="Wave_Offset", keyable=True, at="double", dv=0)
    cmds.addAttr(ctrlSwitch, ln="Wave_Dropoff", keyable=True, at="double", min=-1, max=1, dv=-1)
    cmds.addAttr(ctrlSwitch, ln="Wave_Low_Bound", keyable=True, at="double", min=-10, max=0, dv=0)
    cmds.addAttr(ctrlSwitch, ln="Wave_High_Bound", keyable=True, at="double", min=0, max=10, dv=2)
    cmds.addAttr(ctrlSwitch, ln="Show_Deformer", keyable=True, at="double", min=0, max=1, dv=0)
    #cmds.addAttr(ctrlSwitch, ln="Wave_Ratation_X", keyable=True, at="double", dv=0)
    #cmds.addAttr(ctrlSwitch, ln="Wave_Ratation_Y", keyable=True, at="double", dv=0)
    #cmds.addAttr(ctrlSwitch, ln="Wave_Ratation_Z", keyable=True, at="double", dv=0)
    
    cmds.setAttr(ctrlSwitch + '.FKIK_Attr', lock=True)
    cmds.setAttr(ctrlSwitch + '.Wave_Attr', lock=True)
    
    for e in range(len(totalLocator)):
        blendTranslate = cmds.createNode("blendColors", n=nameGuide+str(e+1)+"Translate_blend")
        cmds.connectAttr(jointFK[e]+".t", blendTranslate+".color2.")
        cmds.connectAttr(jointIK[e]+".t", blendTranslate+".color1.")
        
        blendRotate = cmds.createNode("blendColors", n=nameGuide+str(e+1)+"Rotate_blend")
        cmds.connectAttr(jointFK[e]+".r", blendRotate+".color2.")
        cmds.connectAttr(jointIK[e]+".r", blendRotate+".color1.")
        
        blendScale = cmds.createNode("blendColors", n=nameGuide+str(e+1)+"Scale_blend")
        cmds.connectAttr(jointFK[e]+".s", blendScale+".color2.")
        cmds.connectAttr(jointIK[e]+".s", blendScale+".color1.")
        
        cmds.connectAttr(blendTranslate+".output", jointSkin[e]+".t.")
        cmds.connectAttr(blendRotate+".output", jointSkin[e]+".r.")
        cmds.connectAttr(blendScale+".output", jointSkin[e]+".s.")
        
        cmds.connectAttr(ctrlSwitch+".Switch_FKIK", blendTranslate+".blender.")
        cmds.connectAttr(ctrlSwitch+".Switch_FKIK", blendRotate+".blender.")
        cmds.connectAttr(ctrlSwitch+".Switch_FKIK", blendScale+".blender.")
    
    cmds.setDrivenKeyframe(groupFK+".visibility", cd=ctrlSwitch+".Switch_FKIK", dv=0, v=1)
    cmds.setDrivenKeyframe(groupFK+".visibility", cd=ctrlSwitch+".Switch_FKIK", dv=1, v=0)
    cmds.setDrivenKeyframe(groupIK+".visibility", cd=ctrlSwitch+".Switch_FKIK", dv=0, v=0)
    cmds.setDrivenKeyframe(groupIK+".visibility", cd=ctrlSwitch+".Switch_FKIK", dv=1, v=1)
    cmds.setDrivenKeyframe(groupTRNFK+".visibility", cd=ctrlSwitch+".Switch_FKIK", dv=0, v=1)
    cmds.setDrivenKeyframe(groupTRNFK+".visibility", cd=ctrlSwitch+".Switch_FKIK", dv=1, v=0)
    cmds.setDrivenKeyframe(groupTRNIK+".visibility", cd=ctrlSwitch+".Switch_FKIK", dv=0, v=0)
    cmds.setDrivenKeyframe(groupTRNIK+".visibility", cd=ctrlSwitch+".Switch_FKIK", dv=1, v=1)
    cmds.setDrivenKeyframe(groupPart+".visibility", cd=ctrlSwitch+".Switch_FKIK", dv=0, v=0)
    cmds.setDrivenKeyframe(groupPart+".visibility", cd=ctrlSwitch+".Switch_FKIK", dv=1, v=1)
    
    jntPart = []
    
    for f in range(len(totalLocator)):
        cmds.select(ctrlPart[f])
        jnt = cmds.joint(n=ctrlPart[f].replace(CTL_name, JNT_name))
        jntPart.append(str(jnt))
        cmds.setAttr(jnt+'.visibility', 0)
        
        cmds.parentConstraint(ctrlIK[f], ctrlPart[f].replace(CTL_name, GRP_name), n=ctrlPart[f].replace(CTL_name, 'TRN_PAC'), mo=True)
        cmds.scaleConstraint(ctrlIK[f], ctrlPart[f].replace(CTL_name, GRP_name), n=ctrlPart[f].replace(CTL_name, 'TRN_SCN'), mo=True)
        
        cmds.parentConstraint(ctrlFK[f], jointFK[f], n=jointFK[f].replace(JNT_name, 'TRN_PAC'), mo=True)
        cmds.scaleConstraint(ctrlFK[f], jointFK[f], n=jointFK[f].replace(JNT_name, 'TRN_SCN'), mo=True)
        
        #cmds.scaleConstraint(ctrlPart[f], jointIK[f], n=jointIK[f].replace(JNT_name, 'TRN_SCN'), mo=True)
    
    # --- IK Stretch
    
    curveIKShape = cmds.listRelatives(curveIK, ad=True, type='shape')[0]
    curveIK_info = cmds.createNode("curveInfo", n="{}IK_Info".format(nameGuide))
    curveMD = cmds.createNode("multiplyDivide", n="{}Curve_MD".format(nameGuide))
    curveCond = cmds.createNode("condition", n="{}Cond_MD".format(nameGuide))
    
    cmds.connectAttr(curveIKShape+".worldSpace[0]", curveIK_info+".inputCurve")
    cmds.connectAttr(curveIK_info+".arcLength", curveMD+".input1X")
    cmds.connectAttr(curveMD+".output.outputX", curveCond+".colorIfTrue.colorIfTrueR.")
    cmds.connectAttr(ctrlSwitch+".IK_Stretch", curveCond+".firstTerm.")
    
    for g in range(len(totalLocator)):
        cmds.connectAttr(curveCond+".outColor.outColorR", jointIK[g]+".scaleX")
    
    cmds.setAttr(curveMD+".operation", 2)
    cmds.setAttr(curveMD+".input2X", cmds.getAttr(curveIK_info+".arcLength") + 0)
    cmds.setAttr(curveCond+".secondTerm", 1)
    cmds.setAttr(curveCond+".colorIfFalseR", 1)
    
    # --- IK Stretch
    
    cmds.skinCluster(curveIK, jntPart, tsb=True, maximumInfluences=1, dropoffRate=1)
    cmds.select(curveIK)
    sineAttr = cmds.nonLinear(type='sine')
    sineGRP = cmds.group(sineAttr[1], n=nameGuide+'Sine'+TRN_name, p=groupMisc)
    cmds.setAttr(sineAttr[1]+'.overrideEnabled', 1)
    #cmds.setAttr(sineAttr[1]+'.overrideDisplayType', 2)
    cmds.setAttr(sineAttr[1]+'.translateX', 0)
    cmds.setAttr(sineAttr[1]+'.translateY', 0)
    cmds.setAttr(sineAttr[1]+'.translateZ', 0)
    cmds.setAttr(sineAttr[1]+'.rotateX', 90)
    cmds.setAttr(sineAttr[1]+'.rotateY', 0)
    cmds.setAttr(sineAttr[1]+'.rotateZ', 0)
    cmds.parent(sineGRP, ctrlSwitch)
    cmds.connectAttr(ctrlSwitch+".Wave_Enable", sineAttr[0]+".envelope")
    cmds.connectAttr(ctrlSwitch+".Wave_Amplitude", sineAttr[0]+".amplitude")
    cmds.connectAttr(ctrlSwitch+".Wave_Length", sineAttr[0]+".wavelength")
    cmds.connectAttr(ctrlSwitch+".Wave_Offset", sineAttr[0]+".offset")
    cmds.connectAttr(ctrlSwitch+".Wave_Dropoff", sineAttr[0]+".dropoff")
    cmds.connectAttr(ctrlSwitch+".Wave_Low_Bound", sineAttr[0]+".lowBound")
    cmds.connectAttr(ctrlSwitch+".Wave_High_Bound", sineAttr[0]+".highBound")
    cmds.connectAttr(ctrlSwitch+".Show_Deformer", sineGRP+".visibility")
    #cmds.connectAttr(ctrlSwitch+".Wave_Ratation_X", sineAttr[1]+".rotateX")
    #cmds.connectAttr(ctrlSwitch+".Wave_Ratation_Y", sineAttr[1]+".rotateY")
    #cmds.connectAttr(ctrlSwitch+".Wave_Ratation_Z", sineAttr[1]+".rotateZ")
    #cmds.parentConstraint(ctrlSwitch, sineGRP, n=sineGRP.replace(TRN_name, 'TRN_PAC'), mo=True)
    #cmds.scaleConstraint(ctrlSwitch, sineGRP, n=sineGRP.replace(TRN_name, 'TRN_SCN'), mo=True)
    
    sineAttr[1] = cmds.rename(sineAttr[1], nameGuide+'_SNH')
    sineAttr[0] = cmds.rename(sineAttr[0], nameGuide+'_Sine')
    
    cmds.setAttr(selectedGuide+'.visibility')
    cmds.select(ctrlSwitch)
    
    # Extra Offset Group
    for o in range(len(totalLocator)):
        groupOffset(ctrlPart[o])

def createSwitchSplineInfo_GT():
    print ('')
    print ('--- Create Reverse FKIK ---')
    print ('')
    print ('Function: Create Double Direction CTRL')
    print ('How to Use:')
    print ('    -Please Tools [Control Library]')
    print ('    -Please Create Guide')
    print ("    -Last Guide Doesn't Count")
    print ('    -Run the System')

###

def squashObjectNameLoad_GT():
    selected = cmds.ls(os=True)[0]
    cmds.textField('squashObjectNameText', e=True, text=str(selected))

def createSquash_GT():
    selectedGuide = cmds.ls(os=1, ap=1)
    guideSplit = selectedGuide[0].split("_GUIDES")
    nameGuide = guideSplit[0]
    totalLocator = cmds.listRelatives(selectedGuide[0], ad=True, type="transform")
    totalLocator.reverse()
    childLocator = cmds.listRelatives(selectedGuide[0], ad=True, type="transform")
    childLocator.reverse()
    childLocator.remove(childLocator[0])
    childLocator.remove(childLocator[-1])
    selectedObject = cmds.textField('squashObjectNameText', q=True, text=True)
    numberControl = len(totalLocator)
    
    # Create Controller
    
    importController(nameGuide, "Top")
    importController(nameGuide, "Bot")
    importController(nameGuide, "BaseRotation")
    importController(nameGuide, "DeformRotation")
    importController(nameGuide, "Root")
    
    topCTL = cmds.ls(nameGuide+"Top0"+CTL_name)
    botCTL = cmds.ls(nameGuide+"Bot0"+CTL_name)
    baseCTL = cmds.ls(nameGuide+"BaseRotation0"+CTL_name)
    deformCTL = cmds.ls(nameGuide+"DeformRotation0"+CTL_name)
    rootCTL = cmds.ls(nameGuide+"Root0"+CTL_name)
    
    newCTL = []
    
    if childLocator != []:
        for o in range(len(childLocator)):
            importController(nameGuide, "IK")
            newCTL.append("{}IK{}{}".format(nameGuide, o, CTL_name))
    else:
        pass
    
    # Set Location
    
    getLocation0(topCTL[0], totalLocator[0])
    getLocation0(botCTL[0], totalLocator[-1])
    cmds.delete(cmds.pointConstraint(topCTL[0], botCTL[0], baseCTL[0]))
    cmds.delete(cmds.pointConstraint(topCTL[0], botCTL[0], deformCTL[0]))
    cmds.delete(cmds.pointConstraint(topCTL[0], botCTL[0], rootCTL[0]))
    
    if childLocator != []:
        for o in range(len(childLocator)):
            getLocation0(newCTL[o], childLocator[o])
    else:
        pass
    
    # Create Shape
    
    shapeChange8_CL(topCTL[0], 18, 1)
    shapeChange8_CL(botCTL[0], 18, 1)
    shapeChange10_CL(baseCTL[0], 13, 1)
    shapeChange19_CL(deformCTL[0], 6, 1)
    shapeChange8_CL(rootCTL[0], 17, 1)
    
    if childLocator != []:
        for o in range(len(childLocator)):
            shapeChange8_CL(newCTL[o], 18, 1)
    else:
        pass
    
    # Create Joint
    
    topJNT = cmds.joint(n=nameGuide+"Top0"+JNT_name)
    botJNT = cmds.joint(n=nameGuide+"Bot0"+JNT_name)
    cmds.parent(topJNT, world=True)
    cmds.parent(botJNT, world=True)
    getLocation0(topJNT, totalLocator[0])
    getLocation0(botJNT, totalLocator[-1])
    
    newJNT = []
    
    if childLocator != []:
        for o in range(len(childLocator)):
            cmds.select(childLocator[o])
            JNT = cmds.joint(n=nameGuide+"IK{}{}".format(o, JNT_name))
            cmds.parent(JNT, world=True)
            newJNT.append(JNT)
    else:
        pass
    
    # Create Lattice
    
    objectLattice = cmds.lattice(selectedObject, n=nameGuide+"_FFD", objectCentered=True, divisions=(2, numberControl, 2))
    objectLattice[1] = cmds.rename(objectLattice[1], nameGuide+"Lattice_FFD")
    objectLattice[2] = cmds.rename(objectLattice[2], nameGuide+"Base_FFD")
    cmds.setAttr(objectLattice[0]+".outsideLattice", 1)
    
    groupLattice = cmds.group(empty=True, n=nameGuide+"Lattice"+GRP_name)
    cmds.delete(cmds.pointConstraint(topCTL[0], botCTL[0], groupLattice))
    cmds.parent(objectLattice[1], groupLattice)
    cmds.parent(objectLattice[2], groupLattice)
    
    # Create Locator
    
    startLOC = cmds.spaceLocator(n=nameGuide+"StartDistance"+LOC_name)[0]
    endLOC = cmds.spaceLocator(n=nameGuide+"EndDistance"+LOC_name)[0]
    getLocation(startLOC, topCTL[0])
    getLocation(endLOC, botCTL[0])
    startLOCPoint = cmds.getAttr(startLOC+".t")[0]
    endLOCPoint = cmds.getAttr(endLOC+".t")[0]
    nodeDistance = cmds.distanceDimension(sp=(cmds.getAttr(topCTL[0]+".t")[0]), ep=(cmds.getAttr(botCTL[0]+".t")[0]))
    nodeDistanceParent = cmds.listRelatives(nodeDistance, p=1)
    nodeDistanceParent = cmds.rename(nodeDistanceParent, nameGuide+"Distance"+DIS_name)
    nodeDistance = nameGuide+"Distance"+DIS_name+'Shape'
    
    startLOCGroup = cmds.group(startLOC, n=startLOC.replace(LOC_name, GRP_name))
    endLOCGroup = cmds.group(endLOC, n=endLOC.replace(LOC_name, GRP_name))
    
    # Optional Lattice Shape
    '''
    scalePoint = []
    scalePoint.append(cmds.getAttr(objectLattice[2]+".scaleX"))
    scalePoint.append(cmds.getAttr(objectLattice[2]+".scaleY"))
    scalePoint.append(cmds.getAttr(objectLattice[2]+".scaleZ"))
    scalePointMax = max(scalePoint)
    
    cmds.setAttr(groupLattice+".scaleX", scalePointMax)
    cmds.setAttr(groupLattice+".scaleY", scalePointMax)
    cmds.setAttr(groupLattice+".scaleZ", scalePointMax)
    cmds.setAttr(objectLattice[1]+".translateX", 0)
    cmds.setAttr(objectLattice[1]+".translateY", 0)
    cmds.setAttr(objectLattice[1]+".translateZ", 0)
    cmds.setAttr(objectLattice[2]+".translateX", 0)
    cmds.setAttr(objectLattice[2]+".translateY", 0)
    cmds.setAttr(objectLattice[2]+".translateZ", 0)
    cmds.setAttr(objectLattice[1]+".scaleX", 1)
    cmds.setAttr(objectLattice[1]+".scaleY", 1)
    cmds.setAttr(objectLattice[1]+".scaleZ", 1)
    cmds.setAttr(objectLattice[2]+".scaleX", 1)
    cmds.setAttr(objectLattice[2]+".scaleY", 1)
    cmds.setAttr(objectLattice[2]+".scaleZ", 1)
    '''
    # Create System
    
    groupJNT(topJNT)
    groupJNT(botJNT)
    groupCTL(topCTL[0])
    groupCTL(botCTL[0])
    groupCTL(deformCTL[0])
    groupCTL(baseCTL[0])
    groupCTL(rootCTL[0])
    
    topJNTGroup = cmds.ls(nameGuide+"Top0"+TRN_name)
    botJNTGroup = cmds.ls(nameGuide+"Bot0"+TRN_name)
    topCTLGroup = cmds.ls(nameGuide+"Top0"+GRP_name)
    botCTLGroup = cmds.ls(nameGuide+"Bot0"+GRP_name)
    deformCTLGroup = cmds.ls(nameGuide+"DeformRotation0"+GRP_name)
    baseCTLGroup = cmds.ls(nameGuide+"BaseRotation0"+GRP_name)
    rootCTLGroup = cmds.ls(nameGuide+"Root0"+GRP_name)
    
    newJNTGroup = []
    newCTLGroup = []
    
    if childLocator != []:
        for o in range(len(childLocator)):
            groupJNT(newJNT[o])
            groupCTL(newCTL[o])
            newJNTGroup.append("{}IK{}{}".format(nameGuide, o, TRN_name))
            newCTLGroup.append("{}IK{}{}".format(nameGuide, o, GRP_name))
    else:
        pass
    
    allCTL = []
    
    allCTL.append(topCTL[0])
    
    for o in newCTL:
        test = cmds.ls(o)
        allCTL.append(test[0])
    
    allCTL.append(botCTL[0])
    
    # Connect Attribut
    
    if childLocator != []:
        skinList = newJNT
        skinList.append(str(topJNT))
        skinList.append(str(botJNT))
        cmds.skinCluster(objectLattice[1], skinList, n=nameGuide+"SkinCluster", tsb=True, mi=1, dr=1)
    else:
        cmds.skinCluster(objectLattice[1], topJNT, botJNT, n=nameGuide+"SkinCluster", tsb=True, mi=1, dr=1)
    
    cmds.connectAttr(deformCTL[0]+".rotate", objectLattice[2]+".rotate.")
    cmds.parentConstraint(topCTL[0], topJNTGroup[0], n=topJNTGroup[0].replace(TRN_name, PAC_name), mo=True)
    cmds.scaleConstraint(topCTL[0], topJNTGroup[0], n=topJNTGroup[0].replace(TRN_name, SCN_name), mo=True)
    cmds.parentConstraint(botCTL[0], botJNTGroup[0], n=botJNTGroup[0].replace(TRN_name, PAC_name), mo=True)
    cmds.scaleConstraint(botCTL[0], botJNTGroup[0], n=botJNTGroup[0].replace(TRN_name, SCN_name), mo=True)
    
    for con in ['rotateX', 'rotateY', 'rotateZ']:
        cmds.connectAttr('{}.{}'.format(baseCTL[0], con), '{}.{}'.format(selectedObject, con))
    
    if childLocator != []:
        for o in range(len(childLocator)):
            cmds.parentConstraint(allCTL[o], allCTL[o+2], newCTLGroup[o], n=newCTLGroup[o].replace(GRP_name, PAC_name), mo=True)
            cmds.scaleConstraint(allCTL[o], allCTL[o+2], newCTLGroup[o], n=newCTLGroup[o].replace(GRP_name, SCN_name), mo=True)
            cmds.parentConstraint(newCTL[o], newJNTGroup[o], n=newJNTGroup[o].replace(TRN_name, PAC_name), mo=True)
            cmds.scaleConstraint(newCTL[o], newJNTGroup[o], n=newJNTGroup[o].replace(TRN_name, SCN_name), mo=True)
    else:
        pass
    
    # Create Node
    
    cmds.addAttr(rootCTL[0], ln='squash', keyable=True, at='double', min=0, max=1, dv=1)
    
    nodeScaleWorld = cmds.createNode("multiplyDivide", n=nameGuide+"ScaleWorld"+MD_name)
    cmds.setAttr(nodeScaleWorld+".operation", 2)
    nodeTranslateTop = cmds.createNode("multiplyDivide", n=nameGuide+"TranslateTop"+MD_name)
    nodeTranslateBot = cmds.createNode("multiplyDivide", n=nameGuide+"TranslateBot"+MD_name)
    
    cmds.connectAttr(topCTL[0]+'.translate', nodeTranslateTop+'.input1')
    cmds.connectAttr(rootCTL[0]+'.squash', nodeTranslateTop+'.input2X')
    cmds.connectAttr(rootCTL[0]+'.squash', nodeTranslateTop+'.input2Y')
    cmds.connectAttr(rootCTL[0]+'.squash', nodeTranslateTop+'.input2Z')
    cmds.connectAttr(nodeTranslateTop+'.output', startLOCGroup+'.translate')
    cmds.connectAttr(botCTL[0]+'.translate', nodeTranslateBot+'.input1')
    cmds.connectAttr(rootCTL[0]+'.squash', nodeTranslateBot+'.input2X')
    cmds.connectAttr(rootCTL[0]+'.squash', nodeTranslateBot+'.input2Y')
    cmds.connectAttr(rootCTL[0]+'.squash', nodeTranslateBot+'.input2Z')
    cmds.connectAttr(nodeTranslateBot+'.output', endLOCGroup+'.translate')
    cmds.connectAttr(nodeDistance+".distance", nodeScaleWorld+".input2.input2X.")
    scalePoint = cmds.getAttr(nodeScaleWorld+".input2X")
    cmds.setAttr(nodeScaleWorld+".input1X", scalePoint)
    cmds.connectAttr(nodeScaleWorld+".output.outputX", topJNT+".scale.scaleX.")
    cmds.connectAttr(nodeScaleWorld+".output.outputX", topJNT+".scale.scaleZ.")
    cmds.connectAttr(nodeScaleWorld+".output.outputX", botJNT+".scale.scaleX.")
    cmds.connectAttr(nodeScaleWorld+".output.outputX", botJNT+".scale.scaleZ.")
    
    # Clean Up
    
    groupJoint = cmds.group(empty=True, n=nameGuide+"Squash"+TRN_name)
    groupMisc = cmds.group(empty=True, n=nameGuide+"Misc"+TRN_name)
    groupControl = cmds.group(empty=True, n=nameGuide+"Squash"+GRP_name)
    
    cmds.parent(topJNTGroup[0], groupJoint)
    
    if childLocator != []:
        for o in range(len(childLocator)):
            cmds.parent(newCTLGroup[o], groupControl)
            cmds.parent(newJNTGroup[o], groupJoint)
            
    cmds.parent(botJNTGroup[0], groupJoint)
    cmds.parent(groupMisc, groupJoint)
    cmds.parent(topCTLGroup[0], deformCTL[0])
    cmds.parent(botCTLGroup[0], deformCTL[0])
    cmds.parent(deformCTLGroup[0], rootCTL[0])
    cmds.parent(baseCTLGroup[0], rootCTL[0])
    cmds.parent(groupLattice, groupMisc)
    cmds.parent(nodeDistanceParent, groupMisc)
    cmds.parent(startLOCGroup, groupMisc)
    cmds.parent(endLOCGroup, groupMisc)
    cmds.parent(rootCTLGroup[0], groupControl)
    
    cmds.setAttr(baseCTL[0]+".translateX", l=1, k=0, cb=0)
    cmds.setAttr(baseCTL[0]+".translateY", l=1, k=0, cb=0)
    cmds.setAttr(baseCTL[0]+".translateZ", l=1, k=0, cb=0)
    cmds.setAttr(deformCTL[0]+".translateX", l=1, k=0, cb=0)
    cmds.setAttr(deformCTL[0]+".translateY", l=1, k=0, cb=0)
    cmds.setAttr(deformCTL[0]+".translateZ", l=1, k=0, cb=0)
    cmds.setAttr(groupJoint+".visibility", 0)
    cmds.setAttr(groupMisc+".visibility", 0)

def createSquashInfo_GT():
    print ('')
    print ('--- Create Reverse FKIK ---')
    print ('')
    print ('Function: Create Double Direction CTRL')
    print ('How to Use:')
    print ('    -Please Tools [Control Library]')
    print ('    -Please Create Guide')
    print ("    -Last Guide Doesn't Count")
    print ('    -Run the System')

###

def createDynamicHair_GT():
    global dynamicCTL
    selected = cmds.ls(sl=1)[0]
    findNameLast(selected)
    selectedSplit = selected.split('_')
    dynamicGRP = 'C_dynamicRIG'+GRP_name
    nameRig = selected.split('_GUIDES')[0]+'Dyn'
    nameRigGRP = nameRig+'RIG'+GRP_name
    nameRigTRN = nameRig+'RIG'+TRN_name
    listLOC = cmds.listRelatives(selected, ad=True, type='transform')
    listLOC.reverse()
    
    listCTL = []
    listCTLGroup = []
    listJNT = []
    listTRN = []
    listOffset = []
    listLAG = []
    listAIM = []
    listPMA = []
    listGroupAIM = []
    listORN = []
    stiffValue = 0.48
    dampValue = 0.7
    startValue = 1
    
    for i in listLOC:
        try: cmds.parent(i, selected)
        except: pass
    
    if not cmds.objExists(nameRig+'*End'+LOC_name):
        endLOC = cmds.duplicate(listLOC[-1], name=nameRig+'End'+LOC_name)[0]
        cmds.setAttr(endLOC+'.translateY', cmds.getAttr(listLOC[-1]+'.translateY')+5)
        #cmds.parent(endLOC, selected)
    
    cmds.select(d=True)
    
    if not cmds.objExists(dynamicGRP):
        cmds.group(empty=1, n=dynamicGRP)        
    else:
        pass
    
    cmds.group(empty=1, n=nameRigGRP)
    cmds.group(empty=1, n=nameRigTRN)
    cmds.parent(nameRigTRN, dynamicGRP)
    
    newLOC = cmds.listRelatives(selected, c=True)
    oldLOC = cmds.listRelatives(selected, c=True)
    allLOC = cmds.listRelatives(selected, c=True)
    newLOC.pop(0)
    oldLOC.pop()
    
    # --- Define ---
    
    def makeAllZero(obj):
        for attrs in ('.tx','.ty','.tz','.rx','.ry','.rz'):
            cmds.setAttr(obj+attrs, 0)
    
    def makeattr(node, attr, statekey , tipeatt , val=False , special=False):     
        if special == True:
            cmds.addAttr(node, ln=attr, at=tipeatt, k=statekey , dv=val, max=1, min=0, hnv=1, hxv=1)        
        else:
            cmds.addAttr(node, ln=attr, at=tipeatt, k=statekey)
        
        if tipeatt == 'double3':
            cmds.addAttr(node, ln='{0}X'.format(attr), p=attr, at='double', k=statekey)
            cmds.addAttr(node, ln='{0}Y'.format(attr), p=attr, at='double', k=statekey)
            cmds.addAttr(node, ln='{0}Z'.format(attr), p=attr, at='double', k=statekey)
    
    def createVectorAttr(node, attr, k=False):
        cmds.addAttr(node, ln=attr, attributeType='double3')
        cmds.addAttr(node, ln='{}X'.format(attr), p=attr, at='double', k=k)
        cmds.addAttr(node, ln='{}Y'.format(attr), p=attr, at='double', k=k)
        cmds.addAttr(node, ln='{}Z'.format(attr), p=attr, at='double', k=k)
    
    def createLAGLocator(obj, nameNEW=None):
        cmds.select(d=True)
        loc = cmds.spaceLocator(n='locator')[0]
        cmds.addAttr(loc, ln='enable', at='double', k=True, min=0, max=1)
        cmds.addAttr(loc, ln='start', at='double', k=True)
        cmds.addAttr(loc, ln='stiff', at='double', k=True, min=0, max=1, dv=0.5)
        cmds.addAttr(loc, ln='damp', at='double', k=True, min=0, max=1, dv=0.5)
        
        createVectorAttr(loc, 'gravity', k=True)
        createVectorAttr(loc, 'outTranslate', k=True)
        createVectorAttr(loc, 'velocity', k=True)
        createVectorAttr(loc, 'dynamicTranslate', k=True)
        createVectorAttr(loc, 'dynamicVelocity', k=True)
        createVectorAttr(loc, 'initTranslate', k=True)
        createVectorAttr(loc, 'initVelocity', k=True)
        
        # Var $translate, dapat nilai dari tX tY tZ
        # Var $outTranslate, dapat dari t
        # Var $velocity, dapat dari initVelocity
        # Var $state, dapat dari enable
        
        # Kalau $state lebih dari 0
        # Var $initTranslate, dapat dari initTranslate
        # Var outTranslate, perhitungan
        
        # Kalau global frame lebih dari start Value, hah buat apa ini
            # Var $velocity, dapat dari initVelocity, ga paham :v
            
            # Kalau $state lebih dari 0
                # Var $outTranslate, dapat dari outTranslateX Y Z
                # Var $sniff, dapat dari sniff
                # Var $damp, dapat dari damp
                
                # Var $gravity, dapat dari gravityX Y Z
                
                # Ver $acceleration, perhitungan
                # Ver $velocity, $acceleration * 2
                # Ver $outTranslate, $velocity * 2
                # Ver $outTranslate, perhitungan
        
        # Connect Var ke objek
        
        cmd = ('vector $translate = <<{0}.translateX, {0}.translateY, {0}.translateZ>>;\n'+
            'vector $outTranslate = $translate;\n'+
            'vector $velocity = <<{0}.initVelocityX, {0}.initVelocityY, {0}.initVelocityZ>>;\n'+
            'float $state = {0}.enable;\n\n'+
    
            'if ($state > 0.0001)\n'+
            '{{\n'+
            '    vector $initTranslate = <<{0}.initTranslateX, {0}.initTranslateY, {0}.initTranslateZ>>;\n'+
            '    $outTranslate = $translate+$initTranslate;\n'+
            '}}\n\n'+
    
    
            'if (frame > {0}.start)\n'+
            '{{\n'+
            '    $velocity = <<{0}.velocityX, {0}.velocityY, {0}.velocityZ>>;\n\n'+
    
            '    if ($state > 0.0001)\n'+
            '    {{\n'+
            '        $outTranslate = <<{0}.outTranslateX, {0}.outTranslateY, {0}.outTranslateZ>>;\n'+
            '        float $stiff = {0}.stiff;\n'+
            '        float $damp = {0}.damp;\n\n'+
    
            '        vector $gravity = <<{0}.gravityX, {0}.gravityY, {0}.gravityZ>>;\n\n'+
    
            '        vector $acceleration = (-1*$damp*$velocity)+($stiff*($translate-$outTranslate))+$gravity;\n'+
            '        $velocity += $acceleration;\n'+
            '        $outTranslate += $velocity;\n'+
            '        $outTranslate = ($state*$outTranslate)+((1.0-$state)*$translate);\n'+
            '    }}\n'+
            '}}\n\n'+
    
            '{0}.outTranslateX = $outTranslate.x;\n'+
            '{0}.outTranslateY = $outTranslate.y;\n'+
            '{0}.outTranslateZ = $outTranslate.z;\n\n'+
    
            '{0}.velocityX = $velocity.x;\n'+
            '{0}.velocityY = $velocity.y;\n'+
            '{0}.velocityZ = $velocity.z;')
        
        cmd = cmd.format(loc)
        exp = cmds.expression(string=cmd)
        
        if nameNEW is not None:
            lag = nameNEW.replace(LOC_name, 'LAG')
            loc = cmds.rename(loc, lag)
            cmds.rename(exp, nameRig+('_EXP'))
            cmds.parent(loc, nameRigTRN)
            listLAG.append(lag)
        
        cmds.delete(cmds.parentConstraint(obj, loc, mo=False))
        return loc
    
    def createCTL(obj, index, CTL_name, GRP_name):    
        numb = str(index)
        ctlGroup = cmds.createNode('transform', n=nameRig+numb+GRP_name)
        ctl = cmds.circle(n=nameRig+numb+CTL_name, normal=(1,0,0))
        listCTL.append(ctl[0])
        listCTLGroup.append(ctlGroup)
        cmds.delete(cmds.parentConstraint(obj, ctl, mo=False))
        cmds.delete(cmds.parentConstraint(obj, ctlGroup, mo=False))
        
        if index == 0:
            cmds.parent(ctlGroup, nameRigGRP)
            makeattr(ctl[0], 'dynamic', 1, 'double', 0, special=True)
            makeattr(ctl[0], 'stiff', 1, 'double', stiffValue, special=True)
            makeattr(ctl[0], 'damp', 1, 'double', dampValue, special=True)
            makeattr(ctl[0], 'start', 1, 'double', 1, special=True)
        else:
            cmds.parent(ctlGroup, listCTL[index-1])    
                 
        cmds.parent(ctl[0], ctlGroup)
        makeattr(ctl[0], 'DynamicsBakeRotate', 0, 'double3')
    
    def createJNT(obj, index, jntName, trnName, offsetName):
        numb = str(index)
        jnt = cmds.joint(n=nameRig+numb+jntName)
        trn = cmds.createNode('transform', n=nameRig+numb+offsetName)
        offset = cmds.createNode('transform', n=nameRig+numb+trnName)
        cmds.delete(cmds.parentConstraint(obj, jnt, mo=False))
        cmds.delete(cmds.parentConstraint(jnt, trn, mo=False))
        cmds.delete(cmds.parentConstraint(jnt, offset, mo=False))
        makeAllZero(jnt)
        listJNT.append(jnt)
        listTRN.append(trn)
        listOffset.append(offset)
        
        if index == 0:
            try: cmds.parent(jnt, listCTL[index])
            except: pass
            cmds.delete(trn)
            cmds.delete(offset)
        else:    
            try: cmds.parent(trn, listJNT[index-1])
            except: pass
            cmds.parent(offset, trn) 
            cmds.parent(jnt, offset)
    
    def createOrient(obj, index, nameORN):
        numb = str(index)
        orn = cmds.createNode('orientConstraint', n=nameRig+numb+nameORN)
        listORN.append(orn)
        cmds.parent(orn, obj)
        makeAllZero(orn)
    
    def createGroupAIM(obj, index, nameAIM, oldobj, offset):
        numb = str(index)
        aim = cmds.createNode('transform', n=nameRig+numb+nameAIM)
        cmds.delete(cmds.parentConstraint(oldobj, aim, mo=False))
        listGroupAIM.append(aim)
        
        if index == 0:
            cmds.parent(aim, obj)
        else:
            cmds.parent(aim, offset)
    
    def createAIM(obj, index, nameAIM):
        numb = str(index)
        aim = cmds.createNode('aimConstraint', n=nameRig+numb+nameAIM)
        cmds.parent(aim, obj)
        makeAllZero(aim)
        cmds.connectAttr(aim+'.constraintRotate', obj+'.rotate')
        listAIM.append(aim)
    
    def createPMA(obj, index, namePMA):
        numb = str(index)
        pma = cmds.createNode('plusMinusAverage', n=nameRig+numb+namePMA)
        cmds.setAttr(pma+'.operation', 2)
        listPMA.append(pma)
    
    def connectlag(jnt, ctlGroup, ctl, lag, aim, pma, orn, aimValue, index):
        global mainCTL
        
        if index == 0:
            mainCTL = ctl
    
        cmds.setAttr(aim+'.worldUpType', aimValue)
        
        cmds.connectAttr(ctl+'.worldMatrix', aim+'.worldUpMatrix')
        cmds.connectAttr(lag+'.parentMatrix[0]', aim+'.target[0].targetParentMatrix')
        
        cmds.connectAttr(mainCTL+'.stiff', lag+'.stiff')
        cmds.connectAttr(mainCTL+'.damp', lag+'.damp')
        cmds.connectAttr(mainCTL+'.dynamic', lag+'.enable')
        cmds.connectAttr(mainCTL+'.start', lag+'.start')
       
        cmds.connectAttr(lag+'.outTranslate', pma+'.input3D[0]')
        cmds.connectAttr(lag+'.translate', pma+'.input3D[1]')
        cmds.connectAttr(lag+'.outTranslate', aim+'.target[0].targetTranslate')
        cmds.connectAttr(pma+'.output3D', lag+'.dynamicTranslate')
        cmds.connectAttr(lag+'.velocity', lag+'.dynamicVelocity')
    
        cmds.connectAttr(ctlGroup+'.worldInverseMatrix[0]', orn+'.constraintParentInverseMatrix')
        cmds.connectAttr(jnt+'.worldMatrix[0]', orn+'.target[0].targetParentMatrix')
        cmds.connectAttr(orn+'.constraintRotateX', ctl+'.DynamicsBakeRotateX')
        cmds.connectAttr(orn+'.constraintRotateY', ctl+'.DynamicsBakeRotateY')
        cmds.connectAttr(orn+'.constraintRotateZ', ctl+'.DynamicsBakeRotateZ')
        cmds.connectAttr(ctl+'.rotateOrder', orn+'.constraintRotateOrder')    
        cmds.connectAttr(jnt+'.parentInverseMatrix[0]', aim+'.constraintParentInverseMatrix')
    
    def connectCTL(ctl, offsetTRN, index):
        if not index == 0:
            cmds.connectAttr(ctl[index]+'.translate', offsetTRN[index]+'.translate')
            cmds.connectAttr(ctl[index]+'.rotate', offsetTRN[index]+'.rotate')
            cmds.connectAttr(ctl[index]+'.rotateOrder', offsetTRN[index]+'.rotateOrder')
    
    # --- Run the Script ---
    
    for f in range(len(oldLOC)):
        createLAGLocator(newLOC[f], newLOC[f])
        createCTL(oldLOC[f], f, CTL_name, GRP_name)
        createJNT(listCTL[f], f, JNT_name, 'Offset'+TRN_name, TRN_name)
        createOrient(listCTL[f], f, '_ORN')
        createGroupAIM(listCTL[f], f, 'AIM'+GRP_name, newLOC[f], listOffset[f])
        createAIM(listJNT[f], f, '_AIM')
        createPMA(listLAG[f], f, PMA_name)
        connectlag(listJNT[f], listCTLGroup[f], listCTL[f], listLAG[f], listAIM[f], listPMA[f], listORN[f], 2, f)
        connectCTL(listCTL, listOffset, f)
        cmds.pointConstraint(listGroupAIM[f], listLAG[f], n=listLAG[f].replace('_LAG', PAC_name), mo=False)
    
    for j in range(len(allLOC)):
        if j == 0:
            pass
        else:
            cmds.parent(allLOC[j], allLOC[j-1])
    
    if not cmds.objExists(nameRig+'*End'+LOC_name):
        cmds.delete(nameRig+'*End'+LOC_name)
    
    dynamicCTL = listCTL[0]
    cmds.select(d=True)

def createDynamicHairInfo_GT():
    print ('')
    print ('Please make X axis to the down side you want')

def createDynamicHairInfo_GT():
    print ('')
    print ('--- Create Reverse FKIK ---')
    print ('')
    print ('Function: Create Double Direction CTRL')
    print ('How to Use:')
    print ('    -Please Tools [Control Library]')
    print ('    -Please Create Guide')
    print ("    -Last Guide Doesn't Count")
    print ('    -Run the System')

###

def skirtJointNameTextLoad_GT():
    selected = cmds.ls(os=True)[0]
    cmds.textField('skirtJointNameText', e=True, text=str(selected))

def createSkirt_GT():
    #ctlName = 'C_visibility0_CTL.followSkirt'
    aimName = 'Aim'
    #jointAIMName = '_legKneeSkin0_JNT'
    jointAIMName = cmds.textField('skirtJointNameText', q=True, text=True)
    listController = cmds.ls(os=1)
    #listController = cmds.ls(['*_skirtFrontMain0_CTL', '*_skirtBackMain0_CTL', '*_skirtSideAMain0_CTL', '*_skirtSideBMain0_CTL'])
    #ctlNameSplit = ctlName.split('.')
    #ctlAttr = ctlNameSplit[0]
    #nameAttr = ctlNameSplit[1]
    
    #cmds.addAttr(ctlAttr, ln=nameAttr, at='double', k=1, min=0, max=1, dv=1)
    
    for ctl in listController:
        findName(ctl)
        ctlSplit = ctl.split('_')
        importController(nameGuide, "IK")
        cmds.select()
        offset = cmds.group(n=findNameResult)
        #offset = '{}_{}Offset_GRP'.format(ctlSplit[0], ctlSplit[1])
        #offset = cmds.group(empty=True, name='{}_{}Offset_GRP'.format(ctlSplit[0], ctlSplit[1]))
        #cmds.delete(cmds.parentConstraint(ctl, offset, maintainOffset=False))
        #cmds.parent(offset, '{}_{}_GRP'.format(ctlSplit[0], ctlSplit[1]))
        #cmds.parent(ctl, offset)
        #cmds.connectAttr('{}.rotateY'.format(offset), '{}.rotateY'.format(offset.replace(GRP_name, TRN_name)))
        
        ac = cmds.aimConstraint('{}{}'.format(ctlSplit[0], jointAIMName), offset, n=offset.replace(GRP_name, 'AIM'),
                                aimVector=(1.0, 0.0, 0.0), upVector=(0.0, 1.0, 0.0), skip=['x', 'z'],
                                maintainOffset=True,
                                worldUpType='objectrotation', worldUpVector=(1.0, 0.0, 0.0),
                                worldUpObject='{}_{}{}'.format(ctlSplit[0], ctlSplit[1].replace('Main', aimName), CTL_name))
        '''
        if ctlSplit[0] == 'L':
            cmds.connectAttr('{}.{}'.format(ctlAttr, nameAttr), '{}.{}{}W0'.format(ac[0], ctlSplit[0], jointAIMName), force=True)
        elif ctlSplit[0] == 'R':
            cmds.connectAttr('{}.{}'.format(ctlAttr, nameAttr), '{}.{}{}W0'.format(ac[0], ctlSplit[0], jointAIMName), force=True)
        '''
        cnd = cmds.shadingNode('condition', asUtility=True, name='{}_{}{}'.format(ctlSplit[0], ctlSplit[1], CON_name))
        
        cmds.setAttr('{}.secondTerm'.format(cnd), 0)
        cmds.setAttr('{}.colorIfFalseR'.format(cnd), 0)
        cmds.setAttr('{}.operation'.format(cnd), 5)
        cmds.connectAttr('{}.constraintRotateY'.format(ac[0]), '{}.firstTerm'.format(cnd))
        cmds.connectAttr('{}.constraintRotateY'.format(ac[0]), '{}.colorIfTrueR'.format(cnd))
        cmds.disconnectAttr('{}.constraintRotateY'.format(ac[0]), '{}.rotateY'.format(offset))
        cmds.connectAttr('{}.outColorR'.format(cnd), '{}.rotateY'.format(offset))
    ### Skirt System End ###

def createSkirtInfo_GT():
    print ('')
    print ('--- Create Reverse FKIK ---')
    print ('')
    print ('Function: Create Double Direction CTRL')
    print ('How to Use:')
    print ('    -Please Tools [Control Library]')
    print ('    -Please Create Guide')
    print ("    -Last Guide Doesn't Count")
    print ('    -Run the System')

###

def dummyPlanes_TC(name, list, sizeX):
    selection = cmds.ls(list)
    dup = cmds.duplicate(selection)
    grp = cmds.group(dup)
    
    dupChild = cmds.listRelatives(dup, ad=True, type='locator')
    
    for child in dupChild:
        cmds.setAttr(child+'.localScaleX', 0.1)
        cmds.setAttr(child+'.localScaleY', 0.1)
        cmds.setAttr(child+'.localScaleZ', 1)
    
    bbox = cmds.exactWorldBoundingBox(dup)
    bboxList = [(-bbox[0]+bbox[3]), (-bbox[1]+bbox[4]), (-bbox[2]+bbox[5])]
    bboxListDup = [(-bbox[0]+bbox[3]), (-bbox[1]+bbox[4]), (-bbox[2]+bbox[5])]
    bboxList.sort(reverse=True)
    cube = cmds.polyPlane(n=name, sx=sizeX, sy=1, w=bboxList[0], h=bboxList[1])
            
    cmds.xform(grp, cp=1)
    cmds.delete(cmds.parentConstraint(grp, cube, mo=0))
    cmds.delete(grp)
    
    if bboxList[0] == bboxListDup[2]:
        cmds.setAttr(selection[0]+".rotateY", 90)
    if bboxList[0] == bboxListDup[1]:
        cmds.setAttr(selection[0]+".rotateZ", 90)
    
    cmds.select(cube)
    return cube[0]

def attachObject_TC(list, mesh):
    # Select child list, then select mesh/surface
    # Make sure main object UV already
    selected = list
    mainObject = mesh
    #selected.remove(selected[-1])
    folliceList = []
    
    for element in selected:
        # Find U/V value
        loc = cmds.spaceLocator()[0]
        con = cmds.parentConstraint(element, loc, mo=False)
        x = cmds.xform(loc, t=True, q=True)
        closest = cmds.createNode('closestPointOnMesh')
        cmds.connectAttr(mainObject+'.outMesh', closest+'.inMesh')
        # Help finding exactly U/V point you want
        cmds.setAttr(closest + '.inPositionX', x[0])
        cmds.setAttr(closest + '.inPositionY', x[1])
        cmds.setAttr(closest + '.inPositionZ', x[2])   
        
        uPoint = cmds.getAttr(closest + '.result.parameterU')[0]
        vPoint = cmds.getAttr(closest + '.result.parameterV')[0]
        follicle = cmds.createNode("follicle")
        follicleMain = cmds.listRelatives(follicle, type='transform', p=True)[0]
        follicleMain = cmds.rename(follicleMain, element + 'attach_FLC')
        # Make follicle follow the shape rotate/translate value
        
        #if cmds.checkBox('attachObjectTranslate', query=True, value=True) == True:
        cmds.connectAttr(follicle + ".outTranslate", follicleMain + ".translate")
        #if cmds.checkBox('attachObjectRotate', query=True, value=True) == True:
        cmds.connectAttr(follicle + ".outRotate", follicleMain + ".rotate")
        
        # Make follicle follow main object surface
        cmds.connectAttr(mainObject + '.worldMatrix', follicle + '.inputWorldMatrix')
        cmds.connectAttr(mainObject + '.outMesh', follicle + '.inputMesh')
        cmds.setAttr(follicle + ".simulationMethod", 0)
        cmds.setAttr(follicle + '.parameterU', uPoint)
        cmds.setAttr(follicle + '.parameterV', vPoint)
        # Make element follow follicle
        cmds.parentConstraint(follicleMain, element, mo=True)
        cmds.delete(closest)
        cmds.delete(loc)
        folliceList.append(follicle)
    
    return folliceList

def createTentacle_GT():
    global ctrlSwitch, dynamicCTL
    selectedGuide = cmds.ls(os=1,ap=1)[0]
    #selectedGuide = 'dada_GUIDES'
    guideSplit = selectedGuide.split("_GUIDES")
    nameGuide = guideSplit[0]
    totalLocator = cmds.listRelatives(selectedGuide, ad=True, f=True ,type="transform")
    totalLocator.reverse()
    totalNum = len(totalLocator)
    c = 0
    inbetweenAdd = 3
    
    # Run Major System
    
    cmds.select(selectedGuide)
    createSwitchSpline_GT()
    
    # Create Curve and Mesh
    
    tX = cmds.getAttr(selectedGuide+'.translateX')[0]
    tY = cmds.getAttr(selectedGuide+'.translateY')[0]
    tZ = cmds.getAttr(selectedGuide+'.translateZ')[0]
    rX = cmds.getAttr(selectedGuide+'.rotateX')[0]
    rY = cmds.getAttr(selectedGuide+'.rotateY')[0]
    rZ = cmds.getAttr(selectedGuide+'.rotateZ')[0]
    cmds.setAttr(selectedGuide+'.translateX', 0)
    cmds.setAttr(selectedGuide+'.translateY', 0)
    cmds.setAttr(selectedGuide+'.translateZ', 0)
    cmds.setAttr(selectedGuide+'.rotateX', 0)
    cmds.setAttr(selectedGuide+'.rotateY', 0)
    cmds.setAttr(selectedGuide+'.rotateZ', 0)
    planeMesh = dummyPlanes_TC(nameGuide+'_path'+MSH_name, selectedGuide, (totalNum-1)*(inbetweenAdd+1))
    cmds.makeIdentity(planeMesh, apply=True, t=True, r=True, s=True, n=False, pn=True)
    cmds.setAttr(selectedGuide+'.translateX', tX)
    cmds.setAttr(selectedGuide+'.translateY', tY)
    cmds.setAttr(selectedGuide+'.translateZ', tZ)
    cmds.setAttr(selectedGuide+'.rotateX', rX)
    cmds.setAttr(selectedGuide+'.rotateY', rY)
    cmds.setAttr(selectedGuide+'.rotateZ', rZ)
    
    curvePosition = []
    
    for b in totalLocator:
        locTemp = cmds.spaceLocator(n='C_locTemp'+LOC_name)[0]
        cmds.delete(cmds.pointConstraint(b, locTemp, mo=False))
        locPosition = cmds.getAttr(locTemp+'.t')[0]
        curvePosition.append(locPosition)
        cmds.delete(locTemp)
        
    planeCurve = cmds.curve(p=curvePosition, n=nameGuide+'_path'+CRV_name)
    
    # Create System Curve Wrap
    
    curveWrapName = nameGuide+'_curveWrap'
    curveWrapNode = cmds.createCurveWarp(planeMesh, planeCurve)
    curveWrapNode = cmds.rename(curveWrapNode, curveWrapName)
    curveWrap = curveWrapName
    
    cmds.addAttr(ctrlSwitch, ln="Path_Attr", keyable=True, at="enum", en='---:')
    cmds.addAttr(ctrlSwitch, ln="Path_Follow", keyable=True, at="double", min=0, max=10, dv=0)
    cmds.addAttr(ctrlSwitch, ln="Path_Rotation", keyable=True, at="double", dv=0)
    cmds.addAttr(ctrlSwitch, ln="Path_Twist", keyable=True, at="double", dv=0)
    cmds.addAttr(ctrlSwitch, ln="Path_Scale", keyable=True, at="double", min=0, max=2, dv=1)
    cmds.setAttr(ctrlSwitch+'.Path_Attr', lock=True)
    
    nodePathOffset = cmds.createNode("multiplyDivide", n=nameGuide+"Freeze"+MD_name)
    cmds.setAttr(nodePathOffset+'.operation', 2)
    cmds.setAttr(nodePathOffset+'.input2X', 10)
    
    cmds.connectAttr(ctrlSwitch+'.Path_Follow', nodePathOffset+'.input1X')
    cmds.connectAttr(nodePathOffset+'.outputX', curveWrap+'.offset')
    cmds.connectAttr(ctrlSwitch+'.Path_Rotation', curveWrap+'.rotation')
    cmds.connectAttr(ctrlSwitch+'.Path_Twist', curveWrap+'.twistRotation')
    cmds.connectAttr(ctrlSwitch+'.Path_Scale', curveWrap+'.lengthScale')
    
    # Create Joint
    
    jointTotal = totalNum+((totalNum-1)*inbetweenAdd)
    jointList = []
    edgeNum = 1
    
    for b in range(jointTotal):
        cls = cmds.cluster('{}.e[{}]'.format(planeMesh, str(edgeNum)))
        jnt = cmds.joint(n=C_side+nameGuide+'Fol_'+str(b)+JNT_name)
        cmds.delete(cmds.pointConstraint(cls, jnt, mo=False))
        cmds.parent(jnt, w=True)
        cmds.delete(cls)
        edgeNum = edgeNum+2
        groupJNT(jnt)
        jointList.append(jnt.replace(JNT_name, TRN_name))
        
        if b+1 == jointTotal:
            cmds.delete(cmds.pointConstraint(totalLocator[-1], jnt, mo=False))
    
    #folliceList = attachObject_TC(jointList, planeMesh)
    
    # Clean-up a bit
    
    groupMain = nameGuide+'SplineFKIKMain'+GRP_name
    groupTRN = nameGuide+TRN_name
    groupRIG = nameGuide+GRP_name
    groupMisc = nameGuide+'Misc'+TRN_name
    groupFK = nameGuide+'FK'+GRP_name
    groupIK = nameGuide+'IK'+GRP_name
    groupPart = nameGuide+'Part'+GRP_name
    groupTRNSkin = nameGuide+'Skin'+TRN_name
    groupTRNFK = nameGuide+'FK'+TRN_name
    groupTRNIK = nameGuide+'IK'+TRN_name
    jointSkin = cmds.ls(nameGuide+'Skin*'+JNT_name)
    
    pathGRP = cmds.group(empty=True, n=nameGuide+'_path'+TRN_name)
    jointGRP = cmds.group(empty=True, n=nameGuide+'_joint'+TRN_name)
    folliceGRP = cmds.group(empty=True, n=nameGuide+'_fol'+TRN_name)
    
    cmds.parent(planeMesh, pathGRP)
    cmds.parent(planeCurve, pathGRP)
    cmds.parent(jointList, jointGRP)
    #cmds.parent(folliceList, folliceGRP)
    cmds.parent(jointGRP, pathGRP)
    cmds.parent(folliceGRP, pathGRP)
    cmds.parent(pathGRP, groupTRN)
    
    #cmds.setAttr(groupRIG+'.visibility', 0)
    cmds.setAttr(jointGRP+'.visibility', 0)
    cmds.setAttr(folliceGRP+'.visibility', 0)
    
    # Re-build Sine Wave
    
    sineGRP = nameGuide+'Sine'+TRN_name
    cmds.delete(sineGRP)
    
    cmds.select(planeMesh)
    sineAttr = cmds.nonLinear(type='sine')
    sineGRP = cmds.group(sineAttr[1], n=nameGuide+'Sine'+TRN_name, p=groupMisc)
    cmds.setAttr(sineAttr[1]+'.overrideEnabled', 1)
    cmds.setAttr(sineAttr[1]+'.overrideDisplayType', 2)
    sineAttr[1] = cmds.rename(sineAttr[1], nameGuide+'_SNH')
    sineAttr[0] = cmds.rename(sineAttr[0], nameGuide+'_Sine')
    cmds.parent(sineGRP, groupMisc)
    cmds.connectAttr(ctrlSwitch+".Wave_Enable", sineAttr[0]+".envelope")
    cmds.connectAttr(ctrlSwitch+".Wave_Amplitude", sineAttr[0]+".amplitude")
    cmds.connectAttr(ctrlSwitch+".Wave_Length", sineAttr[0]+".wavelength")
    cmds.connectAttr(ctrlSwitch+".Wave_Offset", sineAttr[0]+".offset")
    cmds.connectAttr(ctrlSwitch+".Wave_Dropoff", sineAttr[0]+".dropoff")
    cmds.connectAttr(ctrlSwitch+".Wave_Low_Bound", sineAttr[0]+".lowBound")
    cmds.connectAttr(ctrlSwitch+".Wave_High_Bound", sineAttr[0]+".highBound")
    cmds.connectAttr(ctrlSwitch+".Wave_Ratation_X", sineAttr[1]+".rotateX")
    cmds.connectAttr(ctrlSwitch+".Wave_Ratation_Y", sineAttr[1]+".rotateY")
    cmds.connectAttr(ctrlSwitch+".Wave_Ratation_Z", sineAttr[1]+".rotateZ")
    cmds.parentConstraint(ctrlSwitch, sineGRP, n=sineGRP.replace(TRN_name, 'TRN_PAC'), mo=True)
    cmds.scaleConstraint(ctrlSwitch, sineGRP, n=sineGRP.replace(TRN_name, 'TRN_SCN'), mo=True)
    cmds.setAttr(ctrlSwitch+".Wave_Ratation_Z", 90)
    
    cmds.delete(cmds.pointConstraint(totalLocator[-1], sineAttr[1], mo=False))
    
    #cmds.skinCluster(planeMesh, jointSkin, tsb=True, maximumInfluences=5, dropoffRate=4)
    
    # Create Reverse FKIK
    
    extraLocator = cmds.duplicate(totalLocator[-1], n='extraLocatorTEMP_loc')[0]
    cmds.parent(extraLocator, totalLocator[-1])
    cmds.setAttr(extraLocator+'.translateX', cmds.getAttr(totalLocator[-1]+'.translateX'))[0]
    cmds.setAttr(extraLocator+'.translateY', cmds.getAttr(totalLocator[-1]+'.translateY'))[0]
    cmds.setAttr(extraLocator+'.translateZ', cmds.getAttr(totalLocator[-1]+'.translateZ'))[0]
    cmds.select(selectedGuide)
    createReverseFKIK_GT()
    cmds.delete(extraLocator)
    
    reverseFKGroup = nameGuide+'Fk'+GRP_name
    reverseIKGroup = nameGuide+'Ik'+GRP_name
    reverseFWDGroupList = cmds.ls(nameGuide+'fwd*'+GRP_name)
    reverseRVSGroupList = cmds.ls(nameGuide+'rvs*'+GRP_name)
    
    dummyFKDup = cmds.duplicate(reverseFKGroup)[0]
    dummyChild = cmds.listRelatives(dummyFKDup, ad=True, type='transform')
    
    for child in dummyChild:
        nameSplit = child.split('|')
        name = 'dummy_'+nameSplit[-1]
        cmds.rename(child, name)
    
    dummyFKDup = cmds.rename(dummyFKDup, 'dummy_'+reverseFKGroup)
    dummyFKGroup = 'dummy_'+reverseFKGroup
    cmds.setAttr(dummyFKGroup+'.visibility', 0)
    cmds.setAttr(reverseRVSGroupList[0]+'.visibility', 0)
    
    # Create Dummy Follow
    
    planeMeshDup = cmds.duplicate(planeMesh, n=planeMesh.replace('_path_', '_dummy_'))[0]
    dummyFWDOffsetGroup = cmds.ls('dummy_{}fwdFk*{}'.format(nameGuide, GRP_name))
    dummyRVSOffsetGroup = cmds.ls('dummy_{}rvsFk*{}'.format(nameGuide, GRP_name))
    folliceListDummyFWD = attachObject_TC(dummyFWDOffsetGroup, planeMesh)
    folliceListDummyRVS = attachObject_TC(dummyRVSOffsetGroup, planeMesh)
    folliceGRPDummy = cmds.group(empty=True, n=nameGuide+'_folDummy'+TRN_name)
    cmds.parent(folliceListDummyFWD, folliceGRPDummy)
    cmds.parent(folliceListDummyRVS, folliceGRPDummy)
    cmds.parent(folliceGRPDummy, pathGRP)
    
    for o in range(len(reverseFWDGroupList)):
        cmds.connectAttr(dummyFWDOffsetGroup[o]+'.translate', reverseFWDGroupList[o]+'.translate')
        cmds.connectAttr(dummyFWDOffsetGroup[o]+'.rotate', reverseFWDGroupList[o]+'.rotate')
        cmds.connectAttr(dummyFWDOffsetGroup[o]+'.scale', reverseFWDGroupList[o]+'.scale')
    
    curveWrapNameDummy = nameGuide+'Dummy_curveWrap'
    curveWrapNodeDummy = cmds.createCurveWarp(planeMeshDup, planeCurve)
    curveWrapNodeDummy = cmds.rename(curveWrapNodeDummy, curveWrapNameDummy)
    curveWrapDummy = curveWrapNameDummy
    
    cmds.connectAttr(nodePathOffset+'.outputX', curveWrapDummy+'.offset')
    #cmds.connectAttr(ctrlSwitch+'.Path_Rotation', curveWrapDummy+'.rotation')
    #cmds.connectAttr(ctrlSwitch+'.Path_Twist', curveWrapDummy+'.twistRotation')
    #cmds.connectAttr(ctrlSwitch+'.Path_Scale', curveWrapDummy+'.lengthScale')
    cmds.setAttr(planeMeshDup+'.visibility', 0)
    cmds.setAttr(folliceGRPDummy+'.visibility', 0)
    
    # Combine 2 System
    
    reverseMainGroup = nameGuide+'ReverseMain'+GRP_name
    
    ctrlPartGroup = cmds.ls(nameGuide+'Part*Offset'+GRP_name)
    cmds.delete(cmds.ls(nameGuide+'Part*TRN_PAC'))
    cmds.delete(cmds.ls(nameGuide+'Part*TRN_SCN'))
    reversePartCTL = cmds.ls(nameGuide+'Ik*'+CTL_name)
    reversePartCTL.reverse()
    
    for o in range(len(ctrlPartGroup)):
        target = ctrlPartGroup[o].replace('Offset', '')
        pac = cmds.parentConstraint(reversePartCTL[o], target, mo=True, n=target.replace(GRP_name, PAC_name))
        scn = cmds.scaleConstraint(reversePartCTL[o], target, mo=True, n=target.replace(GRP_name, SCN_name))
    
    mel.eval('CBdeleteConnection "{}";'.format(groupFK+'.visibility'))
    mel.eval('CBdeleteConnection "{}";'.format(groupIK+'.visibility'))
    mel.eval('CBdeleteConnection "{}";'.format(groupPart+'.visibility'))
    cmds.setAttr(groupFK+'.visibility', 0)
    cmds.setAttr(groupIK+'.visibility', 0)
    cmds.setAttr(groupPart+'.visibility', 0)
    
    cmds.parent(reverseMainGroup, ctrlSwitch)
    
    #cmds.skinCluster(planeMeshDup, jointSkin, tsb=True, maximumInfluences=5, dropoffRate=4)
    
    # Change Something Sorry
    
    planeMeshSkin = cmds.duplicate(planeMesh, n=planeMesh.replace('_path_', '_skin_'))[0]
    #cmds.delete(folliceList)
    folliceList = attachObject_TC(jointList, planeMeshSkin)
    cmds.parent(folliceList, folliceGRP)
    cmds.skinCluster(planeMeshSkin, jointSkin, tsb=True, maximumInfluences=5, dropoffRate=4)
    cmds.parentConstraint(ctrlSwitch, planeCurve, mo=True, n=planeCurve.replace(CRV_name, PAC_name))
    
    # Create Hair Dynamic
    
    cmds.select(selectedGuide)
    createDynamicHair_GT()
    cmds.delete(nameGuide+'DynEnd'+LOC_name)
    
    dynamicTRN = nameGuide+'DynRIG'+TRN_name
    dynamicGRP = nameGuide+'DynRIG'+GRP_name
    
    cmds.parent(dynamicTRN, groupTRN)
    cmds.parent(dynamicGRP, ctrlSwitch)
    cmds.setAttr(dynamicGRP+'.visibility', 0)
    cmds.addAttr(ctrlSwitch, ln="Dynamic_Attr", keyable=True, at="enum", en='---:')
    cmds.addAttr(ctrlSwitch, ln="dynamic", keyable=True, at="double", min=0, max=1, dv=0)
    cmds.addAttr(ctrlSwitch, ln="stiff", keyable=True, at="double", min=0, max=1, dv=0.48)
    cmds.addAttr(ctrlSwitch, ln="damp", keyable=True, at="double", min=0, max=1, dv=0.7)
    cmds.addAttr(ctrlSwitch, ln="start", keyable=True, at="double", min=0, max=1, dv=1)
    cmds.setAttr(ctrlSwitch+'.Dynamic_Attr', lock=True)
    cmds.connectAttr(ctrlSwitch+'.dynamic', dynamicCTL+'.dynamic')
    cmds.connectAttr(ctrlSwitch+'.stiff', dynamicCTL+'.stiff')
    cmds.connectAttr(ctrlSwitch+'.damp', dynamicCTL+'.damp')
    cmds.connectAttr(ctrlSwitch+'.start', dynamicCTL+'.start')
    
    listFWD = cmds.ls(nameGuide+'fwdFk*'+CTL_name)
    listRVS = cmds.ls(nameGuide+'rvsFk*'+CTL_name)
    dynamicJNTList = cmds.ls(nameGuide+'Dyn*'+JNT_name)
    dynamicJNT = []
    listFWDOffset = []
    
    for a in listFWD:
        off = groupOffset(a)
        listFWDOffset.append(off)
    
    for b in listRVS:
        groupOffset(b)
        
    for u in dynamicJNTList:
        dynamicJNT.append(str(u))
    
    for o in range(totalNum):
        cmds.connectAttr(dynamicJNT[o]+'.r', listFWDOffset[o]+'.r')
    
    # Another Random Shit
    
    cmds.connectAttr(ctrlSwitch+'.ShowFK', nameGuide+'Fk'+GRP_name+'.visibility')
    cmds.connectAttr(ctrlSwitch+'.ShowIK', nameGuide+'Ik'+GRP_name+'.visibility')
    
    print ('')
    print ('---Done---')
    print ('')

def createTentacleInfo_GT():
    print ('')
    print ('--- Create Tentacle System ---')
    print ('Function: Create Chain for Tantacle Needs')
    print ('How to Use:')
    print ('    -Please Tools [Control Library]')
    print ('    -Please Create Guide')
    print ("    -Last Guide Doesn't Count")
    print ('    -Follow Direction X')
    print ('    -Run the System')

# --- Windows Setting ---

def resizeMainWindow():
    pass

if (cmds.window(windowName_GT, exists=True)):
    cmds.deleteUI(windowName_GT)

cmds.window(windowName_GT, title=windowTitle_GT, iconName=windowName_GT, resizeToFitChildren=1, h=sizeHeight_GT, w=sizeWidth_GT)

windowWidth = cmds.window(windowName_GT, query=True, width=True)
windowHeight = cmds.window(windowName_GT, query=True, height=True)

cmds.columnLayout('mainWindowColumnLayout', adjustableColumn=1, w=windowWidth)
cmds.scrollLayout('mainWindowScrollLayout', rc='resizeMainWindow()', minChildWidth=sizeWidth_GT, hst=0, vst=0, h=windowHeight, w=windowWidth)

mWS1m = windowWidth/4-holderSize_GT/2
mWS2m = (windowWidth-mWS1m)/1-(holderSize_GT/1+1)
mWS3m = (windowWidth-mWS1m)/2-(holderSize_GT/2+1)
mWS4m = (windowWidth-mWS1m)/3-(holderSize_GT/3+1)
mWS5m = (windowWidth-mWS1m)/4-(holderSize_GT/4+1.5)
mWS6m = (windowWidth-mWS1m)/5-(holderSize_GT/5+2)

menuWidthSize1 = mWS1m
menuWidthSize2 = mWS1m, mWS2m+1
menuWidthSize3 = mWS1m, mWS3m, mWS3m
menuWidthSize4 = mWS1m, mWS4m, mWS4m, mWS4m
menuWidthSize5 = mWS1m, mWS5m, mWS5m, mWS5m, mWS5m+1.5
menuWidthSize6 = mWS1m, mWS6m, mWS6m, mWS6m, mWS6m, mWS6m+2

cWS1m = (windowWidth/1)-(holderSize_GT/1+2)
cWS2m = (windowWidth/2)-(holderSize_GT/2+2)
cWS3m = (windowWidth/3)-(holderSize_GT/3+2)
cWS4m = (windowWidth/4)-(holderSize_GT/4+2)
cWS5m = (windowWidth/5)-(holderSize_GT/5+2)
cWS6m = (windowWidth/6)-(holderSize_GT/6+2)

colomnWidthSize1 = cWS1m+4
colomnWidthSize2 = cWS2m, cWS2m+4
colomnWidthSize3 = cWS3m, cWS3m, cWS3m+3
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

colomnWidthSize2SP = cWS2m+90, cWS2m-86
colomnWidthSize3SP = cWS3m-20, cWS3m+43, cWS3m-20

cmds.rowLayout(numberOfColumns=1, columnWidth1=(colomnWidthSize1), columnAttach=[(1, 'both', 0)])
cmds.text(label="Create Guide", align="center")
cmds.setParent('..')

cmds.rowLayout(numberOfColumns=1, columnWidth1=(colomnWidthSize1), columnAttach=[(1, 'both', 0)])
cmds.text(label="--------------------------------------------------------------------------", align="center")
cmds.setParent('..')

cmds.rowLayout(numberOfColumns=1, columnWidth1=(colomnWidthSize1), columnAttach=[(1, 'both', 0)])
cmds.text(label="Name of Guide", align="center")
cmds.setParent('..')

cmds.rowLayout(numberOfColumns=1, columnWidth1=(colomnWidthSize1), columnAttach=[(1, 'both', 0)])
cmds.textField("guideNameField")
cmds.setParent('..')

cmds.rowLayout(numberOfColumns=1, columnWidth1=(colomnWidthSize1), columnAttach=[(1, 'both', 0)])
cmds.text(label="Number of Guide", align="center")
cmds.setParent('..')

cmds.rowLayout(numberOfColumns=1, columnWidth1=(colomnWidthSize1), columnAttach=[(1, 'both', 0)])
cmds.intField("guideNumberField", value=5)
cmds.setParent('..')

cmds.rowLayout(numberOfColumns=1, columnWidth1=(colomnWidthSize1), columnAttach=[(1, 'both', 0)])
cmds.button("createGuide", label="Create Guide", command="createGuide()", height=35)
cmds.setParent('..')

cmds.rowLayout(numberOfColumns=1, columnWidth1=(colomnWidthSize1), columnAttach=[(1, 'both', 0)])
cmds.text(label="#-------------------------------------------#", align="center")
cmds.setParent('..')

cmds.rowLayout(numberOfColumns=2, columnWidth2=(colomnWidthSize2SP), columnAttach=[(1, 'both', 0), (2, 'both', 0)])
cmds.button("createReverseFKIK", label="Create Reverse FKIK", command="createReverseFKIK_GT()", height=35)
cmds.button('createReverseFKIKInfo', label='!', command='createReverseFKIKInfo_GT()', height=35)
cmds.setParent('..')

cmds.separator(w=sizeWidth_GT-holderSize_GT, h=10)

cmds.rowLayout(numberOfColumns=2, columnWidth2=(colomnWidthSize2SP), columnAttach=[(1, 'both', 0), (2, 'both', 0)])
cmds.button("createSwitchFKIK", label="Create Switch FKIK", command="createSwitchFKIK_GT()", height=35)
cmds.button('createSwitchFKIKInfo', label='!', command='createSwitchFKIKInfo_GT()', height=35)
cmds.setParent('..')

cmds.separator(w=sizeWidth_GT-holderSize_GT, h=10)

cmds.rowLayout(numberOfColumns=2, columnWidth2=(colomnWidthSize2SP), columnAttach=[(1, 'both', 0), (2, 'both', 0)])
cmds.button("createSwitchSpline", label="Create Switch FKIK Spline", command="createSwitchSpline_GT()", height=35)
cmds.button('createSwitchSplineInfo', label='!', command='createSwitchSplineInfo_GT()', height=35)
cmds.setParent('..')

cmds.separator(w=sizeWidth_GT-holderSize_GT, h=10)

cmds.rowLayout(numberOfColumns=3, columnWidth3=(colomnWidthSize3SP), columnAttach=[(1, 'both', 0), (2, 'both', 0), (3, 'both', 0)])
cmds.text(label='Object', align='center')
cmds.textField('squashObjectNameText')
cmds.button('squashObjectNameLoad', label='@', command='squashObjectNameLoad_GT()')
cmds.setParent('..')

cmds.rowLayout(numberOfColumns=2, columnWidth2=(colomnWidthSize2SP), columnAttach=[(1, 'both', 0), (2, 'both', 0)])
cmds.button("createSquash", label="Create Squash", command="createSquash_GT()", height=35)
cmds.button('createSquashInfo', label='!', command='createSquashInfo_GT()', height=35)
cmds.setParent('..')

cmds.separator(w=sizeWidth_GT-holderSize_GT, h=10)

cmds.rowLayout(numberOfColumns=2, columnWidth2=(colomnWidthSize2SP), columnAttach=[(1, 'both', 0), (2, 'both', 0)])
cmds.button("createDynamicHair", label="Create Dynamic Hair", command="createDynamicHair_GT()", height=35)
cmds.button('createDynamicHairInfo', label='!', command='createDynamicHairInfo_GT()', height=35)
cmds.setParent('..')

cmds.separator(w=sizeWidth_GT-holderSize_GT, h=10)

cmds.rowLayout(numberOfColumns=3, columnWidth3=(colomnWidthSize3SP), columnAttach=[(1, 'both', 0), (2, 'both', 0), (3, 'both', 0)])
cmds.text(label='Object', align='center')
cmds.textField('skirtJointNameText')
cmds.button('skirtJointNameTextLoad', label='@', command='skirtJointNameTextLoad_GT()')
cmds.setParent('..')

cmds.rowLayout(numberOfColumns=2, columnWidth2=(colomnWidthSize2SP), columnAttach=[(1, 'both', 0), (2, 'both', 0)])
cmds.button("createSkirt", label="Create Skirt System", command="createSkirt_GT()", height=35)
cmds.button('createSkirtInfo', label='!', command='createSkirtInfo_GT()', height=35)
cmds.setParent('..')

cmds.separator(w=sizeWidth_GT-holderSize_GT, h=10)

cmds.rowLayout(numberOfColumns=2, columnWidth2=(colomnWidthSize2SP), columnAttach=[(1, 'both', 0), (2, 'both', 0)])
cmds.button("createTentacle", label="Create Tentacle", command="createTentacle_GT()", height=35)
cmds.button('createTentacleInfo', label='!', command='createTentacleInfo_GT()', height=35)
cmds.setParent('..')

cmds.showWindow()
