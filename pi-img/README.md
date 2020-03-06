# pi-img

Helps to manage disk images for single board computers: create, flash, mount, modify.

The main and the most exciting feature is a nice colored output, what else could you ever dream of?!
Other features are so minor and insignificant so you'd better stop reading here.

For inline help run `pi-img man` (or without arguments, or see USAGE at the top of the script).

wat? You're still here? Right, who likes to be bothered by reading boring useless docs.
Ok, so review EXAMPLES section at the bottom of help message for quick start.
Why would you want to do so? Ok, you've caught me, you wouldn't, because `wget`, `dd`, and `mount` is all you need.
I would, because it's makes images flashing easy and quick, and it mounts all image partitions at once, and it applies required changes to the image in a handy way and can make it as small as possible, and... who cares? I like it!

WARNING:
- Was originally designed for and tested with Raspbian only!
- Unstable yet, need to thoroughly test it and prepare for generic source images, use at your own risk.
