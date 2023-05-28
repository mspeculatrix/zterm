# zterm

A Go-based terminal to communicate with the Zolatron 6502 computer. Intended to be run on the Raspberry Pi extension board.

This replaces the earlier `zolaterm` program.

Usage:

`zterm [-a] [-p] [-t] [-f ]`

- -a append to log file. Otherwise, overwrite.
- -f filename to use for log file. Very little error checking is done, so be careful.
- -p port to use - eg, ttyACM0
- -t test message to send using command '/t'

The program works in two modes: CMD and RAW.

## CMD MODE (default)

This is intended for working with commands in ZolOS, but will work equally well with any programs designed to deal with line-based input.

In CMD mode, text is sent to the Zolatron only when <return> is entered - ie, you send a line at a time. The carriage return is converted into a Null (ASCII 0), which ZolOS interprets as an end of transmission.

Characters are converted to uppercase before sending.

This mode is not good for any programs that need to deal with one character at a time - ie, which need to read individual characters from the keyboard.

### CMD mode - Local Commands

There are several local commands that are handled by Zterm (and not sent to the remote machine). These are prefixed with '/' and are:

```
/f  Show log filename
/g  Toggle logging
/h  Show this list of commands
/r  Reset the Zolatron
/s  Show settings
/q  Quit Zterm
/w  Switch to RAW mode
```

## RAW MODE

In RAW mode, each individual keypress is sent immediately to the Zolatron.

RAW mode itself has two modes which determine how the <return> key is handled. These are:

- NULL mode - the carriage return (ASCII 13) is converted to Null (ASCII 0).
- RTN mode - the carriage return (ASCII 13) is sent directly to the Zolatron.

You can toggle between these two modes using F2.

If you're using RTN mode, you can send a Null character (to indicate end of transmission) by pressing F4.

### RAW Mode - Function Keys

```
<esc>/F1  switch to CMD mode
F2        toggle NULL/RAW mode for <return> key
F3        show status
F4        send NULL
F8        reset Z64
F10       quit
```
