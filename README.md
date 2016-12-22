[![CircleCI](https://circleci.com/gh/giantswarm/errgo.svg?&style=shield&circle-token=36e15323510f6d4dcc3f095856560e9fd0c6c110)](https://circleci.com/gh/giantswarm/errgo) [![GoDoc](https://godoc.org/github.com/giantswarm/errgo?status.svg)](http://godoc.org/github.com/giantswarm/errgo)

# errgo

The errgo package provides a way to create and diagnose errors. It is compatible
with the usual Go error idioms but adds a way to wrap errors so that they record
source location information while retaining a consistent way for code to inspect
errors to find out particular problems.

This repository is a fork. The original can be found at
https://github.com/juju/errgo. There are two minor changes to polish the error
management.

1. added Trace(error) string

This

```go
fmt.Printf("%s\n", errgo.Trace(err))
```

Produces this

```
[{/go/src/github.com/giantswarm/test/main.go:22} {/go/src/github.com/giantswarm/test/main.go:20} {/go/src/github.com/giantswarm/test/main.go:13}]
```

instead of this using the old `errgo.Details`

```
[{/go/src/github.com/giantswarm/test/main.go:36: } {/go/src/github.com/giantswarm/test/main.go:34: } {jerr}]
```

2. Note that `: ` is omitted in case there is no error message to the location
information of a specific error.
