This repository demonstrates an issue with `analysistest`.

## Explanation

The file `analyzer.go` defines an `analysis.Analyzer`.

When operating on the testdata file `normalpkg.go`, the analyzer (due to buggy
behavior) produces the following syntactically invalid Go output when fixes are
applied:
```go
package normalpkg

<<<>>> // want "^removing$"
<<<>>> // want "^removing$"
```

This output does not match the golden file contents, which is:
```go
package normalpkg

// want "^removing$"
// want "^removing$"
```

But running:
```
go test
```
incorrectly results in a PASS, even though the output and the golden file contents do not match.

