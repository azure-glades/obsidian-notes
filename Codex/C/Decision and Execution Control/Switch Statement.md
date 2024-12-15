[[Decision Control]]

Switch statements are much faster and clearer if-else ladders.
```c
switch(var)
{
	case val1:
		//statement
		break;
	case val2:
		//statement
		break;
	default:
		//statement
		break:
}
```
* *break* exits the switch statement
* *default*  is executed when no case is matched. 
* *default*  can be placed at any portion of the switch statement and does not hinder flow.
* Only 1 *default*  is permitted per switch statement
* Nested switch is allowed.