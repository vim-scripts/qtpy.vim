qtpy.vim
==========
A simple way of running python unit tests from within VIM based on the cursor
location.

Useful for receiving immediate feedback as you write tests, despite what test
runner or framework your project uses to run its tests.


This project was originally derived from Alfredo Deza's pytest.vim. Which is
more focused on soley running py.test unit tests. That project can be found
here: https://github.com/alfredodeza/pytest.vim

Usage
=====
To use this plugin, make sure ftplugins are enabled, via "filetype on" in your
.vimrc.

This plugin provides a single command::

    QTPY

All arguments are able to be tab-completed.

Python Objects
--------------
For running tests the plugin provides 3 arguments with an optional one. 
These arguments are::

    class
    method
    file


As you may expect, those will focus on the tests for the current class, method,
or the whole file.

If you are in a class and want to run all the tests for that class, you would
call this plugin like::

    :QTPY class

Whenever a command is triggered a small message displays informing you that
the plugin is running a certain action. In the above call, you would see 
something like this::

    Running tests for class TestMyClass

If you would like to see the complete qtpy output you can add an optional `verbose`
flag to any of the commands for qtpy. For the previous command, it would
look like::

    :QTPY class verbose

This would open a split scratch buffer that you can fully interact with. You
can close this buffer with ':wq' or you can hit 'q' at any moment in that buffer
to close it.

When tests are successful a green bar appears. If you have any number of fails
you get a red bar with a line-by-line list of line numbers and errors.

I recommend mapping keys to qtpy commands for easy running. To do so, insert
commands like this into your .vimrc::

    " QTPY
    au FileType python nnoremap <F8> :QTPY method verbose<CR>
    au FileType python nnoremap <F9> :QTPY session<CR>

    au FileType python nnoremap <silent><Leader>c <Esc>:QTPY class verbose<CR>

The 'au FileType python' ensures these mappings only occur in a python file. 

Output
------
Output is displayed in a scratch buffer. The previous test session display can
be toggled with::
    
    :QTPY session


Configuration
-------------
qtpy is configured to work with nosetests by default, however, using qtpy with 
other unit tests runners is simple. Just set the necessary variables in your
vimrc. 

For example, insert these lines into your .vimrc to use QTPY with Py.Test::

    " for use with Py.Test
    let g:qtpy_shell_command = "py.test --tb=short" "py.tests
    let g:qtpy_class_delimiter = "::"
    let g:qtpy_method_delimiter = "::"

The delimiter variables are used with constructing the test path to pass into
the test runner. Such as "py.test /testfolder/testfile.py::TestClass::TestMethod"
for the example above where the first '::' is the class_delimiter and the second
is the method_delimiter

Shell Support
-------------
This plugin provides a way to have a better shell experience when running
`verbose` or `pdb` flags by using the `Conque.vim` plugin. If you have this
most excellent piece of Vim plugin (see: http://www.vim.org/scripts/script.php?script_id=2771)
then `qtpy.vim` will use that instead of Vim's own dumb shell environment.

`clear`
-------
If for some reason you need to reset and clear all global variables that affect
the plugin you can do so by running the following command::

    :QTPY clear


License
-------

MIT
Copyright (c) 2011 Alex Meade <hatboy112 [at] yahoo [dot] com>

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.


Attribution
-------

The core functionality of this plugin was brought over from pytest.vim
Copyright (c) 2011 Alfredo Deza <alfredodeza [at] gmail [dot] com>
