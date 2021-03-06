# brewdog

Live at https://elated-goldberg-1ba6ec.netlify.com/

---

## Project Setup

### Using Docker

#### Start

```
docker-compose up
```

Open browser to http://localhost:8081

#### Stop

```
docker-compose stop
```

### Using Yarn

```
yarn install
```

#### Compiles and hot-reloads for development

```
yarn serve
```

#### Compiles and minifies for production

```
yarn build
```

---

## Part 1 Requirements

- [x] Search input field
- [x] Submit button
- [x] Two radio buttons - one to search by food pairing and one to search by beer name
- [x] Dropdown menu to sort the results - selection defaults to “None”
- [x] Menu items: None, Beer Name, First Brewed Date, ABV
- [x] Search results list
- [x] Page must be responsive - the size and layout of elements should adjust based off screen size

## Part 2 Requirements

- [x] When the submit button is clicked or the enter key is pressed with the search input field in focus, any previous search results should be removed and the new query should be performed. The selected radio button will determine which URL parameters are used. If it’s search by food, use the “food” parameter. If it’s search by name, use the “beer_name” parameter.
- [x] On submit, if the input field is empty, display an error message notifying that a search term is required (how that message is displayed is up to you)
- [x] The API request must be asynchronous
- [x] A loading indicator must be displayed while the request is being performed
- [x] Display the number of results returned
- [x] If no results are returned, display a message that nothing was found
- [x] If a sort by option was specified, apply the sort to the results before displaying them

## Part 3 Requirements

- [x] The search results list should display the following info about each beer:

  - Name
  - Image
  - First brewed date
  - Description
  - ABV

- [x] When the sort by option is changed, any existing results should update to the new sort order (bonus points if you include a slick re-sort animation).

## Bonus Requirements

- [ ] Ability to save your favorite beers - e.g. save selections to local storage
- [ ] Make the beers clickable and on click, expand or popup a modal with the full details of the beer
- [ ] Search by brewed before/after date range, set via a datepicker
- [ ] Pagination controls - the default page size is 25 but can be increased via URL parameter
- [ ] Save the state of the page so that refreshing returns you back to where you left off
- [ ] Use popular state management techniques or libraries to demonstrate scalability
