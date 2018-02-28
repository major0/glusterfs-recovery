# GlusterFS Recovery Tool

This tool aims to assist administrators in recovering files in a GlusterFS
filesystem in the event that GlusterFS is not capable of healing the file
itself.

## Usage
`glusterfs-recovery <command> [args]`

## Commands

### list
List files which need fixing.
 - `gluster-recovery list <volume>`

### compare
Compare files between bricks.
 - `gluster-recovery compare <volume>`
 - `gluster-recovery compare <volume> <peer>`
 - `gluster-recovery compare <volume> <peer>:</path/to/old/brick>`
 - `gluster-recovery compare <volume> <oldpeer>:</path/to/old/brick>`

### gfid2path
Find the path/file of a given gfid.
 - `gluster-recovery gfid2path </path/to/brick> <gfid> [<gfid> ...]`

 ## path2gfid
 Find the gfid of a given path.
 - `gluster-recovery path2gfid </path/to/file> [</path/to/file> ...]`

## Credits
Inspirtation for the `gfid2path()` routine came from gfid-parser. See:
https://gist.githubusercontent.com/semiosis/4392640
