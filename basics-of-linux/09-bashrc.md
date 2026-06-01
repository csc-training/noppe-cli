# .bashrc

::: beware
Generated place holder content. Needs work.
:::

Every time you open a new interactive terminal session, Bash runs a script called `.bashrc` from your home directory. It is a regular text file that you can edit to configure your shell environment: define aliases, customise the prompt, and add your own functions.

Let's look at what is already in it.

## Viewing .bashrc

Use `cat ~/.bashrc` or `less ~/.bashrc` to read the current file.

::: note
Files whose names begin with a `.` are hidden by default. Use `ls -la` to see them.
:::

## Aliases

An alias is a shortcut for a longer command. You define one with the syntax `alias name='command'`.

Open `.bashrc` in a text editor and add the following lines:

```bash
alias ll='ls -la'
alias ..='cd ..'
```

After saving, reload the file with `source ~/.bashrc`. Now try out `ll` and `..`.

::: tip
`source` (or its shorthand `.`) executes a file in the current shell session, so changes take effect immediately without opening a new terminal.
:::

::: question
Can you come up with an alias of your own?
:::

## Customising PS1

We experimented with `PS1` temporarily in [chapter 1.1](01.1-cli.md). Adding the assignment to `.bashrc` makes it permanent.

Add a custom `PS1` to your `.bashrc`:

```bash
PS1='\u@\h \w \$ '
```

Reload with `source ~/.bashrc` and observe the change.

## Weather in PS1

As a finishing touch, let's pull in live weather data. The service `wttr.in` provides a compact one-liner format:

```
curl -s "wttr.in/Helsinki?format=1"
```

This returns something like `⛅ +15°C` — short enough to sit comfortably in a prompt.

To avoid slowing down every prompt redraw, we fetch the data once in the background when the terminal opens and cache the result in `~/.weather`. A small function then reads that file each time the prompt is drawn.

Add the following to your `.bashrc`:

```bash
# Fetch weather in the background on login
curl -s --max-time 3 "wttr.in/Helsinki?format=1" > ~/.weather 2>/dev/null &

# Read weather from the cache
get_weather() {
    cat ~/.weather 2>/dev/null
}

# Prompt with weather
PS1='\u@\h:\w $(get_weather) \$ '
```

::: note
Single quotes around the `PS1` value are important here. They prevent `$(get_weather)` from being evaluated once at assignment — instead it is called fresh on every prompt display.
:::

Reload with `source ~/.bashrc`. Open a new terminal session and watch the weather appear.

::: question
Can you change the city to your own location? What other `?format=` values does `wttr.in` support?
:::

Now let's wrap things up in the [Afterword](10-afterword.md).
