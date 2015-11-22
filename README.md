# Video thumbnail generator
> Generate thumbnail sprites from videos.

## Why

![image](https://cloud.githubusercontent.com/assets/244265/11234416/b1a67230-8d95-11e5-97a4-c2acdcbf72f7.png)

Almost all video players enhances user's seekbar navigation by providing a thumbnail preview of the moments where the user want to seek, so generate this sprites shouldn't be hard. This is a python script that, given a video, generate a thumbnail sprite image from it.

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

## Example
```shell
$ ./generator videos/27467_1_milkbots_wg_720p.mp4 2 126 73 10 thumbnails.jpg
Extracting 101 frames
.................................................................. Frames extracted.
Saved!
```

![image](https://cloud.githubusercontent.com/assets/244265/11234316/b42913a6-8d94-11e5-865a-128ea8d801f7.png)


## Browser Support

![IE](https://cloud.githubusercontent.com/assets/398893/3528325/20373e76-078e-11e4-8e3a-1cb86cf506f0.png) | ![Chrome](https://cloud.githubusercontent.com/assets/398893/3528328/23bc7bc4-078e-11e4-8752-ba2809bf5cce.png) | ![Firefox](https://cloud.githubusercontent.com/assets/398893/3528329/26283ab0-078e-11e4-84d4-db2cf1009953.png) | ![Opera](https://cloud.githubusercontent.com/assets/398893/3528330/27ec9fa8-078e-11e4-95cb-709fd11dac16.png) | ![Safari](https://cloud.githubusercontent.com/assets/398893/3528331/29df8618-078e-11e4-8e3e-ed8ac738693f.png)
--- | --- | --- | --- | --- |
IE 9+ ✔ | Latest ✔ | Latest ✔ | Latest ✔ | Latest ✔ |


## Contributing

1. Fork it!
2. Create your feature branch: `git checkout -b my-awesome-new-feature`
3. Commit your changes: `git commit -m 'Add some awesome feature'`
4. Push to the branch: `git push origin my-awesome-new-feature`
5. Submit a pull request :]

## License

This code is under [Apache License](https://github.com/flavioribeiro/video-thumbnail-generator/blob/master/LICENSE).
