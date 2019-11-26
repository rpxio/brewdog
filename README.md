# brewdog

## Part 1 Requirements

- [x] Search input field
- [x] Submit button
- [ ] Two radio buttons - one to search by food pairing and one to search by beer name
- [ ] Dropdown menu to sort the results - selection defaults to “None”
- [ ] Menu items: None, Beer Name, First Brewed Date, ABV
- [x] Search results list
- [ ] Page must be responsive - the size and layout of elements should adjust based off screen size

## Part 2 Requirements

- [ ] When the submit button is clicked or the enter key is pressed with the search input field in focus, any previous search results should be removed and the new query should be performed. The selected radio button will determine which URL parameters are used. If it’s search by food, use the “food” parameter. If it’s search by name, use the “beer_name” parameter.
- [ ] On submit, if the input field is empty, display an error message notifying that a search term is required (how that message is displayed is up to you)
- [ ] The API request must be asynchronous
- [ ] A loading indicator must be displayed while the request is being performed
- [ ] Display the number of results returned
- [ ] If no results are returned, display a message that nothing was found
- [ ] If a sort by option was specified, apply the sort to the results before displaying them

## Part 3 Requirements

- [x] The search results list should display the following info about each beer:

  - Name
  - Image
  - First brewed date
  - Description
  - ABV

- [ ] When the sort by option is changed, any existing results should update to the new sort order (bonus points if you include a slick re-sort animation).

## Bonus Requirements

- [ ] Ability to save your favorite beers - e.g. save selections to local storage
- [ ] Make the beers clickable and on click, expand or popup a modal with the full details of the beer
- [ ] Search by brewed before/after date range, set via a datepicker
- [ ] Pagination controls - the default page size is 25 but can be increased via URL parameter
- [ ] Save the state of the page so that refreshing returns you back to where you left off
- [ ] Use popular state management techniques or libraries to demonstrate scalability

---

## Project setup

```
yarn install
```

### Compiles and hot-reloads for development

```
yarn serve
```

### Compiles and minifies for production

```
yarn build
```

### Lints and fixes files

```
yarn lint
```

### Customize configuration

See [Configuration Reference](https://cli.vuejs.org/config/).
