Uebersicht ueber Haskell Datentypen
===================================

Hier mal eine grobe Uebersicht ueber Record-Datentypen in Haskell. Diese ist
nicht vollstaendig, allerdings ist eine komplette Uebersicht ueber alle
Datentypen in Haskell doch recht umfangreich, da das Typsystem in Haskell eine
eigene Programmiersprache darstellt (ja, selbst Typen habe eigene Typen).

Haskell ist streng statisch getypt, d.h. jeder Wert hat zur Uebersetzungszeit
des Programmes einen genau festgelegten Typ. Dieser muss im Programm jedoch
nicht explizit angegeben werden (wie zum Beispiel in Java), sondern kann von
einem Inferenzsystem *ausgerechnet* werden.

In Haskell gibt es sowohl primitive Datentypen (Integer, String, etc.), aber
auch komplexe Datentype (Records) und algebraische Datentypen, Listen spielen
in Haskell eine zentrale Rolle.


Szenario
--------

Ein ERD des Anwendungsszenarios (eine Variante).

![ERD](https://github.com/J-Hannes/snap-databases/blob/master/DataModel.png?raw=true)


Haskell Datentypen
------------------

Die Entitaeten koennten dann zum Beispiel so in Haskell modelliert werden
(hier mit Attributen).

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
vergleichen. Dann wuerde ein Wert, der einem bestimmten Typ entspricht, ein
Objekt mit genau festgelegtem *Bauplan* (also Anzahl und Art der Attribute)
entsprechen.

```javascript
var authUsers = [
  {
    'userId': 1,
    'username':  'test',
    'password':  'pass',
    'lastLogin': '2010-09-28 13:45:32 GMT',
    // ...
  },
  // more authUsers
];

var users = [
  {
    'firstname': 'Max',
    'lastname':  'Muster',
    'email':     'max.muster@email.com',
    'school':    schools[0],
    'authUser':  XXX
  },
  // more users
];

var schools = ['HTWK Leipzig', /* more schools */];

var tutors = [
  {
    'user':    users[0],
    'courses': [courses[1], courses[2]],
    'groups':  [groups[0],  groups[4], groups[5]],
    'tasks':   [tasks[1],   tasks[2],  /* ... */]
  },
  // more tutors 
];

var students = [
  {
    'user': [users[3]],
    'solutions': [solutions[13], solutions[14],
    'enrollments': [enrollments[4], enrollments[43]]]
  },
  // more students
];
```
