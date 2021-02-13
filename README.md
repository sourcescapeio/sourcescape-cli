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

# Onboarding

First, select the repos you want to watch and index.

<img src="images/repo_select.png" height="500" />

Wait for the initial index to finish.

<img src="images/indexing.png" height="200" />


# Querying

<img src="images/query_console.png" />

<img src="images/query_console_2.png" height="250"/>

## Components

**Query Prompt** - This is where you enter your queries. Learn more [here](#queries).

**Language Selector** - Allows you to select the language you want to query in. Right now, only Javascript is fully fleshed out.

**Targeting Indicator** - Shows you what repo you're searching in. Learn more [here](#targeting). Use the [command bar](#command-bar) (cmd+shift+p) to select targeting. 

**Indexing Indicator** - When SourceScape is indexing or re-indexing a repo, you'll see a loading indicator here. You can click it to get an indexing panel showing progress.

**Saved Query Indicator** - You can save queries with cmd+s. If the query you're using is a saved query, there will be an indicator with the name of the query.

**Cache indicator** - This indicates whether or not you're using the cache, which enables [scrolling](#scrolling) through the [result](#results) set.

**Menu** - A menu ^_^

## Queries

The idea behind SourceScape is that you can just type code and find things to search for. For simple queries, it should feel completely intuitive, without the need for a bunch of extra syntax beyond your understanding of the language itself.

Anywhere you see `___` / `...` - you can add to the query.

This is context dependent of course.

If you type here, you get an argument:

<img src="images/add_arg.png" />

If you type here, you get an item in the function body:

<img src="images/add_body.png" />

SourceScape will show you the possibilities of what you can insert into that segment of the query.

You can Reset the query console from the menu.

### Behind the scenes

For more advanced queries, it's helpful to have an understanding of what's going on behind the scenes.

As you're modifying queries in the visual interface, you're actually manipulating an underlying query language called SrcLog. SrcLog is a logic programming language, basically a very stripped down version of ProLog or DataLog.

There are variables, denoted by capital letters A-Z. You can also define constraints on both the variables and relationships behind the variables.

For example:
```prolog
javascript::function(A).
javascript::return(B).
```
says A must be a function and B must be a return.

Then you can have 
```
javascript::function_contains(A, B).
```
to denote that function A must contain return B.


A query like this:

<img src="images/big_query.png" />

Will break down into 
```prolog
%dialect(javascript).

javascript::function(A).

javascript::return(B).

javascript::jsx-element(C).

javascript::identifier(D)[name = "div"].

javascript::jsx-attribute(E)[name = "style"].

javascript::object(F).

javascript::object-property(G)[name = "marginLeft"].

javascript::function_contains(A, B).

javascript::return(B, C).

javascript::jsx_tag(C, D).

javascript::jsx_attribute(C, E).

javascript::jsx_attribute_value(E, F).

javascript::object_property(F, G)[name = "marginLeft"].
```

It can be helpful to take a look at the raw SrcLog for more advanced queries to get an understanding of what's going on.


### Hover menu

<img src="images/hover_menu_1.png" />

Hovering over an individual object in the query will show a hover menu that allows you to manipulate that variable. This is also context sensitive.

<img src="images/hover_menu_2.png" />
<img src="images/hover_menu_3.png" />

From the menu, you can delete the object, unset its name, [select](#selection) the object, get a [reference](#references) to the object, or change / unset its index.


### References

For more advanced queries, it is useful to reference a specific variable.

For example, suppose we want to find all calls of any function that returns an object with block as a key

We can easily get the function down:

<img src="images/ref_1.png" />

To get calls of that function, you can hover over the function object and select "Reference"

<img src="images/ref_2.png" />

This will get you a reference to the function, which you can turn into a call with `ref[A]()`.

<img src="images/ref_3.png" />

With these references, the interface will annotate the function with `A := ` to make the query a bit clearer.

<img src="images/ref_4.png" />


### Dependencies (experimental)

Dependencies allow your queries to reach across files.

<img src="images/dep.png" />

For example, this query will search for all classes with a property `test` that is a class D with a render method. D can be in another file, SourceScape will automatically detect the imports and exports.

## Results

Click the repo link to open the repo locally or on Github
Click the file link to either open the file locally or on Github


### Scrolling

As you query, SourceScape will show only the first 10 results.

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
