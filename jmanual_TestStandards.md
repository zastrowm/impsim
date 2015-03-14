# Test Standards #
  * JUnit4 style.
  * Classes no longer need to extend TestCase.
  * No need to have "test" in method name. Use @Test annotation instead.
  * Using this new format, there should be no more try-catch blocks.
  * For tests not yet implemented, use the annotation "@Ignore("Descriptive message including name of method under test and explanation as to why it is currently ignored.").

```
Correct (JUnit4):
public class TestDoof {  // does not extend TestCase
    @Test   // annotation letting Junit4 know this is a test
    public exceptionFromDoofiness() {   // no need to have "test" in method name
    . . .
    }
}

Incorrect (JUnit3):
public class TestDoof extends TestCase {
    public testExceptionFromDoofiness {
    . . .
    }
}
```

  * When an exception is expected, use the ExpectedException object:

```
Correct (JUnit4):
public class TestDoof {

    @Rule        // annotation and this object are what catch and test the exceptions
    ExpectedException thrown = ExpectedException.none();

    @Test
    public exceptionFromDoofiness() {
        // must be the line preceding the call that throws, this will catch an exception of type DoofException
        thrown.expect(DoofException.class);  
        new Doof(new BadParam());
    }
}

Incorrect (JUnit3):
public class TestDoof extends TestCase {
    public testExceptionFromDoofiness {
        try {
            new Doof(new BadParam());
        } catch (DoofException de) {
            /* Doof is working correctly since it threw the right exception */
        }
    }
}
```

  * We are no longer asserting 'fail()' in a catch block. Let the exception be thrown from the test method.  The framework will catch this and it is still easily noticed as a fail.


```
Correct:
public class TestDoof {
    @Test
    public exceptionFromDoofiness() throws DerrException { // test fails when exception bubbles out
        new Doof(new WeirdParam());  // exception triggered here
    }
}

Incorrect:
public class TestDoof extends TestCase {
    public testExceptionFromDoofiness {
        try {
            new Doof(new WeirdParam());
        } catch (DerrException de) {
            fail("Caught derr exception and shouldn't have");
        }
    }
}
```