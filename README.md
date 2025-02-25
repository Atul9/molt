# Molt -- More Or Less TCL

The general notion is to build a minimal version of TCL for embedding in Rust
apps.  See [The Molt Book](https://github.com/wduquette/molt-book) for details
and user documentation.

## Building

To build Molt:

*   Install the latest stable version of Rust (1.35.0 at time of writing)
*   Clone this repository
*   To build:

```
$ cd .../molt
$ cargo build
```

* To run the interactive shell

```
$ cargo run shell
```

* To run the language test suite

```
$ cargo run test test/all.tcl
```

## TODO Items

*   Integrate the new Value type into Molt:
    *   Look at how to best store proc details for efficient execution.
    *   Ponder the MoltList API, and consider how to make it cleaner
        *   list! macro to build lists from things that implement `Into<Value>`?
    *   Consider whether to replace Value's two RefCell's with one.
    *   Consider whether var names should be stored as Values.
    *   Consider whether molt::MoltFloat, molt::MoltInt, and molt::MoltList should be
        molt::Float, molt::Int, and molt::List.
        *   Yeah, probably.
*   Need to define some standard benchmarks so when I work on performance-related things
    I can track it.
    *   `time` command.
        *   Use std::time::Instant and std::time::Duration
    *   See core.tcl-lang.org/tclbench/home for the standard Tcl benchmarks.
        This code won't work directly in molt at this point, but I can look at it for
        examples.
* Issues from wduquette/molt.
* Add complete tests for the existing Tcl commands.
    * "catch"
    * "foreach"
    * "global"
    * "incr"
    * "join"
    * "lindex"
    * "list"
    * "llength"
    * "set"
    * "unset"
    * Test expression parser thoroughly
      * Add tests for "eq", "ne", "in", "ni"
      * Implement remaining math functions
* Continue to add commands from the "next" list, below.
* Flesh out Rust tests and Rust API docs in the code base.
  * Follow API design guide from the RUST nursery.
  * Design public API using `pub use` in `lib.rs`, so the examples read
    properly from the user's point of view.
* Define molt extension architecture
  * E.g., the ability to add extensions to Molt as Rust crates.
* Add costly features to core molt (e.g., regexp, glob) as Rust features.
  * `molt test` needs to be able to filter tests based on the available
    features.
* Revise main parser to use CharPtr.
* On-going:
    * Document Molt's TCL dialect using mdbook, and publish to GitHub pages.
* Consider generalizing the Subcommand array mechanism; standard command sets
  can be defined the same way, and loaded into the interpreter on creation.
* Implement stack traces
  * Need not mimic TCL's output.

The following commands need to get implemented next.

* cd, pwd
* concat
* eval
* info level
* info commands (with glob matching)
* list commands
* string
* upvar

The following commands are not implemented by Molt at the present time,
but most will probably be added eventually.

* array
* cd
* concat
* dict
* eval
* format
* info * (most subcommands)
* lassign
* linsert
* lmap
* lrange
* lrepeat
* lreplace
* lreverse
* lsearch
* lset
* lsort
* pwd
* regexp
* regsub
* split
* string
* subst
* switch
* throw
* time
* try
* uplevel
* upvar

## Acknowledgements

I've gotten help from many people in this endeavour; here's a (necessarily partial) list.

* Jonathan Castello, for general Rust info
* Kevin Kenny, for help with TCL numerics
* Don Porter, for help with TCL parsing
* Krishna Sannasi, for help getting MoltValues to work with arbitrary user data types
