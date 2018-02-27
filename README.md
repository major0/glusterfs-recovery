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

### gfid
Resolve the gfid of a given file name.
 - `gluster-recovery gfid </path/to/brick> <gfid> [<gfid> ...]`

### compare
Compare files between bricks.
 - `gluster-recovery compare <volume> <remote node>`

## Credits
Inspirtation for the `gfid2path()` routine came from gfid-parser. See:
https://gist.githubusercontent.com/semiosis/4392640
