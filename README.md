[![Build status](https://ci.appveyor.com/api/projects/status/hvqqnbiwmo90m2fd?svg=true)](https://ci.appveyor.com/project/gs-jenkins/raw-to-ome-tiff)

raw-to-ome-tiff converter
=========================

Java application to convert a directory of tiles to an OME-TIFF pyramid.
This is the second half of iSyntax => OME-TIFF conversion.


Usage
=====

Build with Gradle:

    gradle clean build

Unpack the distribution:

    cd build/distributions
    unzip raw-to-ome-tiff-$VERSION.zip
    cd raw-to-ome-tiff-$VERSION

Run the conversion:

    bin/raw-to-ome-tiff tile_directory --output pyramid.ome.tiff

This same command should work independent of the `--no_pyramid` and `--file_type` options used in the `isyntax-to-raw` step.
If a pyramid was not generated by `isyntax-to-raw`, then this will use the `loci.common.image.IImageScaler` API to create one.

By default, LZW compression will be used in the OME-TIFF file.
The compression can be changed using the `--compression` option.
Valid values are defined in https://github.com/ome/bioformats/blob/v6.2.1/components/formats-bsd/src/loci/formats/out/TiffWriter.java#L144


Areas to improve
================

* Try faster writing option (TiffSaver instead of PyramidOMETiffWriter)
    - this is little more complicated since the tiles are RGB
