[TOC]

# Digital Container Format
A container or wrapper format is a [metafile](https://en.wikipedia.org/wiki/Metafile) [format](https://en.wikipedia.org/wiki/File_format) whose specification describes how different data elements and metadata coexist in a [computer file](https://en.wikipedia.org/wiki/Computer_file). Among the earliest cross-platform container formats were [Distinguished Encoding Rules](https://en.wikipedia.org/wiki/Distinguished_Encoding_Rules) and the 1985 [Interchange File Format](https://en.wikipedia.org/wiki/Interchange_File_Format). Containers are frequently used in *multimedia* applications.

Since the container does not describe how data or metadata is encoded, a program able to identify and open a container file might not be able to decode the contained data. This may be caused by the program lacking the required [decoding algorithm](https://en.wikipedia.org/wiki/Codec).

The differences between various container formats arise from five main issues:

1. **Popularity**; how widely supported a container is.
2. **Overhead**. This is the difference in file-size between two files with the same content in a different container.
3. **Support for advanced codec functionality**. Older formats such as AVI do not support new codec features like B-frames, VBR audio or VFR video natively. The format may be "hacked" to add support, but this creates compatibility problems.
4. **Support for advanced content**, such as chapters, subtitles, meta-tags, user-data.
5. Support of [streaming media](https://en.wikipedia.org/wiki/Streaming_media).

## Multimedia container formats
[Comparison of container formats](https://en.wikipedia.org/wiki/Comparison_of_container_formats)

### Only Audio
- [AIFF](https://en.wikipedia.org/wiki/Audio_Interchange_File_Format) (IFF file format, widely used on Mac OS platform)
- [WAV](https://en.wikipedia.org/wiki/WAV) (RIFF file format, widely used on Windows platform)
- [XMF](https://en.wikipedia.org/wiki/Extensible_Music_Format_(XMF)) (Extensible Music Format)

### Only images
- [FITS](https://en.wikipedia.org/wiki/FITS) (Flexible Image Transport System) still images, raw data, and associated metadata.
- [TIFF](https://en.wikipedia.org/wiki/Tagged_Image_File_Format) (Tagged Image File Format) still images and associated metadata.

### Multimedia
- 3GP (used by many mobile phones; based on the ISO base media file format)
- ASF (container for Microsoft WMA and WMV, which today usually do not use a container)
- [AVI](https://en.wikipedia.org/wiki/Audio_Video_Interleave) (the standard Microsoft Windows container, also based on RIFF)
- DVR-MS ("Microsoft Digital Video Recording", proprietary video container format developed by Microsoft based on ASF)
- [Flash Video](https://en.wikipedia.org/wiki/Flash_Video) (FLV, F4V) (container for video and audio from Adobe Systems)
- IFF (first platform-independent container format)
- [Matroska](https://en.wikipedia.org/wiki/Matroska) (MKV) (not limited to any codec or system, as it can hold virtually anything. It is an open standard and open source container format).
- MJ2 - Motion JPEG 2000 file format, based on the ISO base media file format which is defined in MPEG-4 Part 12 and JPEG 2000 Part 12
- QuickTime File Format (standard QuickTime video container from Apple Inc.)
- MPEG program stream (standard container for MPEG-1 and MPEG-2 elementary streams on reasonably reliable media such as disks; used also on DVD-Video discs)
- MPEG-2 transport stream (a.k.a. MPEG-TS) (standard container for digital broadcasting and for transportation over unreliable media; used also on Blu-ray Disc video; typically contains multiple video and audio streams, and an electronic program guide)
- [MP4](https://en.wikipedia.org/wiki/MPEG-4_Part_14) (standard audio and video container for the MPEG-4 multimedia portfolio, based on the ISO base media file format defined in MPEG-4 Part 12 and JPEG 2000 Part 12) which in turn was based on the QuickTime file format.
- [Ogg](https://en.wikipedia.org/wiki/Ogg) (standard container for Xiph.org audio format Vorbis and video format Theora)
- [RM](https://en.wikipedia.org/wiki/RealMedia) (RealMedia; standard container for RealVideo and RealAudio)
- [WebM](https://en.wikipedia.org/wiki/WebM)

There are many other container formats, such as NUT, MXF, GXF, ratDVD, SVI, [VOB](https://en.wikipedia.org/wiki/VOB) and DivX Media Format

### [WebM](http://www.webmproject.org/)
WebM is an open, royalty-free, media file format designed for the web.

WebM defines the file container structure, video and audio formats. WebM files consist of video streams compressed with the [VP8](https://en.wikipedia.org/wiki/VP9) video codec and audio streams compressed with the [Vorbis](http://xiph.org/vorbis/) audio codec. The WebM file structure is based on the [Matroska](http://matroska.org/) container.

# File Format
## Audio file format
An audio file format is a file format for storing digital audio data on a computer system. This data can be stored uncompressed, or compressed to reduce the file size. It can be a raw bitstream, but it is usually a container format or an audio data format with defined storage layer.

It is important to distinguish between a [file format](https://en.wikipedia.org/wiki/File_format) and an [audio codec](https://en.wikipedia.org/wiki/Audio_codec). A codec performs the encoding and decoding of the raw audio data while the data itself is stored in a file with a specific audio file format. Although most audio file formats support only one type of audio data (created with an audio coder), a multimedia container format (as Matroska or AVI) may support multiple types of audio and video data.

There are three major groups of audio file formats:

- Uncompressed audio formats, such as [WAV](https://en.wikipedia.org/wiki/WAV), AIFF, AU or [raw](https://en.wikipedia.org/wiki/Raw_audio_format) header-less PCM;
- Formats with lossless compression, such as [FLAC](https://en.wikipedia.org/wiki/Free_Lossless_Audio_Codec), [Monkey's Audio](https://en.wikipedia.org/wiki/Monkey%27s_Audio) (filename extension APE), WavPack (filename extension WV), TTA, ATRAC Advanced Lossless, [Apple Lossless](https://en.wikipedia.org/wiki/Apple_Lossless) (filename extension m4a), MPEG-4 SLS, MPEG-4 ALS, MPEG-4 DST, Windows Media Audio Lossless (WMA Lossless), and Shorten (SHN).
- Formats with lossy compression, such as [MP3](https://en.wikipedia.org/wiki/MP3), [Vorbis](https://en.wikipedia.org/wiki/Vorbis), Musepack, AAC, ATRAC and Windows Media Audio Lossy (WMA lossy).

# Open format
An open file format is a published specification for storing digital data, usually maintained by a standards organization, which can therefore be used and implemented by anyone. For example, an open format can be implemented by both proprietary and free and open source software, using the typical software licenses used by each.

[List open file format](https://en.wikipedia.org/wiki/List_of_free_file_formats)

## Multimedia
### Imaging
- [GIF](https://en.wikipedia.org/wiki/Graphics_Interchange_Format)
- [SVG](https://en.wikipedia.org/wiki/Scalable_Vector_Graphics)
- [PNG](https://en.wikipedia.org/wiki/Portable_Network_Graphics)
- ...

### Audio
- FLAC
- Vorbis
- ...

### Video
- Matroska (mkv)
- WebM
- Theora
- ...

### Text
- Plain text
- HTML
- LaTeX
- ...

### Archiving and compression
- 7z
- gzip
- tar
- xz
- ZIP
- ...

### Other
- CSS
- XML
- TrueCrypt
- ...
