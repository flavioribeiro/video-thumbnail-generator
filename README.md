# video-thumbnail-generator
Generate thumbnail sprites from videos.

### Why?
![image](https://cloud.githubusercontent.com/assets/244265/11234416/b1a67230-8d95-11e5-97a4-c2acdcbf72f7.png)

Almost all video players enhances user's seekbar navigation by providing a thumbnail preview of the moments where the user want to seek. This is a python script that, given a video, generate a thumbnail sprite image from it.

### Build

Clone this repository. On project folder:
```shell
$ chmod a+x build && ./build
```

### Run
```shell
$ ./generator --help
Video Thumbnail Generator

Usage:
  ./generator <video> <interval> <width> <height> <columns> <output>
  ./generator (-h | --help)
  ./generator --version

Options:
  -h --help     Show this screen.
  --version     Show version.
  <video>         Video filepath.
  <interval>      Interval em seconds between frames.
  <width>         Width of each thumbnail.
  <height>        Height of each thumbnail.
  <columns>       Total number of thumbnails per line.
  <output>        Output.
```

### Example
```shell
$ ./generator videos/27467_1_milkbots_wg_720p.mp4 2 126 73 10 thumbnails.jpg
Extracting 101 frames
.................................................................. Frames extracted.
Saved!
```

![image](https://cloud.githubusercontent.com/assets/244265/11234316/b42913a6-8d94-11e5-865a-128ea8d801f7.png)

#### License

This code is under [Apache License](https://github.com/flavioribeiro/video-thumbnail-generator/blob/master/LICENSE).
