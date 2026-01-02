# ID24 formal specification 0.99.2

As a part of developing features for the new Doom + Doom II release, certain features were needed in order to make development easier and to provide a solid foundation for any and all future releases. To collect all these features in one place that source ports can implement and use, a new feature specification dubbed ID24 has been created.

### Baseline features

ID24 is a superset of the following standards and features:

* Vanilla Doom
* Boom
* MUSINFO
* MBF
* DEHEXTRA
* MBF21
* DSDHACKED
* UMAPINFO

A complete ID24 implementation requires support for those standards and features.

For simplicity’s sake, these features are also enumerated in the following order, from the least amount of features to the most amount of features and referred to as a **feature level**:

* **Doom 1.9**
* **Limit Removing (with UMAPINFO)**
* **Limit Removing With Bug Fixes**
* **Boom 2.02**
* **complevel 9 (with MUSINFO)**
* **MBF (with DEHEXTRA)**
* **MFB21**
* **DSDHACKED**
* **ID24**

This ordering is important for a few features described by the ID24 specification.

### JSON lumps

A key feature that all new data formats use is the [JSON Lump specification](./JSON_Lump.md). Rather than create a new data format for each new data type, a standard JSON root element has been created that can be parsed and interpreted by both tools and source ports. As a standardised format, this cuts down on the amount of work required to implement new datatypes and provides a simple way to support new datatypes in the future; while also allowing robust tools to be developed using standard libraries and modern programming principles.

### Major features

Each major feature of ID24 is covered in a separate document. These features are:

* [DEMOLOOP](./DEMOLOOP.md) - a way to customise the Doom demo loop
* [Finale lumps](./Finale_lumps.md) - a way to customise Doom finales, and allow continuing to another map from any finale
* [GAMECONF](./GAMECONF.md) - a way to describe how to set up the runtime environment of any WAD
* [Mapping additions](./Mapping_Additions.md) - new linedef types and thing numbers for mappers to use
* [ID24HACKED](./ID24HACKED.md) - extensions to DeHackEd, plus a [way to verify valid DeHackEd](./ID24HACKED_hashing.md) states before parsing additional DeHackEd lumps
* [Interlevel lumps](./Interlevel_lumps.md) - a way to define background animations on victory screens
* [SBARDEF](./SBARDEF.md) - a way to create custom status bars
* [SKYDEFS](./SKYDEFS.md) - a way to create custom skies, including Doom 64 fire skies
* [Translations](./Translations.md) - a way to create new translations for palette swapping

### New placeable things

Perhaps of most interest to the community, Doom + Doom II’s new episode Legacy of Rust includes a suite of new monsters, decorations, and weapons for use in your maps. These new things are exposed to everyone via a new set of table entries that do not conflict with any previous community standard or usage of DeHackEd indices.

### Supporting data

Data used to support the **ID24** specification is contained within the **id24res.wad** file as shipped with your copy of Doom + Doom II from all digital storefronts. When encountering a mod that requests **ID24** support, it is recommended that source ports use their normal IWAD resolution rules to locate this file (including from common install sources such as Steam, GOG, etc) and attempt to load that before the main IWAD in order for any resource overrides to operate correctly.

While users should provide that file themselves, other sources such as those provided by the Freedoom project or as complete IWAD replacement for total conversions are also perfectly acceptable. The standard behavior for handling missing resources should be utilised when attempting to use ID24 features that require resources which cannot be found. For example, in the original Doom and Doom II releases for MSDOS as well as the current Doom + Doom II release an error is issued when attempting to render a missing sprite; and for some sourceports, a “missing sprite” replacement graphic is used in its place.

### Music formats

A complete **ID24** implementation supports the following additional audio formats for music playback:

* OGG Vorbis
* Tracker (.mod, .s3m, .xm, and .it formats)

### Future revisions

Future revisions of any part of the **ID24** specification and feature set will incur the following version number changes for the following reasons:

* Major - breaking changes, not backward compatible
* Minor - additions and minor changes
* Revision - bug fixes and clarifications

As ID24 aims to be a stable feature set, major revisions will aim to be restricted to a new feature set specification.

### Guiding principles for ID24 specifications

As a set of features developed for operation on consoles, ID24 needed to satisfy the requirements of shipping on multiple vendor-controlled platforms with their own sets of rules and allowances. As such, it was designed to maintain compatibility with existing community standards in a way that would allow the community to be able to spread their work to the wider world beyond the PC space. It has also been created to be a stable platform for both community defined work to coexist with any future work id Software may or may not perform on Doom + Doom II and to not create situations where both avenues of development overlap and impede each other’s work.

Rather than assume generic names for data fields, explicit naming for ID24 has been taken in cases where a conflict is likely to occur. This is most pertinent in the DeHackEd features that have been added, where source ports (and even the original Heretic) have taken to calling additional flags fields “flags2”, “flags3”, etc. Naming such fields for ID24 at the code and data level makes it explicit what functionality set these fields should be used for, and avoids conflicting with prior or future functionality.

There are many standards over the years that take the assumption of the implementation before it as a part of its standard. A primary example is UMAPINFO, which changes behavior depending on game mode, and even relies on undocumented behavior on how an episode number is resolved. Rather than assume a prior implementation, an explicit complete implementation is defined and specced. This includes the JSON data level, which have all been authored as reflections of data structures rather than a way to describe modifying existing structures.

When creating a new feature and specification, an attempt was made to see if there were suitable community standards. While some source ports have solutions for what has been specced, there is nothing standard and widely adopted amongst a broad range of source ports. These newly developed specifications will be the basis for any and all official content that may or may not be commissioned in the future and as such have been developed to replicate functionality that was already there, add anything required for this release, and leave a path open for future development and iteration on these features and specifications.
