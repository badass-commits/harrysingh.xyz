---
layout: post
title: "What's in the .git folder"
date: 2023-05-21 15:56:42 -0600
---
Each of the dozens of git repos on your machine contains a .git folder. But you may have never thought about the details of its contents. You know that somehow the folder holds the history of every version of every file ever committed to the repository. You just don’t know how.

The contents are less mysterious than you think. For obvious reasons, git optimizes the contents of the .git folder for size and speed. So you can’t browse into it and see your files. The object files are all named after their guid, and the data is [zlib](https://zlib.net/) compressed. But the structure and organization is documented and understandable.

![git](/assets/images/posts/git.png)

I’m not going to go into a full explanation of the files here. Others, like Rob Richardson ([blog](https://robrich.org/), [twitter](https://twitter.com/rob_rich)) have explained it better than I ever will. It was Rob’s talk at CodeMash that helped me understand how the contents of the .git folder worked. I just created a graphic from the info he shared. Additional details are available at [GitReady.com](https://gitready.com/advanced/2009/03/23/whats-inside-your-git-directory.html).

I’ll simply summarize by saying that the files can be grouped into five categories:

1. **Objects** - (blue)These represent the files and changes. Objects can be further divided into commits, trees, and blobs.
2. **Refs** - (red)These are human-readable files that organize the objects
3. **Logs** - (green)These are used to quickly generate logs displayed to the user.
4. **Config** - (light gray)There are files used to config git’s behavior
5. **Temp** - (gray)These are temporary files for information that git needs to hold between command-line actions.
