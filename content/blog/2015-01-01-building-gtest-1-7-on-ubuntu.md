+++
title = "Building googletest 1.7.0 on Ubuntu"
description = "The one in which I build a C++ unit test framework because testing is important."
date = 2015-01-01

[taxonomies]
tags = ["googletest", "c++", "unit-testing"]
+++

Unit testing is awesome. Working with legacy code, not so much. Of course when
I say [legacy
code](http://www.amazon.com/Working-Effectively-Legacy-Michael-Feathers/dp/0131177052),
I actually mean what Michael Feathers means: code that has no unit tests.

A while back I was getting started with googletest on Ubuntu and ran into
[this](http://www.thebigblob.com/getting-started-with-google-test-on-ubuntu/)
great post. Sadly, the libgtest-dev package does not install the static
libraries, and the Ubuntu 14.04 repo is still stuck on the 1.6.0 version. Can we
do better (other than upgrading to 14.10)? Sure we can! Let's grab the latest
source from the [googletest website](https://code.google.com/p/googletest/) and
build our own! Of course, along the way we're going to build and run the
tests for googletest too. How meta. We're going to need `cmake`.

```shell
$ sudo apt-get install cmake
```

Unzip the googletest source in your directory of choice. I'm a big fan of using
`/usr/local/src` but it's really a personal preference. Change to that
directory and run the following cmake command to build the googletest static
libraries in release mode and the googletest tests (case matters here for the
cmake switches):

```sh
$ sudo cmake -DCMAKE_BUILD_TYPE=RELEASE -Dgtest_build_tests=ON
$ sudo make
```

Next we launch the tests like so:

```sh
$ make test
```

and you should see output that looks something like this:

```sh
Running tests...
Test project /usr/local/src/gtest-1.7.0
     Start  1: gtest-death-test_test
1/41 Test  #1: gtest-death-test_test ..............   Passed    0.84 sec
     Start  2: gtest_environment_test
2/41 Test  #2: gtest_environment_test .............   Passed    0.00 sec
     Start  3: gtest-filepath_test
3/41 Test  #3: gtest-filepath_test ................   Passed    0.01 sec
...
```

Make sure that all of the tests pass. Now it's time to toss your compiled
libraries somewhere that cmake will be able to find them:

```sh
$ sudo cp libgtest* /usr/lib
```

We're going to need to add this line to our .zshrc (or similar shell) file so
that cmake will be able to find the googletest headers.

```sh
export GTEST_ROOT="/usr/local/src/gtest-1.7.0"
```

How did I know this? Well if you look in the file
`/usr/share/cmake-2.8/Modules/FindGTest.cmake` you will find the following
section:

```cmake
find_path(GTEST_INCLUDE_DIR gtest/gtest.h
    HINTS
        $ENV{GTEST_ROOT}/include
        ${GTEST_ROOT}/include
)
```

Because we're building googletest from source in an unconventional directory,
we'll need to give cmake a hint as to where the googletest headers are.

If you didn't want to add the environment variable, you could also have passed
the location of the googletest headers as a switch to cmake:

```cmake
$ cmake -DGTEST_ROOT="/usr/local/src/gtest-1.7.0/"
```

Now we're all set. You can check everything is working by going back to
[this](http://www.thebigblob.com/getting-started-with-google-test-on-ubuntu/)
post and copy-pasta the source code and tests. Happy building!