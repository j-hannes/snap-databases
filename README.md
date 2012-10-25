Uebersicht ueber Haskell Datentypen
===================================

So etwa koennte eine Modellierung eines Datenmodells in das Haskell Typsystem
stattfinden:


Szenario
--------

Ein ERD eines Anwendungsszenarios, nur als Beispiel, wird wahrscheinlich noch
'ummodelliert'.

![ERD](https://github.com/J-Hannes/snap-databases/blob/master/DataModel.png?raw=true)


Haskell Datentypen
------------------

Die Entitaeten koennten dann zum Beispiel so in Haskell modelliert werden
(hier mit Attributen). Diese entsprechen algrbraischen Datentypen

```haskell
data User = User
  { firstname :: String
  , lastname  :: String
  , email     :: String
  , school    :: School
  , authUser  :: AuthUser
  }

data School = HtwkLeipzig

data Tutor = Tutor
  { user    :: User
  , courses :: [Course]
  , groups  :: [Group]
  , tasks   :: [Task]
  }

------------------------------------------------------------------------------
data Course = Course
  , coursename  :: String
  , semester    :: Semester
  , enrollTime  :: TimeFrame
  , assignment  :: Maybe Rational
  , assignments :: [Assignment]
  } 

data Semester = SS12

------------------------------------------------------------------------------
data Assignment = Assignment
  { status            :: Status
  , solutionsAccepted :: TimeFrame
  }

data Status = Mandatory | Optional

------------------------------------------------------------------------------
data Task = Task
  { taskname    :: String
  , scoring     :: Scoring
  , tag         :: String
  , config      :: String
  , signature   :: String
  , assignments :: [Assignment]
  }

-- etc.

```

Mehr Informationen zum Weiterlesen gibt es zum Beispiel
[hier](http://learnyouahaskell.com/making-our-own-types-and-typeclasses) (sehr
gut verstaendliche Referenz im Uebrigen).



Interpretation
--------------

Vielleicht koennten man diese Datenstrukturen auch mit Records in der JSON
Notation vergleichen.


