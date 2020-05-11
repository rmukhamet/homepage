---
title: "Golang Help"
slug: golang
description: "golang help" 
date: 2017-08-20T21:38:52+08:00
lastmod: 2017-08-28T21:41:52+08:00
menu: "main"
weight: 50

# you can close something for this content if you open it in config.toml.
comment: false
mathjax: false
---


## benchmark
### profiling
[source](https://blog.golang.org/pprof)
go test -bench=. -benchmem -cpuprofile=cpu.out -memprofile=mem.out bench_test.go

go tool pprof -alloc_space mem.cputest mem.out
(pprof) list 'func name'

go build -gcflags "-m -m"

### benchcmp
`go test -bench=. -benchmem bench_test.go > new.txt`
git stash
`go test -bench=. -benchmem bench_test.go > old.txt`
`benchcmp old.txt new.txt`

```
benchmark old ns/op new ns/op delta
BenchmarkToJSON 1579 495 -68.65%
```

benchmark old MB/s new MB/s speedup
BenchmarkToJSON 12.66 46.41 3.67x

benchmark old allocs new allocs delta
BenchmarkToJSON 2 2 +0.00%

benchmark old bytes new bytes delta
BenchmarkToJSON 184 48 -73.91%



## debuger

dlv debug main.go # eq go run 
dlv cli> break file:num # define break point
dlv cli> continue #run till break point
dlv cli> locals #show vars
dlv cli> step # go next line

TODO delve