# difftest-runner

### So.... What's that?
I think you'd be hard pressed to find something in Software Engineering that doesn't need or couldn't benefit from some automated testing.  It sucks to make a trivial change to something and not be able to have an equally trivial answer to the question "Well, I wonder if that change broke anything?".  So with that, testing is a must.  

  Testing, however can be done in a bunch of different ways. The simplest 
approach to writing a test is pretty straight forward:

* do something
* see what happens
* decide if that's good, or make changes until it is so
* record that output for later comparison

Using a test is even easier:

* remember that thing you did? do it again
* compare the output to what you decided was good (above)

This is the gist of damn near every testing framework in the world, and they
all have various approaches to all aspects of that process, and generally try
and be available in every single environment you can imagine. Here we try to
ignore how, what, and environment and focus only on facilitating the
'given something done' what does it's output look like and, does that output
look like what it used to.

#### All that is the long winded version of this
difftest-runner is a series of scripts that aim to make the execution of and collection of the output from a body of tests (scripts) easily repeatable
such that you can compare future executions to executions deemed 'good'.

#### Or
difftest-runner helps run and track the output of test scripts so you can quickly
determine if things are the same as they were when you decided they were 'good'.

### Things to Know

difftest-runner is distribted using npm.  This isn't because it's javascript,
or uses node because it's not and doesn't, but because npm is easy to use and
good at this 'package and distribute' thing.

There is a specific directory structure that difftest-runner uses, mostly you
don't have to care and can just interact with this through the commands provided
but it's good to know what the hell al this is:

    difftest 
      |-tests
      |-expected
      |-results
      |-filters

In the example, the root directory is called 'difftest' this is the default
and is technically able to be changed but who wants to fuss with that.

* /difftest/tests - This directory contains the 'scripts' that are run to do
the 'testing'.  Generally I think of these items as scripts but they simply
need to be exec-able, and return some deterministic output to stdout.

* /difftest/expected - This is where the 'good' output of the scripts is stored
for future comparison.  This directory will contain a like named file for each
test found in the tests/ directory, which contains the output from the test
as considered good.

* /difftest/results - This is where the output of the last run of each test is
stored.  The directory will contain a like named file for each test that 
contains the output captured (stdout and stderr) from the most recent run
of the test.

* /difftest/filters - This contains filters to be applied to test output to
make things that vary (like time stamps) fixed so comparison of output
is simplified.

### So how do I use it

Install it *(not yet published)*

    npm install -g difftest-runner

Initialize the directory you want to have tests in, I find this to be the root 
of my repository.

    difftest init

Make a test, currently the template test is nothing more than a stub of a 
bash script.   

    difftest create my_first_test

See that the test is really there
    
    difftest show tests

Edit the test to make it do something, this relies on the environment variable
```EDITOR``` being set.
  
    difftest edit my_first_test

See that it fails (we haven't defined passing yet!)
  
    difftest run

Check the results of the last test run for my\_first\_test

    difftest show my_first_test

Tell difftest that the results of the test are good

    difftest pass my_first_test

See what victory looks like!
  
    difftest run

### TODO

* allow for the creation of custom test templates
