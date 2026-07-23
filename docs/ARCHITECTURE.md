# ARCHITECTURE

> High-level architecture of **Recall**

## Goals

-   Modular by design
-   Offline-first
-   Event-driven communication
-   Moment-first data model
-   Replaceable AI components

------------------------------------------------------------------------

# System Overview

``` text
                +------------------+
                |       GUI        |
                +--------+---------+
                         |
                 Application API
                         |
+------------------------------------------------------+
|                  Core Services                       |
+------------------------------------------------------+
| Library | Watcher | Indexer | Search | Preview | Export |
+------------------------------------------------------+
                         |
                 Event Bus / Messages
                         |
+------------------------------------------------------+
|                  AI Pipeline                         |
+------------------------------------------------------+
| Speech | Vision | OCR | Metadata | Moment Detection |
+------------------------------------------------------+
                         |
                    Database Layer
                         |
                 SQLite + Vector Index
```

------------------------------------------------------------------------

# Main Modules

## GUI

Responsible for user interaction.

Responsibilities:

-   Library browsing
-   Search
-   Timeline preview
-   Clip export
-   Settings

------------------------------------------------------------------------

## Library Manager

Maintains the media library.

Responsibilities:

-   Register files
-   Manage folders
-   Track metadata

------------------------------------------------------------------------

## File Watcher

Monitors configured folders.

Events:

-   Video Added
-   Video Updated
-   Video Removed

------------------------------------------------------------------------

## Indexer

Coordinates the indexing pipeline.

Steps:

1.  Import
2.  Audio extraction
3.  Speech transcription
4.  Frame sampling
5.  OCR
6.  Vision analysis
7.  Metadata generation
8.  Moment detection
9.  Database update

------------------------------------------------------------------------

## Search Engine

Provides unified search across:

-   Transcript
-   Visual descriptions
-   OCR
-   Metadata
-   AI tags

Returns ranked **Moments**.

------------------------------------------------------------------------

## Preview Engine

Displays timeline, highlights detected moments and previews clips.

------------------------------------------------------------------------

## Export Engine

Exports selected moments without modifying originals.

------------------------------------------------------------------------

# Data Model

``` text
Library
 └── Folder
      └── Video
            ├── Moment
            ├── Transcript
            ├── Metadata
            ├── Frames
            └── Analysis
```

**Moment** is the primary entity of the system.

------------------------------------------------------------------------

# Event Flow

``` text
Video Added
    ↓
Watcher
    ↓
Indexer
    ↓
AI Pipeline
    ↓
Database Updated
    ↓
Search Index Updated
    ↓
GUI Refresh
```

------------------------------------------------------------------------

# Architectural Principles

-   Modules communicate through interfaces.
-   Prefer events over direct dependencies.
-   AI models must be replaceable.
-   Every module should be testable independently.
-   Business logic must not depend on the GUI.

------------------------------------------------------------------------

# Future Expansion

The architecture should allow adding:

-   Plugin system
-   New AI models
-   Cloud synchronization
-   Image indexing
-   Audio libraries
-   Distributed processing

without redesigning the existing system.
