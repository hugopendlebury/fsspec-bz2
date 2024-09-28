# FSSPEC-BZ2

This is a simple plugin for the python module fsspec. Which adds support for a new protocol called simplecachebz2.
It works by creating a wheel which adds a new entry point to fsspec.specs

## Why would I used this ?

fsspec is a great module since it abstracts away many details and provides a way of interacting with many different
types of file systems and storage types with a consistent API.
However programs such as those written in C often do not accept a python file like object. Fsspec offers a simplecache
which effectively downloads the file locally so it can be passed to these types of API. E.g. Lets say
you are working in the weather domain and using a library which is based on eccodes such as gribtoarrow of perhaps cfgrib / xarray.
With such pieces of software you might create a url such as :

    simplecache://s3://noaa-gefs-pds/gefs.20240928/00/atmos/pgrb2ap5/geavg.t00z.pgrb2a.0p50.f000

The above URL would download / cache the grib file allowing it to accessed from a library which performs an fopen() call in C.

However as anyone who as worked with grib files for while will no doubt know, these files are often bzipped.

Unfortunatelty which fsspec offers support for compression such as zip and tar these don't work in conjuection with 
caching.

This simple extension seeks to resolve this problem

## Usage

The plugin registers a custom spec with a protocol called simplecachebzip

simplecachebzip://s3://somebuck/somepath/somefile.bz2

## Development

This module uses uv.

Step 1.
    Install uv (with pip or you favorite means)

Step 2.
    Use UV commands

    e.g. uv build, uv run etc..