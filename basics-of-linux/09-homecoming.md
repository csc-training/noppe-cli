# Homecoming

All right. It's now time to put everything you've learnt into practice with the help of a `.bashrc` file.

1. Make sure you are in your home directory. 
2. Long list the contents of the directory.
3. Observe the `.bashrc` entry in the listing.
4. View the file's permissions and contents.
5. Open the file in a text editor.

Is everything OK so far?

The `.bashrc` file is a script that runs whenever a user logs in. Any actions that you define in this file will be performed and available throughout your session.

Great, let's continue.

6. Add the following aliases: `alias k9='kill -9` and `alias ...='cd ../..'`
7. Create a permanent PS1 for your sessions: `PS1='\h \w \$ '`

Save the file and then exit the text editor. Next, run the `source .bashrc` command to activate the file without having to log out and back in again. Start the `sleep 1000` command in the background, then terminate it using your new `k9` alias.

::: terminal
{{USERNAME}}@{{HOSTNAME}}:~$ source .bashrc 
{{HOSTNAME}} ~ $ sleep 1000 &
[1] 490
{{HOSTNAME}} ~ $ k9 490
{{HOSTNAME}} ~ $ 
[1]+  Killed                  sleep 1000
{{HOSTNAME}} ~ $ █
:::

Still with me? Great, let's move on.

8. Add the following and remove the previous PS1 of yours.

```sh
# Location for weather lookup
LOCATION="Helsinki"

# Fetch weather in the background on login
curl -s --max-time 3 "wttr.in/${LOCATION}?format=1" > ~/.weather 2>/dev/null &

# Read weather from the cache
get_weather() {
    cat ~/.weather 2>/dev/null
}

# Prompt with weather
PS1='\u@\h:\w $(get_weather)@'"${LOCATION}"' \$ '
```

9. Save the file, exit the editor, log out of your session and log back in.
10. Verify the changed PS1 and the functionality of the aliases.

Now let's wrap things up in the [Afterword](10-afterword.md).
