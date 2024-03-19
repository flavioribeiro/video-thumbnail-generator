#!/usr/bin/env python3

"""Video Thumbnail Generator

Usage:
  ./generator <video> <interval> <width> <height> <columns> <output> [<parallelism>]
  ./generator (-h | --help)
  ./generator --version

Options:
  -h --help       Show this screen.
  --version       Show version.
  <video>         Video filepath.
  <interval>      Interval in seconds between frames.
  <width>         Width of each thumbnail.
  <height>        Height of each thumbnail.
  <columns>       Total number of thumbnails per line.
  <output>        Output.
  [<parallelism>] Number of files to process in parallel.
"""

from docopt import docopt
from moviepy.editor import VideoFileClip
from PIL import Image
from click import progressbar
from collections import namedtuple
from multiprocessing import cpu_count, Queue, Process
import glob
import os
import random
import shutil
import math
import tempfile
import sys


TMP_FRAMES_PATH = tempfile.mkdtemp()


def generate_video_thumbnails(args):
    input_path = args['<video>']
    interval = int(args['<interval>'])
    size = (int(args['<width>']), int(args['<height>']))
    columns = int(args['<columns>'])
    output_path = args['<output>']
    parallelism = args.get('[<parallelism>]', cpu_count()*2-1)

    work_queue = Queue()
    work_units = 0

    if os.path.isdir(input_path):
        # Ensure output path is also directory
        if not os.path.isdir(output_path):
            print(
                "If input path is directory then "
                "output path must be directory"
            )
            sys.exit(1)

        # Strip separator so constructing output is uniform
        output_path = output_path.rstrip(os.sep)

        # Add all files in directory for processing
        for file_name in os.listdir(input_path):
            file_path = os.path.join(input_path, file_name)
            if os.path.isfile(file_path):
                # Construct output path for thumbnail using
                # the video files filename
                single_output_path = os.path.join(
                    output_path, os.path.basename(file_path) + ".png"
                )

                work_queue.put((file_path, single_output_path,
                                interval, size, columns,))
                work_units += 1
    else:
        work_queue.put((input_path, output_path, interval, size, columns,))
        work_units += 1

    # Limit the number of parallel jobs if lower number of files
    parallelism = min(int(parallelism), work_units)

    # Start worker processes
    processes = []
    for i in range(parallelism):
        p = Process(target=worker, args=(work_queue,))
        p.start()
        processes.append(p)

    # Block until all processes complete
    for p in processes:
        p.join()


def worker(queue):
    while True:
        try:
            work_unit = queue.get(False)

            # If no work unit then quit
            if not work_unit:
                break
        # Handle exception when no more items in queue
        except:
            break

        input_file, output_file, interval, size, columns = work_unit

        file_name = os.path.basename(input_file)

        # Skip over any thumbnails that exist already
        if os.path.exists(output_file):
            print("[{file_name}] Already exists, skipping".format(
                file_name=file_name))
            continue

        try:
            video_file_clip = VideoFileClip(input_file)
            output_prefix = get_output_prefix()
            generate_frames(file_name, video_file_clip,
                            interval, output_prefix, size)
            generate_sprite_from_frames(output_prefix, columns,
                                        size, output_file)
        except Exception as e:
            print("[{file_name}] Error occurred with file: {error}".format(
                file_name=file_name, error=e))


def generate_frames(file_name, video_file_clip, interval, output_prefix, size):
    duration = video_file_clip.duration
    frame_count = 0
    total_frames = int(duration / interval)
    for i in range(0, int(duration), interval):
        frame_count += 1
        print("[{file_name}] Extracting frame {current}/{total}".
              format(file_name=file_name, current=frame_count,
                     total=total_frames))
        extract_frame(video_file_clip, i, output_prefix, size, frame_count)


def extract_frame(video_file_clip, moment, output_prefix, size, frame_count):
    output = output_prefix + ("%05d.png" % frame_count)
    video_file_clip.save_frame(output, t=int(moment))
    resize_frame(output, size)


def resize_frame(filename, size):
    image = Image.open(filename)
    image = image.resize(size, Image.Resampling.LANCZOS)
    image.save(filename)


def generate_sprite_from_frames(frames_path, columns, size, output):
    frames_map = sorted(glob.glob(frames_path + "*.png"))

    master_width = size[0] * columns
    master_height = size[1] * int(math.ceil(float(len(frames_map)) / columns))

    line, column, mode = 0, 0, 'RGBA'

    try:
        final_image = Image.new(
            mode=mode,
            size=(master_width, master_height),
            color=(0, 0, 0, 0)
        )
        final_image.save(output)
    except IOError:
        mode = 'RGB'
        final_image = Image.new(mode=mode, size=(master_width, master_height))

    for filename in frames_map:
        with Image.open(filename) as image:

            location_x = size[0] * column
            location_y = size[1] * line

            final_image.paste(image, (location_x, location_y))

            column += 1

            if column == columns:
                line += 1
                column = 0

    final_image.save(output)
    shutil.rmtree(frames_path, ignore_errors=True)
    output_file = os.path.basename(output)
    print("[{output_file}] Saved".format(output_file=output_file))


def get_output_prefix():
    if not os.path.exists(TMP_FRAMES_PATH):
        os.makedirs(TMP_FRAMES_PATH)
    return TMP_FRAMES_PATH + os.sep + ("%032x_" % random.getrandbits(128))


if __name__ == "__main__":
    arguments = docopt(__doc__, version='0.0.2')
    generate_video_thumbnails(arguments)
