---
author: Matt Pritchard
title: Sample doc
date: 2023-08-25
description: A sample of a documentation page
tags: ["language", "example"]
layout: doc
draft: true
---

## First heading

Vivamus iaculis metus sed magna porta tincidunt. Aliquam molestie eget orci eu elementum. Integer pellentesque dolor sit amet suscipit maximus. Duis consequat, massa vitae volutpat rhoncus, erat augue venenatis velit, a auctor leo nulla nec turpis. Nunc ut libero sapien. Vivamus aliquam ultrices vestibulum. Sed sit amet vestibulum dolor, ut vehicula diam. Sed felis purus, feugiat vitae vulputate quis, sodales vitae dui. Pellentesque volutpat fringilla sapien varius condimentum. Integer odio massa, pharetra at bibendum vitae, aliquam nec erat.

## Second heading

Vivamus iaculis metus sed magna porta tincidunt. Aliquam molestie eget orci eu elementum. Integer pellentesque dolor sit amet suscipit maximus. Duis consequat, massa vitae volutpat rhoncus, erat augue venenatis velit, a auctor leo nulla nec turpis. Nunc ut libero sapien. Vivamus aliquam ultrices vestibulum. Sed sit amet vestibulum dolor, ut vehicula diam. Sed felis purus, feugiat vitae vulputate quis, sodales vitae dui. Pellentesque volutpat fringilla sapien varius condimentum. Integer odio massa, pharetra at bibendum vitae, aliquam nec erat.

## Third heading

Can you link straight to this in the table of contents? Vivamus iaculis metus sed magna porta tincidunt. Aliquam molestie eget orci eu elementum. Integer pellentesque dolor sit amet suscipit maximus. Duis consequat, massa vitae volutpat rhoncus, erat augue venenatis velit, a auctor leo nulla nec turpis. Nunc ut libero sapien. Vivamus aliquam ultrices vestibulum. Sed sit amet vestibulum dolor, ut vehicula diam. Sed felis purus, feugiat vitae vulputate quis, sodales vitae dui. Pellentesque volutpat fringilla sapien varius condimentum. Integer odio massa, pharetra at bibendum vitae, aliquam nec erat.

The `command` shortcode generates terminal output for either `bash`, `powershell`, or `sql` shell languages. The following example generates a block with a default bash command prompt.

<!-- markdownlint-disable MD037 -->
{{< example lang="hugo" >}}
{{</* command */>}}
export MY_VAR=123
{{</* /command */>}}
{{< /example >}}
<!-- markdownlint-enable MD037 -->

## Arguments

The shortcode supports the following arguments:

{{< table >}}
| Argument  | Required | Description |
|-----------|----------|-------------|
| user      | No | Optional user to add to the prompt, e.g. "user". |
| host      | No | Optional host to add to the prompt, e.g. "localhost". |
| prompt    | No | Optional prompt override, e.g. "PS C:\Users\User>". |
| shell     | No | Type of shell, either "bash" (default), "powershell", or "sql". |
| class     | No |  Optional class attribute of the command element. |
{{< /table >}}

## Examples

Change the style and language of your command prompt with shortcode arguments.

### Bash

Specify `user` and `host` to add the user context to the prompt. In addition, use `(out)` to specify an output line and use `\` to denote a line continuation.

<!-- markdownlint-disable MD037 -->
{{< example lang="hugo" >}}
{{</* command user="user" host="localhost" */>}}
export MY_VAR=123
echo "hello"
(out)hello
echo one \
two \
three
(out)one two three
echo "goodbye"
(out)goodbye
{{</* /command */>}}
{{< /example >}}
<!-- markdownlint-enable MD037 -->

Here's some Python code

```python
def hello():
    print("hello world")
```
