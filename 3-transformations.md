## Transforming data

The data in the `items_owned` column is a set of items in a list. The list is in square brackets and each item is in single quotes. Before we split the list into individual items in the next section, we first want to remove the brackets and the quotes.

1. Click the down arrow at the top of the `items_owned` column. Choose `Edit Cells` > `Transform...`
2. This will open up a window into which you can type a GREL expression. GREL stands for Google Refine Expression Language.

![OR_Transform](https://datacarpentry.org/openrefine-socialsci/fig/OR_02_Transform.png)

3. First we will remove all of the left square brackets (`[`). In the Expression box type `value.replace("[", "")` and click `OK`.

4. What the expression means is this: Take the `value` in each cell in the selected column and replace all of the `"["` with `""` (i.e. nothing - delete).

5. Click `OK`. You should see in the `items_owned` column that there are no longer any left square brackets. 

### Exercise 3
Use this same strategy to remove the single quote marks (`'`), the  right square brackets (`]`), and spaces from the `items_owned` column.

> ### Solution
> 1. `value.replace("'", "")`
> 2. `value.replace("]", "")`
> 3. `value.replace(" ", "")`  

You should now have a list of items separated by semi-colons (`;`). 

Now that we have cleaned out extraneous characters from our `items_owned` column, we can use a text facet to see which items 
were commonly owned or rarely owned by the interview respondents.

1. Click the down arrow at the top of the `items_owned` column. Choose `Facet` > `Custom text facet...`
2. In the `Expression` box, type `value.split(";")`. 
3. Click `OK`.

You should now see a new text facet box in the left-hand pane.

### Exercise 4
Which two items are the most commonly owned? Which are the two least commonly owned?

> ### Solution
> Select `Sort by:` `count`. The most commonly owned items are mobile phone and radio, the least commonly owned are cars and computers. 

### Exercise 5
Perform the same clean up steps and customized text faceting for the `months_lack_food` column. Which month(s) were farmers more likely to lack food? 

> ### Solution
> - All four cleaning steps can be performed by combining `.replace` statements. The command is: `value.replace("[", "").replace("]", "").replace(" ", "").replace("'", "")`. This can also be done in four separate steps if preferred.
> - November was the most common month for respondents to lack food.

### Exercise 6
Perform the same clean up steps for the `months_no_water`, `liv_owned`, `res_change`, and `no_food_mitigation` columns.
Hint: To reuse a GREL command, click the `History` tab and then click `Reuse` next to the command you would like to apply to that column.

## Using undo and redo.

It's common while exploring and cleaning a dataset to discover after you've made a change that you really should have done something else first. OpenRefine provides `Undo` and `Redo` operations to make this easy.

### Exercise 7
1. Click where it says `Undo / Redo` on the left side of the screen. All the changes you have made so far are listed here.
2. Click on the step that you want to go back to, in this case go back several steps to before you had done any text transformation. 
3. Visually confirm that those columns now contain the special characters that we had removed previously.
4. Notice that you can still click on the later steps to `Redo` the actions. Before moving on to the next lesson, redo all the steps in your analysis so that all of the column you modified are lacking in square brackets, spaces, and single quotes.

## Trim Leading and Trailing Whitespace

Words with spaces at the beginning or end are particularly hard for we humans to tell from strings without, but the blank characters will make a difference to the computer. We usually want to remove these. OpenRefine provides a tool to remove blank characters from the beginning and end of any entries that have them.

1. Create a new text facet for the column `respondent_wall_type`. You 
should see some choices that appear identical (`burntbricks` and 
`muddaub` both have two choices). In reality, one of these choices
includes either leading or trailing whitespace. 
2. To remove the whitespace, choose `Edit cells` > `Common transforms` > `Trim leading and trailing whitespace`.
3. You should now see only four choices in your text facet. 
