# GRIB2 library for Go programming language (golang)

> Parse GRIB2 files using Golang

## History

Currently in need of a parser for [GRIB Edition 2](https://www.wmo.int/pages/prog/www/WMOCodes/Guides/GRIB/Introduction_GRIB1-GRIB2.pdf) (GRIB2) we found the most an up-to-date repo in [amsokol/gogrib2](https://github.com/sdifrance/gogrib2). Nevertheless, the last commit date from 2 feb 2018 and we felt the need to maintain it.

[amsokol/gogrib2](https://github.com/sdifrance/gogrib2) did a great work in:

- Porting [wgrib2](http://www.cpc.ncep.noaa.gov/products/wesley/wgrib2/) from **C** to **Go**
- Made `wgrib2` thread-safe, by removing a lot of global read/write variables inside code
- Applied new features and patches from original `wgrib2` development stream

## How-to

```bash
go get -u github.com/sdifrance/gogrib2
```

It contains only one function that parses GRIB2 file:

```go
func Read(data []byte) ([]GRIB2, error)
```

where `GRIB2` is the structure with parsed data:

```go
// GRIB2 simplified file structure
type GRIB2 struct {
    RefTime     time.Time
    VerfTime    time.Time
    Name        string
    Description string
    Unit        string
    Level       string
    Values      []Value
}

// Value is data item of GRIB2 file
type Value struct {
    Longitude float64
    Latitude  float64
    Value     float32
}
```

See the following usage examples:

- [file-grib2csv](https://github.com/sdifrance/gogrib2/tree/master/cmd/examples/file-grib2csv) - export GRIB2 file to CSV
- [http-grib2csv](https://github.com/sdifrance/gogrib2/tree/master/cmd/examples/http-grib2csv) - export `nomads.ncep.noaa.gov` HTTP response to CSV

## Previous Known Issues

`gogrib2` does not support `jpeg`, `png` and `aec` data package formats. The reason is `wgrib2` uses external `C` libraries to parse these formats. If you have an idea how to easy port `jpeg`, `png` and `aec` please let me know.

## Contributions are Welcome

The main axis for development will be:

- Parse GRIB2 files in Go
- Performance
- Correctly treat errors
- Provide good documentation
