# Install

### Prereqs
```bash
brew install watchman

npm install -g @sourcescape/cli
```

### Launching

```bash
sourcescape up <project_folder_1> <project_folder_2>
```

You must point the CLI to the directories you want to mount. The indexer will search the directories recursively for Git repos so you can simply hand it a project directory. For example, if you have a projects directory at `~/Projects` with repos `~/Projects/repo1` and `~/Projects/repo2`, you can just tell SourceScape to mount `~/Projects`.

However, it's advised to not go too many levels up as the recursive search can get expensive.

### Upgrading



# Onboarding

Select the repos you want to watch and index.

<img src="images/repo_select.png" height="500" />

Wait for initial index to finish.

<img src="images/indexing.png" height="200" />


# Querying

<img src="images/query_console.png" />

<img src="images/query_console_2.png" />

## Components

**Query Prompt** - This is where you enter your queries. Learn more [here](#queries).

**Language Selector** - Allows you to select the language you want to query in. Right now, only Javascript is fully fleshed out.

**Targeting Indicator** - Shows you what repo you're searching in. Learn more [here](#targeting). Use the [command bar](#command-bar) (cmd+shift+p) to select targeting. 

**Indexing Indicator** - When SourceScape is indexing or re-indexing a repo, you'll see a loading indicator here. You can click it to get an indexing panel showing progress.

**Saved Query Indicator** - You can save queries with cmd+s. If the query you're using is a saved query, there will be an indicator with the name of the query.

**Cache indicator** - 

**Menu** - A menu ^_^

## Queries

The idea behind SourceScape is that you can just type code and find things to search for. For simple queries, it should feel completely intuitive, without the need for a bunch of extra syntax.

Anywhere you see `___` / `...` - you can type here to add to the query.

If you type here, you get an argument.
If you type here, you get an item in the function body.

SourceScape will show you the possibilities of what you can insert into that segment of the query.

Reset from the menu.

### Behind the scenes

Brief description of SrcLog.

Each object has an id.

It can be helpful to take a look at the raw SrcLog for more advanced queries to get an understanding of what's going on, especially as 


### Hover menu

Hovering over an individual object in the query will show a hover menu that allows you to manipulate that object.

Delete

Unset name

Select

Get a reference to that object


Change index




### References

For more advanced queries, it is useful to reference a specific id.

For example, suppose we want to find all calls of any function that returns an object with block as a key


You will also see

G := function () {

}

### Dependencies (experimental)

Dependencies allow you to reach across files

example



## Results

Click the repo link to open the repo locally or on Github
Click the file link to either open the file locally or on Github


### Scrolling

As you query, SourceScape will show the first 10 results.

If you want to get all the results, you will have to click "Fetch all". This loads all the query results into a cache and allows you to scroll through these results. 

### Selection

SourceScape results can span many parts of a file and even across files. It's important to select the right pieces.


## Targeting

SourceScape allows you to target your query to specific 

*

Repo

Repo Branch

Repo SHA

File filter

You can also save targeting with shift+cmd+s


## Command bar

The command bar is the main point of interaction for selecting targeting and getting saved queries.

cmd+shift+p

Repos
Branches and commits (when a repo is selected)
Saved queries
Saved targeting
