
# Robot Framework

## Multiple Action for TearDwon
ref. [How to make multi-lines test setup or teardown in RobotFramework without creating new keyword?](http://stackoverflow.com/questions/22691941/how-to-make-multi-lines-test-setup-or-teardown-in-robotframework-without-creatin)

    Test Case
      [Teardown]  Run Keywords  Teardown 1  Teardown 2
    or also

    Test Case
      [Teardown]  Run Keywords  Teardown 1  
      ...                       Teardown 2 
    and with arguments

    Test Case
      [Teardown]  Run Keywords  Teardown 1  arg1  arg2
      ...         AND           Teardown 2  arg1