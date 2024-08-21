<p align="center">
  <img src="data/mw-logo-only.svg" alt="Logo" height=170>
</p>

# CDX Reporting Tech Test

Welcome to the MirrorWeb Web Tech Test! We'd like to see how you approach building out some new features, as well as how you work through debugging issues.

## Overview

You've been tasked with writing a simple CLI application to extract some useful insights from archived web content for further analysis. Your application should parse and extract the data contained within a CDX file and output the required data in an easily digestable file format of your choice.

### What's a CDX file?

CDX is a file format used for indexing web content archived in [WARC](https://iipc.github.io/warc-specifications/specifications/warc-format/warc-1.1-annotated/) files so that it can be looked up and retrieved more efficiently later. The format has evolved over time, with several variations on the fields included, but the web archiving community has largely settled on the 11-field format outlined at the top of the following specification: <https://iipc.github.io/warc-specifications/specifications/cdx-format/cdx-2015/>.

## Tasks

Use Node.js v20+ to write a CLI application to extract the required data from a CDX file and output it in an easily digestable file format of your choice. Please DO NOT use any external libraries for this, only what Node.js built-in modules provide.

This repository contains an example CDX file you can use for developing your application. However, please bear in mind that your script could be used on files of arbitrary size (potentially many GBs), so performance matters.

Your script should do the following:

* accept a CLI argument for a relative path of a file to parse
* accept a CLI argument to filter the data to be processed via the passed url origin e.g. <https://www.example.com> (the filter value should be included in the output file if one was passed)
* accept a CLI argument to filter the data to be processed via the passed content-type e.g. `text/html` (the filter value should be included in the output file if one was passed)
* only include valid HTTP/HTTPS scheme urls - anything outside of this should be excluded from output data
* any invalid data encountered should log a warning to the user but continue processing data
* any errors should be logged to the caller and either handled or exit the program gracefully if not recoverable
* generate an output file containing the following data collated from the input:
  * the name of the input file
  * the total 'valid' lines
  * the total 'invalid'/ignored lines
  * a list of the unique url domains included in the input file, along with totals for each e.g. `www.example.com`
  * a list of the unique HTTP response status codes included in the input file, along with totals of each
  * a list of the unique content types included in the input file, along with totals for each
