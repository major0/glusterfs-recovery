# GlusterFS Recovery Tool

This tool aims to assist administrators in recovering files in a GlusterFS
filesystem in the event that GlusterFS is not capable of healing the file
itself and once other options such as splitmount have failed or are not
applicable to the given failure scenario.

See: https://joejulian.name/post/glusterfs-split-brain-recovery-made-easy/

### Requirements
These tools need to be run as root on a node which is part of a gluster volume.
Further more, many of the commands expect ssh to be usable for contacting other
nodes w/out a password prompt (ssh `authorized_leys` configured appropriately).

### Credits
This tool contains the routine `gfid2path()` which was inspired by the
`gfid-parser` utility by semiosis. See: https://gist.githubusercontent.com/semiosis/4392640

# Commands

## help
Display help about the specified command, or generic help if no command is specified.

**Example:**
```
# gluster-recovery help list
```

## ls | list
List which files on the local node are in need of healing.

**Example:**
```
# gluster-recovery list <volume>
```

## rm | remove
*note: requires ssh*

Remove a file from all bricks in a volume simultaneously.

It is possible to have files be available at the glusterfs mount point which
are corrupt and can not be removed/rewritten.  Should this situation arise then
this command will attempt to remove the file and its repsective gfid link from
the brick directly.

**WARNING** This command will make irrivocable changes to the filesystem, it is
recommended that a copy of the brick be made before using this command.

**Examples:**

To perform a dry-run of a remove and see what the tool will do:
```
# gluster-recovery remove <volume> --dry-run </path/to/file>
```

To remove a file:
```
# gluster-recovery remove <volume> </path/to/file>
```

To remove a directory:
```
# gluster-recovery remove <volume> -r </path/to/directory>
```

## cmp | compare
*note: requires ssh*

Compare files between various peers which are, or were, non-arbiter members of a replicated volume.

**Example:**

To compare files from the local node to the first valid member of the specified volume:
```
# gluster-recovery compare <volume>
```

To compare files from the local node to files of specified peer:
```
# gluster-recovery compare <volume> <peer>
```

Lastly, it is also possible to compare files from the local node against
alternate locations which are not currently part of the volume.  This is useful
for comparing against snapshots, backup directories, or even old peers which
have been subsequently replaced.

**Example:**
```
# gluster-recovery compare <volume> <hostname>:</path/to/brick>
```

## gfid2path
Find the path/file of a given gfid.

**Example:**
```
# gluster-recovery gfid2path <volume> <gfid>
```

## path2gfid
Find the gfid of a given path.

**Example:**
```
# gluster-recovery path2gfid </path/to/file>
```
