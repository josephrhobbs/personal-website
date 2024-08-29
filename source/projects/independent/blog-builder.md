# Blog Builder

~

When I was in middle school, my parents began running a CrossFit program at their local gym.  As a ten-year-old CrossFit enthusiast, my parents entrusted me with the responsibility of maintaining the program website and posting the daily workout each day.

This sounded like a complicated responsibility for a ten-year-old, but in reality it was no more complicated than pressing "Publish" on the Blogger website every night.  However, the job still sparked my interest in web development that would continue throughout my adolescent years.

When I was in high school, I would start two other websites: one a fitness blog for my high school's Junior ROTC program and another as a project for a class on Contemporary Issues.

During my time in college, as I became more proficient in programming, I discovered that I didn't like services like WordPress and Blogger.  I found that they had too many unnecessary features and too few features that I actually wanted.  Furthermore, I didn't like my inability to manage URL structure or page layout as I desired.  For these reasons, I began developing my own web framework, called the Blog Builder.

This website is itself built by the Blog Builder framework, which makes this catalog of my projects itself one of my most actively maintained projects.  I particularly enjoy this because it allows me to experiment with and continually improve my own software.

## Development

The Blog Builder framework is written in pure stable Rust 1.80.  I made this selection primarily out of a desire to improve my ability to write robust, reliable Rust code to perform a complex task (constructing a static website).

## Features

The Blog Builder currently supports plain text, hyperlinks, headers, menus, tiles, images, italics, and boldface.

## Usage

I designed Blog Builder to be very simple to use.  Because it is built to serve static content, I write all of my webpages in pseudo-Markdown source files and then pass them to the Blog Builder for compilation to HTML.

## Source Code

The source code for the Blog Builder is publicly available and licensed under the MIT License.  Below is the link to its GitHub repository.

[https://github.com/josephrhobbs/blog-builder](https://github.com/josephrhobbs/blog-builder)