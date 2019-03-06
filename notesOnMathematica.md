# Expected Mathematica Code

For PX4514 (Mathematical Modelling)

## Global Variables
### global constants
 - idealPosition
 - positionCoordinates[]  % this should be the coordinates of the ideal position in which the attacker would contact the ball
 - basePositionDifficulty[]
	
### globally required input variables
 - ownPoints
 - oposingPoints
 - remaintingSets
 - setterPosition
 - setterCoordinates
 
### globally required processed variables
 - distanceFromIdeal: setterCoordinates to idealPosition
 - distanceToRun: setterCoordinates to setterPosition
 - pressure= [Pressure](#pressure)

## Functions:

### Pressure()
inputs
 - ownPoints
 - oposingPoints
 - remaintingSets 
 
  return
 - calculating(TODO)
 - default=0

### PositionDifficulty(p)
 inputs
 - position: p

 return
 - distanceFromIdeal * positionCoordinates[p]
 - default=?

### PositionIsValid(p)
 inputs
 - position: p

 return
 - 0: setter is not allowed to set to this position
 - 1: setter is allowed to set to this position

### SetToScore(p)
 inputs
 - position: p

 return
 - (PositionDifficulty(p) + pressure + distanceToRun) * PositionIsValid(p)

### AttackerScore(p)
 inputs
 - position: p

 return
 - (basePositionDifficulty[p] + pressure) * SetToScore(p)

### CalculateAllScores
 inputs
 - none

 return
 - value[]= AttackerScore(position) : for all position

### CalculateGlobalVariables()
 input
 - none

 does
 - gloabal distanceFromIdeal= EuclideanDistanceOf(setterCoordinates,idealPosition)
 - global distanceToRun= EuclideanDistanceOf(setterCoordinates,setterPosition)
 - global pressure= Pressure()

 return
 - none
 
### Run Program(ownP, oposP, remaining, position, coordinates)
 inputs
 - ownPoints: ownP
 - oposingPoints: oposP
 - remaintingSets: remaining
 - setterPosition: position
 - setterCoordinates: coordinates

 does
 - global ownPoints= ownP
 - global oposingPoints= oposP
 - global remaintingSets= remaining
 - global setterPosition= position
 - global setterCoordinates= coordinates
 - CalculateGlobalVariables()

 return
 - CalculateAllScores()
