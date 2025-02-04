# Statements

## If statements

If statements use a similar style to most programming languages and will execute their asigned code if the test placed inside returns the boolean value true. If I wanted to have something occur if, and only if, our previous `ReturnTrueOrFalse` function returned true, then you can use:

```squirrel

  if( ReturnTrueOrFalse() )
```

Conditional operators can also be used to make comparisons, such as `==` (equals), `<` (less than), `<=` (less than or equal), `!=` (not equal), etc., returning true if their condition is satisfied. For example, to execute code if a dice roll landed on 5:

```squirrel
  if( RandomInt( 6 ) + 1 == 5 )
```

Like other languages, if statements can be connected to `else if` and `else` statements. `else if` statements must be used immediately after an `if` or `else if` and will only check their condition if the preceding statements failed. `else` statements behave similarly, but always run if the preceding statements failed and must be last.

Squirrel supports ternary operations like most languages. The value of the expression depends if a condition is truthy or not. However, if not used carefully this can worsen readability.
The Syntax is `condition ? if_condition_true : if_condition_false`. This is especially useful when declaring variables or passing parameters.

```squirrel

  // shortenedUsername is "longus..."" if username is "longusername" or "short" if username is "short"
  string shortenedUsername = username.len() > 9 ? username.slice(0,6) + "..." : username;
```

## Loops

Loops are used to execute the same code n times.

### While Loops

A while loop runs as long as the condition evaluates to a truthy value.

```squirrel

  while( true )
  {
    // this will result in an endless loop because the probe condition will never be false 
  }

  while( RandomInt( 2 ) )
  {
    // This will run until a 1 is generated by chance, because squirrel treats 0 as a falsy value and 1 as truthy.
  }
```

### Do While Loop

A do while loop is the same as a while loop but the condition is checked **after** the body is executed.

```squirrel

  do
  {
    // this will execute only one time
  } while( false )
```

### For Loop

A for loop also runs until a condition is met however it provides you with a counter variable.

The Syntax is as follows: `for( int counter; condition; behaviour_after_body_execution )`

```squirrel

  // prints 0, 1, 2, 3, 4
  for( int i; i < 5; i++ )
  {
    print( i )
  }

  array<int> arr = [ 14, 2, 18, 9 ]
  // prints 14, 2, 18, 9
  for( int i; i < arr.len() * 2; i += 2 )
  {
    print( arr[i] )
  }
```
  
### Foreach Loop

A foreach loop iterates over a `table` or an `array` and executes for each entry. The loop provides you with an optional counter for arrays or key for tables.

```squirrel

  array<int> arr = [ 1, 2, 3, 4 ]
  table<string, string> map = {
    key1 = "mapped value 1",
    key2 = "mapped value 2"
  }

  // prints 0 1, 1 2, 2 3, 3 4
  foreach( int index, int value in arr )
  {
    printt( index, value )
  }

  // prints key1 mapped value 1, key2 mapped value 2
  foreach( string key, string value in map )
  {
    printt( key, value )
  }
```

## Implicit conditional behavior

Conditional statements, such as while loops and if statements, also implictly cast non-boolean inputs to booleans. For numbers, this means 0 is considered false and anything else is considered true. For instance variables like arrays and entities, `null` is considered false and anything else is considered true. For example, these inputs are considered true by the if statements:

```squirrel

  if(2)
```

```squirrel

  array somelist = [0, 1]
  if(somelist)
```

Be aware that empty arrays and strings, `[]` and `""`, are considered true by this logic.

## Formatting of actions
So great, we can loop and check things, but what can we do with this information? Squirrel uses `{}` to denote the contents of a series of actions caused by such a statement.

For example, lets make our `ReturnTrueOrFalse` function, that randomly picks either true or false, first:

```squirrel

  bool function ReturnTrueOrFalse() {
    return RandomInt(2) == 1
  }
```

Note that while functions always need `{}`, single-line `if`/`else` statements and loops do not:


```squirrel

  if(ReturnTrueOrFalse())
    printt("Only called if true")
```

Now let's make a more complicated function that will use the previous script to determine true or false, printing a list each time it returns true:

```squirrel

  array<int> someinformation = [1,2,3,4,5,6]
  void function ThisDoesStuff(){
    while(ReturnTrueOrFalse()){
      foreach( int information in someinformation){
        printt(information)
      }
    }
  }
```
