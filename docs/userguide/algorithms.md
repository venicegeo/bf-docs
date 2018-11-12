# Algorithms

## NDWI

While bfalg-ndwi can be used as a Python library (as from the Beachfront web app),
it can also be run using the Command Line Interface (CLI). Use the help switch
(-h or --help) to display inline help.

The parameters listed below may also be set through the Beachfront UI.

```
$ python bfalg_ndwi.py -h
usage: bfalg-ndwi [-h] -i INPUT [-b BANDS BANDS] [--outdir OUTDIR]
                  [--basename BASENAME] [--l8bqa L8BQA] [--coastmask]
                  [--minsize MINSIZE] [--close CLOSE] [--simple SIMPLE]
                  [--verbose VERBOSE] [--version]

Beachfront Algorithm: NDWI (v1.0.8)

optional arguments:
  -h, --help            show this help message and exit
  -i INPUT, --input INPUT
                        Input image (1 or 2 files) (default: None)
  -b BANDS BANDS, --bands BANDS BANDS
                        Band numbers for Green and NIR bands (default: [1, 1])
  --outdir OUTDIR       Save intermediate files to this dir (otherwise temp)
                        (default: )
  --basename BASENAME   Basename to give to output files (no extension,
                        defaults to first input filename (default: None)
  --l8bqa L8BQA         Landat 8 Quality band (used to mask clouds) (default:
                        None)
  --coastmask           Mask non-coastline areas (default: False)
  --minsize MINSIZE     Minimum coastline size (default: 100.0)
  --close CLOSE         Close line strings within given pixels (default: 5)
  --simple SIMPLE       Simplify using tolerance in map units (default: None)
  --verbose VERBOSE     0: Quiet, 1: Debug, 2: Info, 3: Warn, 4: Error, 5:
                        Critical (default: 2)
  --version             Print version and exit
```

If a single filename is provided via the INPUT argument, then BANDS needs to be
provided to specify which bands in the file should be used. Otherwise it defaults
to '1, 1', meaning it would use the same band for both Green and NIR. This example
uses the first band in the file as the Green band and the fifth as the NIR.

```
$ bfalg-ndwi -i test1.tif -b 1 5
```
If the INPUT parameter is provided twice for two filenames, then BANDS is the band
number for the first file (Green) and the second file (NIR). This example uses
the second band from the `test1.tif` as the Green band, and the first band from
`test2.tif` as the NIR band.

```
$ bfalg-ndwi -i test1.tif -i test2.tif -b 2 1
```

Input files are all that are absolutely required, but a more typical scenario
would look like this (using the CLI):

```
$ bfalg-ndwi -i scene123.tif -b 1 2 --basename testrun --outdir scene123-output --coastmask
```

This will apply the included buffered coastline (`bfalg_ndwi/coastmask.shp`) to
the image to mask out non-coastal regions. It will store all output files with
the name `testrun` (+ additional tag and extension, e.g. `testrun.geojson`,
`testrun_otsu.TIF`) in the directory `scene123-output/`.

For Landsat8: If the BQA band is available, it can be provided which will mask
out the clouds from the scene.

```
$ bfalg-ndwi -i LC80080282016215LGN00_B1.TIF -i LC80080282016215LGN00_B5.TIF --l8bqa LC80080282016215LGN00_BQA.TIF --basename LC80080282016215LGN00 --outdir LC80080282016215LGN00_test --coastmask
```
The last three remaining parametes are tuning parameters involving the creation
of the vector output.

-   `minsize` (100): This is the minimum size a linestring should be before being
    filtered out. This corresponds to the `potrace` [parameter](http://potrace.sourceforge.net/#usage)
    `-t`/`--turdsize`, and is not the length of the line but rather some measure
    of the extent of it. The default of 10 will not filter out many lines. For
    Landsat, a value of 100 works well at removing false coasts, but may also
    remove islands or smaller incomplete shorelines.
-   `close` (5): Linestrings will be closed if their two endpoints are within this
    number of pixels. The default is 5 and setting it to 0 will turn it off. This
    should not be set to a value much higher than 10.
-   `simplify` (None): Simplification will not be done by default. If provided, it
    is in units of degrees and is used to simplify and smooth the output.
    Simplification is heavily application and source imagery dependent, and is a
    lossy process. Consider starting points for RapidEye and PlanetScope data to be
    0.00035, and  0.0007 for Landsat8.

### Band Combinations
The traditional NDWI algorithm uses the Green and NIR bands to calculate a
normalized difference index:

```
NDWI = (green-nir) / (green+nir)
```

The band names Green and NIR are what is referenced to in the online help.
However, other bands can work as well or even better on some instruments. The
Green band is a band that has a high water reflectance, while the NIR band is a
band that has a very low water reflectance. The following bands are recommended.

| Sensor        | 'Green' band  | 'NIR' band  |
|---------------|---------------|-------------|
| Landsat8      | 1 (Coastal)   | 5 (NIR)     |
| RapidEye      | 2 (Green)     | 4 (NIR)     |
| PlanetScope   | 2 (Green)     | 4 (NIR)     |
| Sentinel-2    | 2 (Blue)      | 8 (NIR)     |
