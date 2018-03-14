# Method Call Tree

These traces have been collected with [yajta](https://github.com/diverse-project/yajta) in its released 1.1.0.
They are traces of JUnit test execution with maven. (One file per test classes, one directory per project)
They log only the classe and method name (and formal parameters) of methods called for classes of the project.

Therefor the execution of the following test class:

```Java
package org.myPackage
class MyTest {
	@Test
	public void test() {
		int i = 1;
		assertEquals(i,1);
	}
}
```

would produce
```json
{"name":"Threads", 
"yajta-version": "1.1.0", 
"serialization-version": 0, 
"children":[
	{"class":"null", "method":"main", "children":[
		{"class":"org.myPackage.MyTest", "method":"test()", "children":[]}
	]}
]}
```

and no traces of `assertEquals` as it is not a method from `org.myPackage`. (Note that a method from a class `org.myPackage.subPackage.MyCLass` will be logged.
(The first node (named `Threads`) contains as children a node for each thread whose `class` is `"null"` with `method` containing the name of the thread (In this example `main`, as we monitor only the main thread).

## Projects traced

 * commons-lang 3.3.2
 * commons-codec 1.10
 * Gson 2.3.2
