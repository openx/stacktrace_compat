# Changelog
All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](http://keepachangelog.com/en/1.0.0/)
and this project adheres to [Semantic Versioning](http://semver.org/spec/v2.0.0.html).

## [1.0.2] - 2019-01-19
### Fixed
- unwarranted import of rebar3_hex plugin in library consumers

## [1.0.1] - 2018-07-11
### Fixed
- generation of unsafe stacktrace variables upon the existence of
  multiple try-catch blocks, within a function, with the same hierarchy
  (and equivalent but more contrived cases.)
  E.g, in the following transformed code:
```
function() ->
    try error(foobar)
    catch
        error:foobar:StacktraceCompat444353487_1 ->
            {foobar, StacktraceCompat444353487_1}
    end,

    try error(foobar)
    catch
        error:foobar:StacktraceCompat444353487_1 ->
            % ^^ This unsafe use of 'StacktraceCompat444353487_1'
            % no longer occurs; the generated variable name
            % would now be 'StacktraceCompat444353487_2'.
            {foobar, StacktraceCompat444353487_1}
    end.
```

## [1.0.0] - 2018-06-23
### Added
- ability of replacing most erlang:get_stacktrace() instances with variable captures in OTP 21+
