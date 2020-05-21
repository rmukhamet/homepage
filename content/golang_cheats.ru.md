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

`dlv debug main.go` # eq go run  
`dlv exec`  # debug compiled bin  
`dlv test` # eq go test  
`dlv attach` # debug running app  
`dlv trace` # 

dlv cli> break file:num # define break point  
dlv cli> continue #run till break point  alias `c`  
dlv cli> locals #show vars  
dlv cli> step # execute next line  
dlv cli> next # Step over to next source line.  
dlv cli> stepout # execute till return and stop  
dlv cli> restart # restart app with debug and all breakpoints  

dlv cli>source path # execute dlv commands from file defined in path separated by newline  
dlv cli> frame 0 locals # show locals in 0 frame goroutine   


dlv variables cmd:
- locals in current func 
- print specific var
- args shows args current function
- vars all package level vars
- funcs
- types 

dlv
- sources list all sources files 
- list code around line executed or we can specify line in source file currently executing like 'list 50'
- disassemble 
- regs shows CPU registers

dlv get app state
- stack
- goroutines #shows all goroutines   flag -g shows place of goroutine creation 
- treads

dlv manipulate app state
- set # changes var value
- goroutine #change goroutine
- tread #change active thread

dlv app halt cmd
- break
break main.go:2 app stops just BEFORE line 2
- condition
condition breakpoint ID condition itself
- trace #not halting but logging
trace label main.go
- breakpoints #list breakpoints
- on 
- clear
- clearall


TODO delve