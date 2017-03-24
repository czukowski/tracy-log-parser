LogParser COM Plug-In for reading Tracy Debugger Log Files
==========================================================

This package makes it possible to view and query log files written by [Tracy Debugger][tracy],
part of the [Nette Framework][nette] for PHP, using [Microsoft Log Parser][logparser].

A COM Plug-In is implemented to parse Tracy log files. Obviously, it'll work only on Windows.

Installation and Usage
----------------------

After you've downloaded the SCT file from this package, it must be registered using the following syntax:

```sh
regsvr32 Tracy.LogParser.Scriptlet.sct
```

To use it, run Log Parser with parameters that tell it to use this COM Plug-In, for example:

```sh
logparser "SELECT * FROM 'C:\foo\exception.log' WHERE TO_DATE(DateTime) = SYSTEM_DATE()" -i:COM -iProgID:Tracy.LogParser.Scriptlet
```

About
-----

Tracy log files contain the following notable features:

```
DateTime Message  @  Request [ @@  ExceptionFile]
```

 * `DateTime` in `[YYYY-MM-DD HH:MM:SS]` format (wrapped in square brackets)
 * `Message` is any text message, for error and exception logs this is the respective error message
 * `Request` is a request URL or CLI command that have originally executed the script, separated by ` @ `
    from the previous part
 * `ExceptionFile`, only found in exception logs, states a file name, in which exception details, such
    as stack trace, can be found. It is separated by ` @@ ` from the previous part.

This COM Plug-In is heavily based on tutorials by [Robert McMurray][robmcm] on Microsoft blog, especially:

 * [Advanced Log Parser Charts Part 4 – Adding Custom Input Formats][tutorial-part-4]
 * [Advanced Log Parser Part 6 – Creating a Simple Custom Input Format Plug-In][tutorial-part-6]
 * [Advanced Log Parser Part 7 – Creating a Generic Input Format Plug-In][tutorial-part-7]

It would not have been possible to create this Plug-In without these. Also, last time I was writing
anything in VB was well more than 10 years ago, so there are bound to be some gotchas with this work.


 [logparser]: https://technet.microsoft.com/en-us/scriptcenter/dd919274.aspx
 [nette]: https://nette.org/en/
 [robmcm]: https://social.msdn.microsoft.com/profile/robmcm
 [tracy]: https://tracy.nette.org/en/
 [tutorial-part-4]: https://blogs.msdn.microsoft.com/robert_mcmurray/2012/05/25/advanced-log-parser-charts-part-4-adding-custom-input-formats/
 [tutorial-part-6]: https://blogs.msdn.microsoft.com/robert_mcmurray/2013/02/27/advanced-log-parser-part-6-creating-a-simple-custom-input-format-plug-in/
 [tutorial-part-7]: https://blogs.msdn.microsoft.com/robert_mcmurray/2013/02/28/advanced-log-parser-part-7-creating-a-generic-input-format-plug-in/
