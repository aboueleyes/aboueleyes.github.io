@def title = "VHDL"
@def tags = ["guc"]
@def hascode = true
# VHDL  بصمجة  

\tableofcontents 

## Basic Entity

```vhdl
ENTITY name IS 
    port(_first, _second : in std_logic;
    _Q : out std_logic);
```

### Input and Output
- `Bit`  0 & 1 only
- `STD_LOGIC` 0, 1,  X unknown, Z high Impedance
- `STD_LOGIC_VECTOR`($i$ downto $j$) instead of repeating `i > j`
- `Integer Range` $i$ To $j$. To prevent overflow.

### Types of variabels 
- `In` assigned once (Read ONLY) & it's only input of a function.
- `Out` assigned once (Write only) & it's only output of a function.
- `Buffer` used when particular port need to be read & written 
- `INOUT` it's like buffer but allows but allow the port to be connected to mulitpule source.


### Generic 
`Generic` is used to create a variable that can take on different values
depending on size of component you're creating.

#### Example
```
ENTITY _name IS
    Generic (_N : Integer := _defaultValue)
    Port (_X: IN STD_LOGIC_VECTOR (_N downto 0);
    _Y OUT STD_LOGIC_VECTOR(_N + 1 downto 0));
```

### Use Entity in another place

1. `component` present in architecture of the other Entity
2. `Package` after writing the entity & arch 

```
Package _Pname IS
    component _name IS
        Port (...);   <- same as entity.
    end component;
end _Pname;
```

Import it in the other place.

```
library work;
use work._Pname.all;
```

## Architecture 

### Signal 

- `signal` variable that os neither input nor output.
- created before `begin`
- `signal s1, s2 : STD_LOGIC;`

### Component 
- allows a previously created entity to be used as a component in a bigger architecture.
- created before begin 
```
Component fulladd 
    PORT (x, y : IN STD_LOGIC, 
    s : out STD_LOGIC);
END Component;
```

### Port Map

- used to create interconnections between inputs, components, signals, ..etc.
- created after `begin`.
- `stage0: fulladd portmap(x, y, s);`


### Select Signal Assignmnets 

- allows signal to be assigned one of several values.
- created after `begin`.
- keywords `with`, `when`, `others`, 'select'

```
with _S Select
    f <= w0 when '0'
        w1 when others;
```
### Conditional signal assignment

- keywords `when`, `select`
- `f <= w0 when s='0' else w1;`

### For Generate

- created after `begin`

```
LABEL: FOR i IN 0 TO M Generate
    Component_label: PORT MAP (..);
END Generatel
``` 

### IF Generate

- must be inside FOR Generate

```
genertae_label: if i = _value Generate
    Component_label: PORT MAP(...);
END Generate;
```

### Process Statement

- created after `begin`
```
Process(_v1, _v2, ..) <- sensetivity list 
BEGIN 
    IF _cond THEN 
        _statement;
    ELSE 
        _statement;
    END IF;
END PROCESS;
```
- `x'Event` 
```
Process(clk, D)
BEGIN 
    IF clk'Event AND clk = '1' Then
        Q <= D;
    END IF;
End Process;
```

- `wait until` sensitivity list is omitted 
```
Process 
BEGIN 
    wait until clk'Event AND clk = '1'
        Q <= D;
End Process;
```

## Type 
- to create user defined signal type 
- implemented before begin

```
Type _myType IS (.., .., ..);
Signal _signal : _myType;
```

## User defined attribute 

- used to associate some desired type of info with an object in `VHDL`

```
Type _myType IS (.., .., ..);
Attribute ENUM_ENCODING : String;
Attribute ENUM_ENCODING OF _myType IS "         ";
Signal _signal : _myType;
```

## Case Statement

- created after `begin`

```
Case _variable IS 
    when _v1 => 
        _statement;
    when _v2 => 
        _statement;
    when others => 
        _statement;
End Case;
```

## Generic Map

- is similar to the port map used to assign values to the generic 
parameters of the sub-circuit.

- after `begin`

```
stage0 : _fnName Generic Map (_fnVal) Port Map(_in, _out);
```

## Loop 
```
loop-label : for _i in _k downto
    _statement;
End loop;
```

## Functions 
### Syntax 

```
[kind] function fnName [(parameter_declaration)] 
return type_name is [function_declartian]
begin 
    sequentail_statements
end [function][function_name]
```

```
function func1 (Signal A, B : in Integer; MaxValue: Integer) return Integer is 
variable Temp, Max: Integer;
BEGIN
    Temp := A + B;
    if Temp < MaxValue then
        Max := MaxValue;
    else 
        Max := MaxValuel
    end if;
    return Max;
end func1;
```
- function is calld `v <= func1(m, n, 12);`


> Thanks to the riginal author.
