# javascript-challenge
<!-- cloned from alplky/javascript-challenge -->
## Background
Provided with a dataset of UFO sightings, create a dynamic table that will filter and show data based on user input. 

## Technologies Used
- JavaScript
- D3
- HTML
- CSS

## Objectives
- UFO Level 1: Automatic Table and Date Search

    Use a date form in the HTML document and write JavaScript code that will listen for events and search through the date/time column to tind rows that match user input. 
- UFO Level 2: Multiple Search Categories
    Using multiple input tags, write JavaScript code so the user can set multiple filters and search for UFO sightings based on the following table columns: date, city, state, country, shape (of UFO).

### UFO Level 1
```javascript
// function to show data 
function tableData(data) {
    
    let table = d3.select("#ufo-table")

    table.selectAll("tr").remove()
    
    // set up header row
    let headerRow = table.append("tr")

    headerRow.append("th").text("Datetime")
    headerRow.append("th").text("City")
    headerRow.append("th").text("State")
    headerRow.append("th").text("Country")
    headerRow.append("th").text("Shape")
    headerRow.append("th").text("Duration (min)")
    headerRow.append("th").text("Comments")

    // set up table body
    let tableBody = table.append("tbody")

    data.forEach((d) => {
        let row = tableBody.append("tr")
        row.append("td").text(d.datetime)
        row.append("td").text(d.city)
        row.append("td").text(d.state)
        row.append("td").text(d.country)
        row.append("td").text(d.shape)
        row.append("td").text(d.durationMinutes)
        row.append("td").text(d.comments)
    })

}

// create function to filter by date input
function handleClick() {
    let dateInput = d3.select("#datetime").property("value")
    let filteredDate = data.filter((d) => d.datetime === dateInput)

    tableData(filteredDate)
}

// pass id for button and function to click
d3.select("#filter-btn").on("click", handleClick)

```

### UFO Level 2
Instead of having the user enter inputs into the same field, multiple fields were created for each search category. 

```html
<li class="filter list-group-item">

    <!-- multiple filters -->
     <label for="date">Enter a Date</label>
    <input class="form-control" id="datetime" type="text" placeholder="1/1/2010">

    <label for="city">Enter a City</label>
    <input class="form-control" id="city" type="text" placeholder="fresno">

    <label for="state">Enter a State</label>
    <input class="form-control" id="state" type="text" placeholder="ca">

    <label for="country">Enter a Country</label>
    <input class="form-control" id="country" type="text" placeholder="us">

    <label for="shape">Enter a UFO shape</label>
    <input class="form-control" id="shape" type="text" placeholder="triange">

</li>
```

The table set up for Level 2 was exactly the same as Level on. The only difference was how the table was filtered based on user input. Here a variable was created for each avaiable input field. Then the data was filtered based on a user input using || (or) so the user can choose any of the fields and receive data back. 

```javascript
// create function to filter by various inputs
function handleClick() {
    let dateInput = d3.select("#datetime").property("value")
    let cityInput = d3.select("#city").property("value")
    let stateInput = d3.select("#state").property("value")
    let countryInput = d3.select("#country").property("value")
    let shapeInput = d3.select("#shape").property("value")

    let filteredData = data.filter((d) => d.datetime === dateInput || 
                                            d.city === cityInput ||
                                            d.state === stateInput ||
                                            d.country === countryInput ||
                                            d.shape === shapeInput)

    tableData(filteredData)

}

// pass id for button and function to click
d3.select("#filter-btn").on("click", handleClick)
```
