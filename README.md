# Opvia Take-home Product Challenge

## Completed by: Kenan Garayev

## App & Its Features (User's Perspective)

### Main Features

- A table with the scientific data (datetime and numbers) is rendered to the screen
- A user could click a "calculation column" button and an additional input box along with specific arithmetic operator buttons and other useful functional buttons appears. this is a restricted input box with only specific input values could be used.
- the input values could be either the columns that a user could select (by clicking to any cells contained within those columns) or clicking the specific arithmetic operator buttons.
- Any sensible valid arithmetic formula could be constructed. If a formula is invalid, nothing will happen and a small error message will appear.
- If a formula is valid and a user is happy to proceed, a submit button could be clicked. This will add a column to the righ tof the table with the results of the formula (i.e. the formula output) for each row of the table except for the last. For example, a user could create a column to calculate 'Cell Density \* Volume'.
- Any number of reuslts columns could be added with different formulas.
- Results columns could be removed also by pressing the corresponding button.
- for each column, the last row is reserved. A dropdown menu in each cell of that last row can be used to select a column aggregation function (max, min, median). Once selected, the cell will show the aggregated value.
- Calculation Columns: Users can add a new column to the table after they input the formula and if the formula is valid.

### Additional/Prospective Features

- Enhannse the UI - add more features for the ease of user experience. For instance, use the Blueprint in-build features and properties to the maximum. Like adjusting row heights. Also, make the column creation a bit more dynamic and seamless.
- Add a reset functionality for the aggregation row.
- Add a functionality to take a result column titles/names, so a user could see viually what each added column represents.
- Column delete functionality at the top of each column (i.e. almost a little "x" icon at the corner of each column).
- Formula input could be less restrictive. Instead of using buttons, a keyboarded input combined with the cell/column selection could be used for an easier user experience.
- Improved visua/design changes.
- More responsive design (different screen sizes etc.) and better accessibilit (semantic html).
- Add error if the column aggregation is not possible due to the specific data type in that column.

## Code and Structure (Software Engineers' Perspective)

### How the code works

- Using Blueprint Core and Table components.
- Storing different state variable to add the requested features (local state).
- When calculation column button is clicked, a FormulaInput component is rendered. This component includes a space for the formula to be displayed as well as additional buttons for arithmetic operators and clear and submit and remove functionality.

- When either a cell or arithmetic operator is clicked, addToFormula() function is called to add the characted to the formula string stored in the state. This function is either called directly by the operators or from inside the onCellFocus() callback function that specifically adds a column name to the formula by lookng up the columns array (array of objects)
- When clearFormula button is clicked clearFormula() function is called to clear the formula state variable
- When the submit button is clicked, evalFormula() function is called. This function is at the heart of this functionality. It essentially uses math.js module to evaluate the formula at each row by replacing the column names with the individual numerical values for each row. If there is an error in formula evaluation, then an error message is shown to the user (through setting a state variable setFormulaError). If all is okay, then the new results column is added to the list of results columns by calling the addResultsCol() function.
- addResultsCol() function basically adds the result to a allResultsCols state variable (array of arrays, i.e. matrix) as well as updates the header names of these columns by updating the colHeaders state variable (array of objects). Similarly, removeResultsCol() function, removes these.
- getSparseRefFromIndexes() function converts row and column index (numbers) into a special string representation to look up the data from the dummyData.
- cellRenderer() function that is passed as a callback to a Column component and that has rowIndex and columnIndex as parameters. It has multiple flows depending on certain conditions:
  1. If we are at the last row (a special case), then the function will return a special cell contianing a drop down menu to select aggregation type. If an appropriate option is selected,

### Opportunities for Improvement of the Code

- Storing Original Column Data: To enhance performance and flexibility, consider storing the original column data in the component's state or abstracting away the data extraction process.
- State Management: Implement a state management solution like Redux Toolkit to manage the component's state more efficiently, especially when dealing with complex data manipulation.
- Modular Code: Consider abstracting the functions into separate modules and importing them to improve code organization and maintainability.

### Rate of Change Calculations

1. Process time-based data format (like the one in the column 0) by the evalFormula function in addition to numbers. For example, users could input expressions like (Cell Count[0] - Cell Count[1]) / (Time[0] - Time[1]) to calculate the rate of cell count growth.
2. Modify the formula evaluation process to handle time-based calculations by incorporating timestamps or time-related data from the original data source.
3. If the time-based calculation is applied, it needs to be obvious that the first row will have a value of 0 (since there is no previous value to calculate the rate of growth from - i.e. relative value).

---

### Original Readme

Congratulations on being selected for the next stage of our interview process!

We really appreciate the time you have invested in the process so far and only invited you to this next challenge because we think there's a very good chance you'd be a great fit at Opvia. This is the penultimate step in the interview process! For context at this stage the probability of a candidate receiving an offer is (~25%).

This is our only opportunity to see how you deliver on a product problem, so we it very highly.

## How to complete this stage of the interview process

1. Please clone this repo and use it as your starting point. This is a simple create-react-app featuring the blueprintjs table component https://blueprintjs.com/docs/#table
2. Complete the 'Opvia product problem' below
3. When you are done, create a private repo and push your code to it
4. Invite _hfmw_ & _OliverWales_ to view the repo

## Opvia product problem

Scientists are using Opvia to store all their data in a standardised structure. The example data has come from a scientists who is uploading their bioreactor data into Opvia.

They have said that it would be useful if they could calculate the cell count in Opvia, as well as being able to see its maximum value.

The Opvia platform allows scientists to build what they need. So, instead of building in these specific features, we have identified two higher level features which would enable the customer to achieve what they need, whilst also being useful for other use-cases.

1. `Calculation columns`, where the user can add a column with a formula such as `Cell Density * Volume`
2. `Column aggregations`, where the user can aggregate data from a column e.g. `Max Cell Count`

You have a call scheduled with the scientist. Build a working MVP that you could give the user access to to get their feedback.

In the readme describe what improvements you would make, and how you would make it possible to do `Rate of change calculations` e.g. `Rate of Cell Count Growth`

#### FAQS

- Can I change the structure/content of the raw data? - yes feel free to, but don't feel obligated to (this is a product not an engineering challenge)
- Where is the data coming from? It's from an instrument (a bioreactor).
- Unsure whether to submit? Would you happily get on a call with a scientist and give them access? Would what you've showed them make them more excited about using Opvia?
- Ran out of time? Document any features that you'd like to have built.
- I have a question? Please ask!! Email `oli@opvia.io` and cc `will@opvia.io`
- How should I communicate? Please over communicate. We want to learn what it's like to work with you :)
- Do I need to write tests? - not unless it helps you! We're just looking for "a working MVP that you could give the user access to to get their feedback"
