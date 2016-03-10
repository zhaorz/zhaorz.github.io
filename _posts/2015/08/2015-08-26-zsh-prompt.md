---
layout: post
title: Customize your zsh prompt
tags: [zsh]
---

![zsh prompt]({{ site.baseurl }}/img/2015-08-26-zsh-prompt/zsh-splash.png)

Recently, I switched from bash to zsh. Both are very powerful shells, and the differences aren't huge. I mainly like zsh for its extra autocompletion features, but there are a variety of plugins you can install to further enhance zsh. Here, I'll talk about prompt customization.

<!--excerpt-->

Customization is about adapting something to best fit your own needs. Tweaking things for personal flair is like marking your territory on something. People who customize their cars, for example, take great pride in the modifications and details they add to them. I don't own a car. But I do own a computer, and I spend a good deal of time staring into a terminal, so I thought I might as well make it look decent.

The process of customizing things inherently leads to _over_-customization. In a terminal, a long prompt takes up valuable space, and may even hide important information. I narrowed my prompt to 5 elements:

1. **Hostname:** Who you are.
2. **Path:** Where you are.
3. **Prompt:** Where to start typing.
4. **Git information:** Immediately know if you're in a repo.
5. **Timestamp:** Gives context if you scroll back up.

Since I'm using zsh, I've chosen to use [oh-my-zsh](https://github.com/robbyrussell/oh-my-zsh) to manage themes and plugins. All of my configuration code is in a `.zsh-theme` file. My `.zshrc` then points to it with

~~~sh
ZSH_THEME="myCustomTheme"
~~~

And, for reference, [here are the docs on zsh prompt expansions](http://zsh.sourceforge.net/Doc/Release/Prompt-Expansion.html).

## Hostname, path, and prompt

The hostname, path, and prompt make up the left-hand-side of my zsh prompt. These elements are what most default shells include in their prompts.

~~~ shell
#
# Main prompt
#

local host_name="%{$fg[cyan]%}赵"
local path_string="%{$fg[yellow]%}%~"
local prompt_string="»"

# Make prompt_string red if the previous command failed.
local return_status="%(?:%{$fg[blue]%}$prompt_string:%{$fg[red]%}$prompt_string)"

PROMPT='${host_name} ${path_string} ${return_status} %{$reset_color%}'
~~~

Although my computer's actual **hostname** is `zhao`, my last name, I've chosen to save 3 characters of space by using the Chinese character, `赵`, instead. The character actually takes up just under 2 regular characters of space, due to the way Unicode renders CJK (Chinese, Japanese, Korean) characters.

Any standard Unicode works in the bash prompt, so the possibilities are endless. I've seen a lot of themes use `λ` in place of hostname, which is pretty cool as well.

In terms of the **path**, I'm using the escape sequence `%~`. This ensures paths that start with `$HOME` get simplified to just `~/...`. Thus, `/Users/Richard/Documents` gets truncated to `~/Documents`. Other path variants can be found in the [zsh prompt docs](http://zsh.sourceforge.net/Doc/Release/Prompt-Expansion.html).

As the last standard element, I chose `»` (U+00BB) instead of the traditional `$`. `return_status` uses the escape sequence `%?` and colors the prompt accordingly.

In zsh, `PROMPT` corresponds to the left-hand prompt. It's equivalent to bash's `PS1`.

## Right hand prompt

![zsh rprompt]({{ site.baseurl }}/img/2015-08-26-zsh-prompt/zsh-rprompt.png)

Zsh conveniently allows us set a right-hand prompt, without any extra effort, with the `RPROMPT` variable. I chose to store git and time information on the right-hand side.

~~~ shell
# oh-my-zsh $(git_prompt_info) puts 'dirty' behind branch
git_custom_prompt() {
  # branch name (.oh-my-zsh/plugins/git/git.plugin.zsh)
  local branch=$(current_branch)
  if [ -n "$branch" ]; then
    # parse_git_dirty echoes PROMPT_DIRTY or PROMPT_CLEAN (.oh-my-zsh/lib/git.zsh)
    echo "$(parse_git_dirty)$ZSH_THEME_GIT_PROMPT_PREFIX$branch$ZSH_THEME_GIT_PROMPT_SUFFIX"
  fi
}
~~~

Oh-my-zsh comes with a git plugin with a `git_prompt_info` function, but it put the branch 'dirty' information behind the branch name. The above code puts this information in front of the branch name, which ensures the branch names are nicely aligned on the right hand side of the shell.




















