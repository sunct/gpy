# gpy

[![CircleCI Status](https://circleci.com/gh/go-ego/gpy.svg?style=shield)](https://circleci.com/gh/go-ego/gpy)
[![Build Status](https://travis-ci.org/go-ego/gpy.svg?branch=master)](https://travis-ci.org/go-ego/gpy)<!-- [![Coverage Status](https://coveralls.io/repos/gtihub.com/go-ego/gpy/badge.svg?branch=master)](https://coveralls.io/r/github.com/go-ego/gpy?branch=master) -->
[![codecov](https://codecov.io/gh/go-ego/gpy/branch/master/graph/badge.svg)](https://codecov.io/gh/go-ego/gpy)
[![Go Report Card](https://goreportcard.com/badge/github.com/go-ego/gpy)](https://goreportcard.com/report/github.com/go-ego/gpy)
[![GoDoc](https://godoc.org/github.com/go-ego/gpy?status.svg)](https://godoc.org/github.com/go-ego/gpy)

汉语拼音转换工具 Go 版。

原地址：[github.com/go-ego/gpy](github.com/go-ego/gpy)

## Installation

```
go get -u github.com/go-ego/gpy
```
或者使用我的这个分支
```
go get -u github.com/sunct/gpy
```
### install CLI tool:

```
go get -u github.com/go-ego/gpy/pinyin
$ gpy 中国人
zhōng guó rén
```


## Documentation

API documentation can be found here:
[godoc](https://godoc.org/github.com/go-ego/gpy)


## Usage

```go
package main

import (
	"fmt"

	"github.com/go-ego/gpy"
)

func main() {
	hans := "中国人"

	// 默认
	a := gpy.NewArgs()
	fmt.Println(gpy.Pinyin(hans, a))
	// [[zhong] [guo] [ren]]

	// 包含声调
	a.Style = gpy.Tone
	fmt.Println(gpy.Pinyin(hans, a))
	// [[zhōng] [guó] [rén]]

	// 声调用数字表示
	a.Style = gpy.Tone2
	fmt.Println(gpy.Pinyin(hans, a))
	// [[zho1ng] [guo2] [re2n]]


	
	// 首字母风格
	a.Style = gpy.FirstLetter
	fmt.Println(gpy.Pinyin(hans, a))
	// [[z] [g] [r]]
	
	
	... ...
	
	
	// 开启多音字模式
	a = gpy.NewArgs()
	a.Heteronym = true
	fmt.Println(gpy.Pinyin(hans, a))
	// [[zhong zhong] [guo] [ren]]
	a.Style = gpy.Tone2
	fmt.Println(gpy.Pinyin(hans, a))
	// [[zho1ng zho4ng] [guo2] [re2n]]

	fmt.Println(gpy.LazyPinyin(hans, gpy.NewArgs()))
	// [zhong guo ren]

	fmt.Println(gpy.Convert(hans, nil))
	// [[zhong] [guo] [ren]]

	fmt.Println(gpy.LazyConvert(hans, nil))
	// [zhong guo ren]
}
```

说明，目前可使用模式包括：
```$xslt
    Normal      = 0 // 普通风格，不带声调（默认风格）。如： zhong guo
	Tone        = 1 // 声调风格1，拼音声调在韵母第一个字母上。如： zhōng guó
	Tone2       = 2 // 声调风格2，即拼音声调在各个韵母之后，用数字 [1-4] 进行表示。如： zho1ng guo2
	Tone3       = 8 // 声调风格3，即拼音声调在各个拼音之后，用数字 [1-4] 进行表示。如： zhong1 guo2
	Initials    = 3 // 声母风格，只返回各个拼音的声母部分。如： zh g
	FirstLetter = 4 // 首字母风格，只返回拼音的首字母部分。如： z g
	Finals      = 5 // 韵母风格，只返回各个拼音的韵母部分，不带声调。如： ong uo
	FinalsTone  = 6 // 韵母风格1，带声调，声调在韵母第一个字母上。如： ōng uó
	FinalsTone2 = 7 // 韵母风格2，带声调，声调在各个韵母之后，用数字 [1-4] 进行表示。如： o1ng uo2
	FinalsTone3 = 9 // 韵母风格3，带声调，声调在各个拼音之后，用数字 [1-4] 进行表示。如： ong1 uo2
```

## Related Projects

* [hotoo/pinyin](https://github.com/hotoo/pinyin): 汉语拼音转换工具 Node.js/JavaScript 版。
* [mozillazg/python-pinyin](https://github.com/mozillazg/python-pinyin): 汉语拼音转换工具 Python 版。
* [mozillazg/rust-pinyin](https://github.com/mozillazg/rust-pinyin): 汉语拼音转换工具 Rust 版。


## License

Under the MIT License, base on [go-pinyin](https://github.com/mozillazg/go-pinyin).
