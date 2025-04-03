# cpp header parser for rttr

## info
This project was created as a way to generate reflection files for rttr

- Parses Namespaces, Class, Enums Methods, Properties
- Parses the directories specified
- Creates generated files in the output directory specified
- Detects macros in header files to parse sections of a class

## macros
These are the macros used for parsing:
- DECALARE_(CLASS|STRUCT|ENUM)(...)
- DECLARE_FUNCTION(...)
- DECLARE_PROPERTY(...)

Note: Each macro takes in arguments that is used to generate rttr metedata

```
[section]

DECLARE_STRUCT(MetaDataName = MetaDataValue)
struct REFLECTED_STRUCT
{
	DECLARE_FUNCTION()
	bool IsReflected();

	DECLARE_FUNCTION()
	void SetIsReflected(bool arg){}

public:
	DECLARE_PROPERTY()
	int Property0 = 0;
private:
	DECLARE_PROPERTY(ReadOnly)
	float Property {1};
};
```

### properties

Reflected properties uses built in meta data to further reflect a property
The built in metadata it looks for include the following:
```
DECLARE_FUNCTION()
void SetValue(float x);

DECLARE_FUNCTION()
float GetValue() const;

DECLARE_PROPERTY(Setter = SetValue, Getter = GetValue)
float Property;

DECLARE_PROPERTY(Getter = GetValue)
float Property;

```
```
DECLARE_PROPERTY(Policy = rttr::property::policy)
```
```
DECLARE_PROPERTY(ReadOnly, AccessModifier)
```

## app arguments
- --input main directory to find h files
- --output directory to ouput generated files to
- --include{multiple} - other directories to include in parsing
```
exe -input "directory" --output "generated" --include "directory2" --include "directory3"
```
Requires the rttr library to be used for the project the generated files are used for
RTTR : https://github.com/rttrorg/rttr | https://www.rttr.org/