Overview over Haskell data types
================================

Brief example of some Haskell data structures.


Scenario
--------

The following diagram gives an overview over entities in the usage scenario.

![ERD](https://github.com/J-Hannes/snap-databases/blob/master/DataModel.png?raw=true)


Haskell DS
----------

This could be converted to the following Haskell data structures (example,
snippet):

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

data Student = Student
  { user        :: User
  , solutions   :: [Solution]
  , enrollments :: [Enrollment]
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

data Scoring = Increasing | Decreasing | None


------------------------------------------------------------------------------
data Solution = Solution
  { task    :: Task
  , content :: String
  , score   :: Int
  , time    :: UTCTime
  }


------------------------------------------------------------------------------
data Enrollment =
  { time    :: UTCTime
  }


------------------------------------------------------------------------------
data Group = Group
  { course      :: Course
  , groupname   :: String
  , capacity    :: Capacity
  , enrollments :: [Enrollment]
  }


------------------------------------------------------------------------------
data TimeFrame = TimeFrame
  { from :: UTCTime
  , to   :: UTCTime
  }
```
