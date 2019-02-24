2015-506-editing-movies-in-avfoundation/readme.md


- Tim Monroe, AV Foundation Engineering

## What You Will Learn


AV Foundation provides new classes for editing QuickTime movie files:

Perform range-based editing on movies and tracks Add and remove tracks
Set track associations between tracks
Add or modify movie and track metadata
Create movie files and URL sample reference movie files


## Session Outline


Introduce new classes for creating and editing QuickTime movie files Survey the new movie- and track-editing methods
Describe a personal project that will benefit from these new capabilities


### New Movie Editing Classes

- AVMovie and AVMutableMovie
- AVMovieTrack and AVMutableMovieTrack 
- AVMediaDataStorage

### QuickTime Movie Files

- AVMovie represents the data in a file that conforms to the QuickTime movie file format  
or to one of the related ISO base media file formats (such as MPEG-4)
- These formats impose a strict separation between the sample data and the information that organizes that sample data into tracks and movies

Sample Reference Movie Files

- Provide a powerful workflow tool
- But sample reference movies are inherently fragile
- To help reduce that fragility, use relative URLs
- When it’s time to deliver content, export it using AVAssetExportSession

