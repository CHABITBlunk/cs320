# tail recursion

### definition

- a recursive fn in which last task of fn is recursive call

### example in prolog

```prolog
member(X,[X|Y]).
member(X,[Head|Tail]) :- member (X,Tail).
```

this means X is in a list if it's the first element of a list

X is a variable

```prolog
List: [First_Element | Rest_of_List]
List: [Head | Tail]
```

Tail is also a List
this code is also a definition of what it means for X to be a member of a List

### prolog

- declarative, not procedural
  - programmer specifies what goals
