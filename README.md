# socco-ng

![build](https://github.com/regadas/socco-ng/workflows/ci/badge.svg)
[![GitHub license](https://img.shields.io/github/license/regadas/socco-ng.svg)](./LICENSE)
![Maven Central](https://img.shields.io/maven-central/v/io.regadas/socco-ng_2.13.10)

**socco-ng** is a Scala compiler plugin to generate documentation from Scala source files. This is a fork from [criteo/socco](https://github.com/criteo/socco).

It produces HTML documents that display your comments alongside your code. Comments are passed through Markdown, and the Scala code is syntax highlighted, typed and linked to the appropriate API Doc.

## Usage

If you use SBT, add the following settings to enable the plugin:

```scala
autoCompilerPlugins := true
addCompilerPlugin("io.regadas" %% "socco-ng" % "0.1.8")
```

If you are using scalac directly, add the following option:

```sh
-Xplugin:io.regadas.socco-ng_2.13.10-0.1.8.jar
```

This can be followed by any of the available options:

- `-P:out:$outDir` to specify the output directory.
- `-P:style:$stylesheetPath` to specify a custom stylesheet.
- `-P:packagge_$packageName:$scalaDocUrl` to specify a Scala API doc to link.
- `-P:header:$headerPath` to specify a custom HTML header.
- `-P:footer:$footerPath` to specify a custom HTML footer.

## Syntax

The plugin will handle all scala source files starting with a comment line like:

```
// Example: (.*)
```

The captured group will be used as the example title in the generated HTML documents.

The comments can use Markdown syntax, and will be correctly rendered to the generated documentation.

Also, there is a special kind of comment:

```
// @className
```

When added on top of a code block, it will add the CSS class to the generated block. Allowing you to style it further wit CSS.

## Prior art

- [Docco](https://jashkenas.github.io/docco/) generates this kind of layout for CoffeeScript code. It has been ported to several other languages.
- [Tut](https://github.com/tpolecat/tut) is a documentation tool that allow to embed (and compile) Scala code into Markdown documents. Which is exactly the opposite of Socco 😛.
- [SXR](https://github.com/sbt/sxr) is Scala compiler plugin that turn source code into syntax highlighted and browsable HTML documents. It is outdated now but was a good source of inspiration for socco.

## License

This project is licensed under the Apache 2.0 license.
