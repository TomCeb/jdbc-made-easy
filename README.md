# jdbc-made-easy
Lightweight JDBC library for Java.


## Purpose
Simplified JDBC usage developed and tested on Oracle database.

## Usage
Examples given in src/test/OracleMainTestEasy.java.

### Simple example

POJO with annotations
```
@EasyRow
public class TestEntity
{

	@EasyColumn(name="SOME_STRING")
	private String someString;

	@EasyColumn(name="JUST_DATE")
	private LocalDate justDate;
	
	@EasyColumn(name="SOME_INTEGER")
	private Integer someInteger;
	
	@EasyColumn(name="CURRENCY")
	private BigDecimal currency;
	
	@EasyColumn(name="STATUS",enumFactoryClass=EnumTypes.class,staticEnumMethod="statusFactory")
	private EnumTypes.Status status;

	@EasyColumn(name="TS")
	private LocalDateTime pointInTime;

    ...
    getters / setters
}
```

Invoke select:

```
    List<TestEntity> lst = new EasyPreparedStatement<>(
            "Select * From TABLE(pckTestEasyJDBC.GetTestForSelect(:string,:date,:integer))",
            connection,
            TestEntity.class,
            OracleParameterFactory.stringParameter("string").setValue("A"),
            OracleParameterFactory.dateParameter("date").setValue(new Date()),
            OracleParameterFactory.decimalParameter("integer").setValue(BigDecimal.ZERO)
            ).executeAsList();

```

More examples to come.