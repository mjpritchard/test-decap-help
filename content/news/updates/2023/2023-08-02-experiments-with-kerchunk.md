---
title: Technical Blog Post - Experiments with Kerchunk
date: 2023-08-02 09:54:58+00:00
tags: ['news']
aliases: ['/blog/experiments-with-kerchunk']
thumbnail: 
icon: fas circle-info
---

[Check out our technical blog post all about Kerchunk!](https://techblog.ceda.ac.uk/2023/05/04/kerchunk-experiments.html)


It covers how we have been experimenting with a library of python tools called Kerchunk to represent CEDA archive data for easier cloud access without the need to convert or duplicate data in cloud-optimised formats.  
  



Kerchunk provides a single uniform method of representing chunked compressed data formats for cloud access without requiring format conversion. This is useful because converting archived data is impractical on a large scale and duplicating data in multiple formats requires a significant increase to the storage requirements for the archive.  
  



This technical blog post would be interesting to anyone looking into cloud accessible analysis ready data. It may also be useful to anyone currently converting or looking to convert data into Zarr format, as Kerchunk provides an alternative with considerable advantages, like reduced computation time and storage requirements. Kerchunk files can also be updated due to changes in NetCDF files more quickly than reconverting to Zarr.  
  



Experiments with different optimisation methods for kerchunk explored here include representing chunk data formulaically using tools from python libraries and custom syntax extending the usage of these tools to cover less uniform NetCDF file structure.



[Find out more about our work with Kerchunk and our other technical projects here.](https://techblog.ceda.ac.uk/)


