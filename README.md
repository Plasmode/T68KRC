# T68KRC, Tiny68K for RC2014
## Introduction

T68KRC derived from version 1 of Tiny68K. The major differences are Instead of 16 meg of memory, T68KRC has 2 meg of memory, and an expansion bus that's compatible with RC2014's I/O module is added. Like Tiny68K, T68KRC has no parallel ROM. The boot ROM is a 32Kbyte serial flash that's copied into the lowest 32Kbyte of the memory when powered up or with a reset. The RAM-resident boot software can be modified just like any data in RAM but is overwritten on the next power cycle or with a reset.

Current version of T68KRC is rev0.1.  It corrected a minor engineering change in rev0

![](T68KRC_REV0.1/t68krc_rev01_topview.jpg)

