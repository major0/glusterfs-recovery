# GlusterFS Recovery Tool

This tool aims to assist administrators in recovering files in a GlusterFS
filesystem in the event that GlusterFS is not capable of healing the file
itself.

## Requirements
These tools need to be run as root on a node which is part of a gluster volume.
Further more, many of the commands expect ssh to be usable for contacting other
nodes w/out a password prompt (ssh `authorized_leys` configured appropriately).

## Usage
`glusterfs-recovery <command> [args]`

## Commands

### list
List which files on the local node are in need of healing.
 - `gluster-recovery list <volume>`

### remove (TODO)
- requires ssh
Remove a file from all bricks in a volume simultaneously.

It is possible to have files be available at the glusterfs mount point which
are corrupt and can not be removed/rewritten.  Should this situation arise then
this command will attempt to remove the file and its repsective gfid link from
the brick directly.

**WARNING** This command will make irrivocable changes to the filesystem, it is
recommended that a copy of the brick be made before using this command.

### compare
- requires ssh
Compare files between various peers which are, or were, non-arbiter members of a replicated volume.

Example:
 - To compare files from the local node to the first valid member of the specified volume: `gluster-recovery compare <volume>`
 - To compare files from the local node to files of specified peer: `gluster-recovery compare <volume> <peer>`

Lastly, it is also possible to compare files from the local node against
alternate locations which are not currently part of the volume.  This is useful
for comparing against snapshots, backup directories, or even old peers which
have been subsequently replaced.

Example: `gluster-recovery compare <volume> <hostname>:</path/to/brick>`

### gfid2path
Find the path/file of a given gfid.
 - `gluster-recovery gfid2path </path/to/brick> <gfid> [<gfid> ...]`

 ## path2gfid
 Find the gfid of a given path.
 - `gluster-recovery path2gfid </path/to/file> [</path/to/file> ...]`

## Credits
Inspirtation for the `gfid2path()` routine came from gfid-parser. See:
https://gist.githubusercontent.com/semiosis/4392640
