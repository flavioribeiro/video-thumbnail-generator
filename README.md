# Video thumbnail generator
Generate thumbnail sprites from videos.

## Why

![image](https://cloud.githubusercontent.com/assets/244265/11234416/b1a67230-8d95-11e5-97a4-c2acdcbf72f7.png)

Almost all video players enhances user's seekbar navigation by providing a thumbnail preview of the moments where the user want to seek, so generate this sprites shouldn't be hard. This is a python script that, given a video, generates a thumbnail sprite image from it.

## Build

1. Clone it:

```sh
$ git clone git@github.com:flavioribeiro/video-thumbnail-generator.git
```

2. Then go to the project's folder:

```sh
$ cd video-thumbnail-generator
```

3. And finally run:
```shell
$ chmod a+x build && ./build
```

## Run
```shell
$ ./generator --help
Video Thumbnail Generator

Usage:
  ./generator <video> <interval> <width> <height> <columns> <output> [<parallelism>]
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
  [<parallelism>]   Number of files to process in parallel
```

## Example
**Single file**
```shell
$ ./generator samples/sample.mp4 60 300 200 2 output/sample.mp4.png
[sample.mp4] Extracting frame 1/3
[sample.mp4] Extracting frame 2/3
[sample.mp4] Extracting frame 3/3
[sample.mp4.png] Savedacted.
Saved!
```

**Directory**
```shell
$ ./generator samples/ 60 300 200 2 output/
[sample copy.mp4] Extracting frame 1/3
[sample.mp4] Extracting frame 1/3
[sample copy.mp4] Extracting frame 2/3
[sample.mp4] Extracting frame 2/3
[sample copy.mp4] Extracting frame 3/3
[sample.mp4] Extracting frame 3/3
[sample copy.mp4.png] Saved
[sample.mp4.png] Saved
```

![image](https://cloud.githubusercontent.com/assets/244265/11234316/b42913a6-8d94-11e5-865a-128ea8d801f7.png)


## Contributing

1. Fork it!
2. Create your feature branch: `git checkout -b my-awesome-new-feature`
3. Commit your changes: `git commit -m 'Add some awesome feature'`
4. Push to the branch: `git push origin my-awesome-new-feature`
5. Submit a pull request :]

## License

This code is under [Apache License](https://github.com/flavioribeiro/video-thumbnail-generator/blob/master/LICENSE).
