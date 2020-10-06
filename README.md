# Multi-threading Note

## Three Ways to Create Threads

```cpp
#include <thread>
```

- Function Pointer
- Function Objects
- Lambda

## Function Pointer

```cpp
#include <iostream>
#include <thread>

void thread_A()
{
    for(int i = 0; i < 10000; i++);
        std::cout<<"I'm thread A! "<<std::endl;
}

int main()  
{
    std::thread threadObj(thread_A);
    sleep(5);
    threadObj.join();
    return 0;
}
```

## Function Objects

## Options

```yml
title: Your awesome title
lang: # default: en
description: Write an awesome description for your new site here

readme_index:
  with_frontmatter: true

## optional settings ##
direction: # default: auto, syntax: [ltr|rtl]

meta:
  key1: value1
  key2: value2

google:
  gtag:
  adsense:

mermaid:
  custom: # mermaid link
  initialize: # mermaid options, default: {}

# also available via file: _include/assets/custom.scss
scss:

# also available via file: _include/assets/custom.js
script:

# also available via file: _data/translate.yml
translate:
  # shortcodes
  danger:
  note:
  tip:
  warning:
  # 404
  not_found:
  # copyright
  revision:
  # search
  searching:
  search:
  search_docs:
  search_results:
  search_results_found: # the "#" in this translate will replaced with results size!
  search_results_not_found:

## optional plugins ##
plugins:
  - jemoji
  - jekyll-avatar
  - jekyll-mentions
```

## Writing

Document writing specifications, please refer to [rundocs.io](https://rundocs.io) for details

## The license

The theme is available as open source under the terms of the MIT License
