# CountLoc Releases
binary releases of my line counting tool (click releases, then download zip file)

CountLoc v1.9 (c) 2015-18 mar

Supported platforms: x86 (Win), x64 (Linux/OSX)

usage:
```
usage: CountLoc [args] <dir> [<dir2> ...]
args:
	-h, -? help
	-sp show progress (off by default)
	-g greedy mode (count punctuation as code)
	-f count by file (off by default)
	-np don't pretty-print numbers
	-nr don't recurse on subdirs
	-xd=dir,dir2,... exclude dirs
	-xe=ext,ext2,... exclude extensions
	-fe=ref_ext,ext force extension
		example: -fe=pas,inc
	-le list extensions in dir
	-la list anomalies in dir (empty/dups/UTF-16)
	-v always show version
	-max=n ignore files bigger than n megabytes (default=64)
	-stdin=name.ext input from stdin
		example: --stdin=*.tar
	-sa scan archives (zip/tar/gz) along the way (default=off)
		note: nested archives will fail to open
	-csv <filename> output results (total even if counting by file) to csv
		note: always overwrites filename without prompting!
		this implies no output to stdout unless stdout
		is supplied as filename; csv will then
		be printed to stdout instead
	-diff <filename> diff results with previously saved csv
```

Directory is relative to current working directory.
Duplicate files are detected using md5 hash (and ignored).
By default, CountLoc doesn't count separate punctuation on a line as code.
This allows the following code fragments to give the same LOC:

```
if (x)
	y();

if (x) {
	y();
}

if (x)
{
	y();
}
```

partial support for archives (zip/tar/tar.gz and tgz), only deflate supported for zip
Note to unix users: don't forget to chmod u+x

changes sice 1.8:
- add support for TypeScript (ts), Go (go) and Rust (rs)
- add support for template literals in JavaScript/TypeScript
- dropped FreeBSD support because of issues with my virtual machine

changes since 1.7.2:
- add -f (by file) argument

changes since 1.7.1:
- fix potential crash when loading broken zip/gz files

changes since 1.7:
- fix tar parsing (GNU long names)

changes since 1.6.2:
- diff support; output relative to last saved csv state
- manually define maximum file size using -max
- support tar/tar.gz and .tgz (only ustar and partially gnu/pax)
- support for stdin (-stdin) (must supply virtual filename)
- support for force-extension (-fe) (i.e. force inc => pas etc.)
- scan archives along the way with -sa (default is off)
- optionally show progress with -sp
- micro-optimize processing (3% faster or so)

changes since 1.6.1:
- display relative names in zip archive properly with -la
- display open/read error with -la

changes since 1.6:
- ignore files bigger than 64MB
- slightly faster zip processing

changes since 1.5:
- output csv file for machine processing (optional)
- always show version (optional)

changes since 1.0:
- support UTF-16 LE/BE source files
- more extensions (now also d, lua, py, pas)
- more dirs
- file support (i.e. count lines in a single file)
- zip support (deflate only), count lines in a given zip file
- new args
- pretty-print numbers
- sort by LOC (descending)
- print punctuation lines in default mode
- fix EOF handling
- lexer now supports string literals so this
```
	"text /*"
	"..."
```
  is properly parsed as 2 loc in C (0 comments)
