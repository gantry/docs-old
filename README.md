Gantry Documentation
====================
This repository contains the source of the Gantry documentation, currently accessible at <http://gantry-framework.com/documentation>.

The documentation is contained in [Docs/](Docs) and is structured in folders, exactly as you see them on the main website.

You can read all of the documentation within, as it's just in plain text files, marked up with [Markdown](http://daringfireball.net/projects/markdown/).

If you would like a local copy of the documentation, you can either [download it](https://github.com/gantry/docs/archive/master.zip) or you can clone the reopistory by running the follwing command:

~~~ .bash
git clone git://github.com/gantry/docs gantry-docs
~~~


Contributing
------------
Contributing to the documentation is very simple. Feel free to fork the repository, add your changes and give back by issuing a pull request. You can even edit the docs directly on GitHub, without having to ever download the files. Make sure to follow the conventions before issuing a pull request.

You are also very welcome to make any suggestions or report any kind of problem with the documentation by opening a new [Issue](https://github.com/gantry/docs/issues/new).

If you decide to fork for providing new content as commits. Please ensure you create a branch for your changes, before making them. This will make the process of integrating them more easier. Every change must pass through the `staging` branch first, so please ensure your pull-requests are directed to the proper branch.

To get started with a local environment into the proper `staging` branch, you can run these commands:

~~~ .bash
git clone git://github.com/gantry/docs gantry-docs
cd gantry-docs
git checkout -b staging origin/staging
~~~


Conventions
-----------
This is a list of few conventions we follow when writing documentation that help keep the repository well organized and consistent. Feel free to use any other file in the docs as reference. We also have a [skeleton](Skeleton.md) with all the conventions in place and with many examples of Markdown in use.

* Every change/pull request must be applied or requested to the [staging branch](https://github.com/gantry/docs/tree/staging). Once reviewed, approved and pulled, it will get merged into the **master** branch and automatically picked up by the website.

* Folder and file names must be written in snake_case and always lowercase. For example, if you wanted to convert “How to Install” in snake_case, you would name it “how_to_install”. Filenames in the "assets" folders must be instead dash concatenated.

* There are some reserved names that can’t be used for anything but the scope they are intended for:
    * **README.md**: [ _file_ ] This is a reserved name of GitHub, used to describe the content of a particular repository directory, like this you are reading right now.

    * **TOC.md**: [ _file_ ] TOC (Table Of Content) does represent the structure of a project. Its content is a list of links to the various documents in the project. The TOC is represented as sidebars in the [Gantry Docs](http://gantry-framework.com/documentation).

    * **INDEX.md**: [ _file_ ] This file defines the default content for a folder. Exactly like HTML pages, if you hit a folder without specifying any file, INDEX.md (if found) will be assumed.

    * **REDIRECT.md**: [ _file_ ] This file sorely purpose is to redirect projects to different locations. For example, if a project `/docs/project/subproject/` contains a `REDIRECT.md`, when hitting on the web the `subproject` page, you’ll get redirect to `project`. By default it takes you back one level, although you can configure where to redirect to through YAML headers ([read more about YAML headers below](#yaml-headers)).

    * **assets**: [ _folder_ ] When the project requires assets, such as images, they can be placed in the `assets` folder. Any filename inside `assets` must be lower-case and dash concatenated.

* Every header, except for the title one, must be preceeded by 2 empty lines and succeeded by no empty line.

* Headers sub lines (`=` and `-`) must always align to the header text. Because this can easily get confusing, be sure to use a mono-spaced fonts. Here a couple of examples of well aligned headers:

    ~~~
    Header H1
    =========

    Header H2
    ---------
    ~~~


YAML Headers
------------
Our Markdown implementation uses special [YAML headers](http://www.yaml.org/spec/1.2/spec.html). These headers are encapsuled in between a set of three dashes and an empty line. This is how a YAML header looks like:

~~~
---
title: Project Title
breadcrumb: /joomla:Joomla/!extensions:Extensions/project:Project

---
~~~

The headers allow for a much flexible output. For example we can define a title of a Markdown file based on its header title variable, rather than the file name itself.

Below is a list of supported `YAML` variables that can be used and a description on what they do:

* **title**: The title of the article. This is used whenever a page needs to be referenced. When the title is set on a `TOC` file, it globalize the title for each document in the project itself.

    ~~~
    ---
    title: Hello World!

    ---
    ~~~

* **description**: Describes the project. This is usually set in the `TOC` and should describe the project in a generic way, although it is also possible to override the `TOC` description from another MD file.

    The description supports Markdown inline syntax, such as _strong_, _italic_, _links_. You should not be using anything else (ie, _headers_, _images_ and such).

    ~~~
    ---
    description: The most powerful project you have *ever* seen

    ---
    ~~~


* **breadcrumb**: _(defaults: false)_ Represents the pathway to the current project. The format of the breadcrumb is a UNIX path format with each folder being the real path and the display name of the folder, separated by `:`.

    For example, for a project that resides at `/wordpress/extensions/project`, the breadcrumb format would look like `/wordpress:Wordpress/!extensions:Extensions/project:Project/`.

    When a folder starts with the exclamation point `!`, it means it won't be converted into a clickable link, otherwise it will.

    It is important to remember that the pathway follows the real Documentation folder structure, it has to start from the root and it can't miss folders in between.

    ~~~
    ---
    breadcrumb: /joomla:Joomla/!extensions:Extensions/project:Project/`

    ---
    ~~~

* **redirect_to**: _(defaults: ../)_ This property can only be used in `REDIRECT.md` files and allows to have a project redirecting to a different specified path. The path to redirect to can be either relative or absolute, by default it redirects one level up.

    Examples:

    ~~~
    ---
    redirect_to: ../../

    ---
    ~~~

    ~~~
    ---
    redirect_to: /joomla/

    ---
    ~~~

If you have any question feel free to open an [Issue](https://github.com/gantry/docs/issues/new).

_The RocketTheme Team_
